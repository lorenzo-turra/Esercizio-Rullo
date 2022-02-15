# Esercizio-Rullo

è necessaria per il controllo del servomotore, tramite il quale viene regolata la posizione di un astina necessaria per lo smistamento dei pacchi. Il servomotore è collegato tramite dei cavi ai pin della scheda stm32. Nello specifico è collegato al pin PA1, il quale  è settato come alternate function ed è assegnato ad un timer (PA1 -> TIM5_CH2) che genera un segnale PWM, necessario alla regolazione della posizione del servomotore. Questa task deve essere in funzione quando la TaskRilevaColore() rivela di che colore è il  pacco. Se il pacco è di colore nero il servomotore lo smisterà a destra mentre se è bianco a sinistra.
 

