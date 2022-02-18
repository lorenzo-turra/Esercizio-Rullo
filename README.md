:smile: _Esercizio di Lorenzo Turra_ :smile:


## _Esercizio-Rullo_


# **_SERVOMOTORE_**

![immagine rappresentativa servomotore](https://www.pintoelettronica.com/files/np_Files/Foto/20079_2.PNG)
 
 **_inntroduzione teorica_**
 
 
Il servomotore è un particolare tipo di motore, generalmente di piccola potenza. 

A differenza dei motori tradizionali che ruotano in modo continuo, rimane fisso su una posizione;   Può essere:

  _° elettrico_ 
  
  _° pneumatico_ 
  
  _° idraulico._ 
  
  
I servomotori trovano applicazione nei controlli di posizione,
nelle macchine a controllo numerico e nei sistemi automatici di regolazione e nelle periferiche di sistema, 
come stampanti e plotter.
Possono ruotare con un angolo compreso tra 0° e 180°, mantenendo stabilmente la posizione raggiunta. 
_(in realtà esistono anche alcuni servo che ruotano a 360° ma sono una minoranza)_

**_Utilizzo servomotore nel progetto, tramite la creazione di task_**

TaskSmistaOggettpo è necessaria per il controllo del servomotore, tramite il quale viene regolata la posizione di un astina necessaria per lo smistamento dei pacchi. Il servomotore è collegato tramite dei cavi ai pin della scheda stm32. Nello specifico è collegato al pin PA1, il quale  è settato come alternate function ed è assegnato ad un timer (PA1 -> TIM5_CH2) che genera un segnale PWM, necessario alla regolazione della posizione del servomotore. Questa task deve essere in funzione quando la TaskRilevaColore() rivela di che colore è il  pacco. Se il pacco è di colore nero il servomotore lo smisterà a destra mentre se è bianco a sinistra.
 
 **_Foto rappresentative schemi elettrici Schedina e Servomotore_**
 
 ![foto rappresentativa schema elettrico schedina](https://github.com/lorenzo-turra/Esercizio-Rullo/blob/main/SchemaElettricoSchedina.PNG)_Schema elettrico schedina_
 ![foto rappresentativa schema elettrico servomotore](https://github.com/lorenzo-turra/Esercizio-Rullo/blob/main/SchemaElettricoServoMotore.PNG)_Schema elettrico servomotore_ 
 
 **_Pilotaggio di un servomotore_**
 
Dobbiamo generare un segnale impulsivo con periodo di _20ms_ e impostare il _duty cycle_ in modo da avere la parte impulsiva con durata tra _1 e 2ms_. _L’ampiezza_ del segnale dipende dal servomotore che andiamo a scegliere e di solito compresa tra _3,3V e 7,2V_

