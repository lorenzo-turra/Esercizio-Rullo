# Esercizio-Rullo


descrizione progetto

Creare un nastro trasportatore che rallenta alla rilevazione dell'oggeto, individua se nero o bianco e infine lo smista se bianco a sinistra e se nero a destra.


//=== INCLUDES =============================================================================
#include "FreeRTOSConfig.h"             // ARM.FreeRTOS::RTOS:Config
#include "FreeRTOS.h"   
#include "task.h"                       // ARM.FreeRTOS::RTOS:Core
#include "timer.h"                     	// ARM.FreeRTOS::RTOS:Timers
#include "event_groups.h"               // ARM.FreeRTOS::RTOS:Event Groups
#include <stdio.h>
#include "Servo.h"
#include "Led.h"
#include "Arduino.h"

extern EventGroupHandle_t xServo;

void ServoMotoreInit(void){
	RCC->AHB2ENR |= RCC_AHB2ENR_GPIOEEN;
	GPIOE->MODER &= ~GPIO_MODER_MODE11_Msk;
	GPIOE->MODER |= GPIO_MODER_MODE11_1;
	GPIOE->AFR[1] &= ~GPIO_AFRH_AFSEL11_Msk;
	GPIOE->AFR[1] |= GPIO_AFRH_AFSEL11_0;

	TIM1_CH2_PWM(1551);
	
	xTaskCreate(vTaskSmistaDx, /* Pointer to the function that implements the task.              */
	"Task 4 (Smista destra)",    /* Text name for the task.  This is to facilitate debugging only. */
	50,   /* Stack depth in words.                */
	NULL,  /* We are not using the task parameter. */
	1,     /* This task will run at priority 1.    */
	NULL); /* We are not using the task handle.    */
	xTaskCreate(vTaskSmistaSx, /* Pointer to the function that implements the task.              */
	"Task 5 (Smista sinistra)",    /* Text name for the task.  This is to facilitate debugging only. */
	50,   /* Stack depth in words.                */
	NULL,  /* We are not using the task parameter. */
	1,     /* This task will run at priority 1.    */
	NULL); /* We are not using the task handle.    */
}

void ServoMotoreTestInit(void){
	xTaskCreate(vTaskPA0, /* Pointer to the function that implements the task.              */
		"Task 1 (PA0 check)",    /* Text name for the task.  This is to facilitate debugging only. */
		50,   /* Stack depth in words.                */
		NULL,  /* We are not using the task parameter. */
		1,     /* This task will run at priority 1.    */
		NULL); /* We are not using the task handle.    */
	xTaskCreate(vTaskPA1, /* Pointer to the function that implements the task.              */
		"Task 2 (PA1 check)",    /* Text name for the task.  This is to facilitate debugging only. */
		50,   /* Stack depth in words.                */
		NULL,  /* We are not using the task parameter. */
		1,     /* This task will run at priority 1.    */
		NULL); /* We are not using the task handle.    */
}

void vTaskSmistaDx(void * pvParameters){
	const EventBits_t xBitsToWaitFor = EVENT_SMISTADX;
	while(1){
		xEventGroupWaitBits(xServo,xBitsToWaitFor,pdTRUE,pdTRUE,portMAX_DELAY);
		LedRossoToggle();
		TIM1->CCR2 = 800;	//Sposta a 0�
		vTaskDelay(700);
		TIM1->CCR2 = 2500; //Va a 150�
		vTaskDelay(1500);
		TIM1->CCR2 = 10000;//Sposta a 0�
	}
}

void vTaskSmistaSx(void * pvParameters){
	const EventBits_t xBitsToWaitFor = EVENT_SMISTASX;
	while(1){
		xEventGroupWaitBits(xServo,xBitsToWaitFor,pdTRUE,pdTRUE,portMAX_DELAY);
		LedVerdeToggle();
		TIM1->CCR2 = 2500;
		vTaskDelay(700);
		TIM1->CCR2 = 800;
		vTaskDelay(1500);
		TIM1->CCR2 = 10000;
	}
}

void vTaskPA0(void * pvParameters){
	while(1){
		while(!digitalRead(PA0));
		while(digitalRead(PA0)){;}
			xEventGroupSetBits(xServo, EVENT_SMISTASX);
	}	
}

void vTaskPA1(void * pvParameters){
	while(1){
		while(!digitalRead(PA1));
		while(digitalRead(PA1)){;}
			xEventGroupSetBits(xServo, EVENT_SMISTADX);
	}	
}

