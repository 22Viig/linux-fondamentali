---
layout: page
title: I processi
permalink: /01-processi/

---


I processi sono i programmi in esecuzione sul computer. Sono gestiti dal kernel, dove a ogni processo è associato un ID, noto anche come PID . Il PID aumenta in base all'ordine di avvio del processo. Ad esempio, il 60° processo avrà un PID pari a 60.

## Visualizzazione dei processi

Possiamo usare il ***`ps`*** per fornire un elenco dei processi in esecuzione come sessione del nostro utente e alcune informazioni aggiuntive come il suo codice di stato, la sessione che lo sta eseguendo, quanto tempo di utilizzo della CPU sta utilizzando e il nome del programma o comando effettivamente in esecuzione.

Per visualizzare i processi eseguiti da altri utenti e quelli che non vengono eseguiti da una sessione (ad esempio i processi di sistema), dobbiamo usare: ***`ps aux`***

Un altro comando molto utile è il comando top; top fornisce statistiche in tempo reale sui processi in esecuzione sul sistema, anziché una visualizzazione una tantum. Queste statistiche si aggiornano ogni 10 secondi, ma si aggiornano anche quando si utilizzano i tasti freccia per scorrere le varie righe. Un altro ottimo comando per ottenere informazioni dettagliate sul sistema è il  ***`top`*** comando.

### Gestione dei processi

È possibile inviare segnali che terminano i processi; esistono diversi tipi di segnali che determinano esattamente quanto "pulitamente" il processo viene gestito dal kernel. Per terminare un comando, possiamo usare il comando ***`kill`*** con il nome appropriato e il PID associato che desideriamo terminare. 

Di seguito sono riportati alcuni dei segnali che possiamo inviare a un processo quando viene terminato:

SIGTERM - Termina il processo, ma consentigli di eseguire alcune attività di pulizia in anticipo
SIGKILL - Interrompe il processo - non esegue alcuna pulizia successiva
SIGSTOP - Arresta/sospendi un processo

### Come iniziano i processi?

Iniziamo parlando di namespaces. Il sistema operativo (SO) utilizza gli namespaces per suddividere le risorse disponibili sul computer tra i processi (come CPU, RAM e priorità). Immagina di suddividere il computer in fette, come una torta. I processi all'interno di quella fetta avranno accesso a una certa quantità di potenza di calcolo, che tuttavia rappresenterà una piccola parte di quella effettivamente disponibile per ogni processo nel suo complesso.

I namespaces sono ottimi per la sicurezza perché rappresentano un modo per isolare i processi dagli altri: solo quelli che si trovano nello stesso spazio dei nomi saranno in grado di vedersi a vicenda.

Abbiamo già parlato del funzionamento del PID , ed è qui che entra in gioco. Il processo con ID 0 è un processo che viene avviato all'avvio del sistema. Questo processo è l'init del sistema su Ubuntu, come ***`systemd`*** , che viene utilizzato per gestire i processi di un utente e si interpone tra il sistema operativo e l'utente. 

### Come avviare processi/servizi all'avvio

Alcune applicazioni possono essere avviate all'avvio del sistema di cui disponiamo. Ad esempio, server web, server di database o server di trasferimento file. Questi software sono spesso critici e gli amministratori ne ordinano l'avvio durante l'avvio del sistema.

In questo esempio, diremo al server web Apache di avviare Apache manualmente e poi diremo al sistema di avviare apache2 all'avvio.

Inseriamo l'uso di ***`systemctl`***-- questo comando ci permette di interagire con il processo/demone systemd . Proseguendo con il nostro esempio, ***`systemctl`*** è un comando facile da usare che accetta la seguente formattazione:***`systemctl`*** [option] [service]

Ad esempio, per dire ad Apache di avviarsi, useremo ***`systemctl`*** start apache2. Sembra abbastanza semplice, vero? Lo stesso vale per se volessimo arrestare Apache : basterebbe sostituire [option]con stop (invece di start come abbiamo fornito).

Possiamo fare quattro opzioni con ***`systemctl`***:
- Start
- Stop
- Enable
- Disable

### Introduzione al backgrounding e  al foregrounding  in Linux

I processi possono essere eseguiti in due stati: in background e in primo piano. Ad esempio, i comandi eseguiti nel terminale, come "echo" o simili, verranno eseguiti in primo piano, poiché sono gli unici comandi forniti a cui non è stato specificato di essere eseguiti in background. "Echo" è un ottimo esempio, poiché l'output di echo verrà visualizzato in primo piano, ma non in background.

Per eseguire processo in backgroud possiamo aggiungere al comando che vogliamo lanciare l'operatore ***`&`***. Ad esempio se vogliamo lanciare il background il processo generato dal comando ***`echo`*** possiamo scrivere ***`echo "Ciao!" &`***, l'output di questo comando non sarà ***`Ciao!`***, sarà invece l'id del processo che verrà eseguito, ad esempio 17882.

Possiamo fare esattamente lo stesso quando eseguiamo cose come gli script: invece di affidarci all'operatore &, possiamo usarlo ***`Ctrl + Z`*** sulla tastiera per mettere in background un processo. È anche un modo efficace per "mettere in pausa" l'esecuzione di uno script o di un comando.

Ora che abbiamo un processo in esecuzione in background, ad esempio uno script "background.sh", che può essere confermato utilizzando il comando  ***`ps aux`***, possiamo fare marcia indietro e riportare questo processo in primo piano per interagire con esso.

Con il nostro processo in background (eseguito con  ***`Ctrl + Z`*** o l'operatore ***`&`***), possiamo riportarlo in primo piano con il comando ***`fg`***.