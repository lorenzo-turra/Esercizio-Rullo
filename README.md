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

**_Componenti interni di un servo motore_**

Per ottenere questo particolare movimento, si deve analizzare in dettaglio come è composto all’interno un servo motore. La rotazione del perno in uscita si ottiene attraverso un motore DC (a corrente continua) collegato ad un meccanismo di demoltiplica che consente di aumentare la coppia in fase di rotazione, riducendo la velocità e aumentando la forza di torsione.

**_Componenti del meccanismo di demoltiplica e motore DC_**

Per quanto riguarda il controllo dell’angolo di rotazione, questo viene attuato attraverso un circuito di controllo interno che grazie ad un potenziometro resistivo riesce a conoscere l’angolo di rotazione del perno. Una volta raggiunto l’angolo desiderato, il circuito di controllo blocca il motore.

**_Come funzionano i servomotori_**

![immagine rappresentativa duty circle](https://www.ne555.it/wp-content/uploads/2018/03/pwm-arduino.jpg)
 _immagine rappresentativa duty cycle_
  

Un servo motore controlla la rotazione di un motore DC attraverso un circuito di controllo che ne regola l’angolo. Il controllo viene ottenuto regolando la lunghezza di un impulso ad onda quadra inviato al servo motore. 
Questo treno di impulsi si caratterizza dal duty cycle, cioè dal tempo occupato dall’impulso rispetto all’interno periodo destinato ad un singolo segnale.

Modulando quindi quindi queste durate durante l’invio di un treno di impulsi si possono inviare delle informazioni al sistema di controllo nel servo motore. A seconda del duty cycle, varierà l’angolo di rotazione. Partendo da un duty cycle del 1%, corrispondente all’angolo di 0°, via via incrementando il duty cycle, crescerà anche l’angolo di rotazione del servo motore. Con un duty cycle del 50%, il perno del motore si posizionerà su 90° (che è proprio la metà dell’intervallo di rotazione possibile). Con un duty cycle del 99%, avremo una rotazione di 180°


![immagine rappresentativa duty circle con servomotore](https://www.meccanismocomplesso.org/wp-content/uploads/2020/08/Arduino-PWM-duty-cycle-angolo-del-servo-motore.jpg)

_immagine rappresentativa duty circle con servomotore_
  

**_Utilizzo servomotore nel progetto, tramite la creazione di task_**

TaskSmistaOggettpo è necessaria per il controllo del servomotore, tramite il quale viene regolata la posizione di un astina necessaria per lo smistamento dei pacchi. Il servomotore è collegato tramite dei cavi ai pin della scheda stm32. Nello specifico è collegato al pin PA1, il quale  è settato come alternate function ed è assegnato ad un timer (PA1 -> TIM5_CH2) che genera un segnale PWM, necessario alla regolazione della posizione del servomotore. Questa task deve essere in funzione quando la TaskRilevaColore() rivela di che colore è il  pacco. Se il pacco è di colore nero il servomotore lo smisterà a destra mentre se è bianco a sinistra.
 
 **_Foto rappresentative schemi elettrici Schedina e Servomotore_**
 
 ![foto rappresentativa schema elettrico schedina](https://github.com/lorenzo-turra/Esercizio-Rullo/blob/main/SchemaElettricoSchedina.PNG)_Schema elettrico schedina_
 ![foto rappresentativa schema elettrico servomotore](https://github.com/lorenzo-turra/Esercizio-Rullo/blob/main/SchemaElettricoServoMotore.PNG)_Schema elettrico servomotore_ 
 
 **_Pilotaggio di un servomotore_**
 
Dobbiamo generare un segnale impulsivo con periodo di _20ms_ e impostare il _duty cycle_ in modo da avere la parte impulsiva con durata tra _1 e 2ms_. _L’ampiezza_ del segnale dipende dal servomotore che andiamo a scegliere e di solito compresa tra _3,3V e 7,2V_

***Grazie della visione --- Lorenzo Turra 5L***

link di riferimento 
[clicca qui](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)

link di riferimento
[clicca qui](https://docs.google.com/presentation/d/1yTK0-TrzFx8WaVb63fAroDZPwvzK_yD7E4AlsnlEozw/edit#slide=id.g109a595099c_0_214)
