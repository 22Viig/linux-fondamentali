---
layout: page
title: I processi
permalink: /01-processi/

---
- [1. Introduzione](#1-introduzione)
- [2. Automazione](#2-automazione)
- [3. Pacchetti](#3-pacchetti)
- [4. Log](#4-log)

## 1 Introduzione
I processi sono i programmi in esecuzione sul computer. Sono gestiti dal kernel, dove a ogni processo è associato un ID, noto anche come PID.

# 1.1 Visualizzazione dei processi

Possiamo usare il ***`ps`*** per fornire un elenco dei processi in esecuzione come sessione del nostro utente e alcune informazioni aggiuntive come il suo codice di stato, la sessione che lo sta eseguendo, quanto tempo di utilizzo della CPU sta utilizzando e il nome del programma o comando effettivamente in esecuzione.

Per visualizzare i processi eseguiti da altri utenti e quelli che non vengono eseguiti da una sessione (ad esempio i processi di sistema), dobbiamo usare: ***`ps aux`***

Un altro comando molto utile è il comando top; top fornisce statistiche in tempo reale sui processi in esecuzione sul sistema, anziché una visualizzazione una tantum. Queste statistiche si aggiornano ogni 10 secondi, ma si aggiornano anche quando si utilizzano i tasti freccia per scorrere le varie righe. Un altro ottimo comando per ottenere informazioni dettagliate sul sistema è il  ***`top`*** comando.

# 1.2 Gestione dei processi

È possibile inviare segnali che terminano i processi; esistono diversi tipi di segnali che determinano esattamente quanto "pulitamente" il processo viene gestito dal kernel. Per terminare un comando, possiamo usare il comando ***`kill`*** con il nome appropriato e il PID associato che desideriamo terminare. 

Di seguito sono riportati alcuni dei segnali che possiamo inviare a un processo quando viene terminato:

SIGTERM - Termina il processo, ma consentigli di eseguire alcune attività di pulizia in anticipo
SIGKILL - Interrompe il processo - non esegue alcuna pulizia successiva
SIGSTOP - Arresta/sospendi un processo

# 1.3 Come iniziano i processi?

Iniziamo parlando di namespaces. Il sistema operativo (SO) utilizza gli namespaces per suddividere le risorse disponibili sul computer tra i processi (come CPU, RAM e priorità). Immagina di suddividere il computer in fette, come una torta. I processi all'interno di quella fetta avranno accesso a una certa quantità di potenza di calcolo, che tuttavia rappresenterà una piccola parte di quella effettivamente disponibile per ogni processo nel suo complesso.

I namespaces sono ottimi per la sicurezza perché rappresentano un modo per isolare i processi dagli altri: solo quelli che si trovano nello stesso spazio dei nomi saranno in grado di vedersi a vicenda.

Abbiamo già parlato del funzionamento del PID , ed è qui che entra in gioco. Il processo con ID 0 è un processo che viene avviato all'avvio del sistema. Questo processo è l'init del sistema su Ubuntu, come ***`systemd`*** , che viene utilizzato per gestire i processi di un utente e si interpone tra il sistema operativo e l'utente. 

# 1.4 Come avviare processi/servizi all'avvio

Alcune applicazioni possono essere avviate all'avvio del sistema di cui disponiamo. Ad esempio, server web, server di database o server di trasferimento file. Questi software sono spesso critici e gli amministratori ne ordinano l'avvio durante l'avvio del sistema.

In questo esempio, diremo al server web Apache di avviare Apache manualmente e poi diremo al sistema di avviare apache2 all'avvio.

Inseriamo l'uso di ***`systemctl`***-- questo comando ci permette di interagire con il processo/demone systemd . Proseguendo con il nostro esempio, ***`systemctl`*** è un comando facile da usare che accetta la seguente formattazione:***`systemctl`*** [option] [service]

Ad esempio, per dire ad Apache di avviarsi, useremo ***`systemctl`*** start apache2. Sembra abbastanza semplice, vero? Lo stesso vale per se volessimo arrestare Apache : basterebbe sostituire [option]con stop (invece di start come abbiamo fornito).

Possiamo fare quattro opzioni con ***`systemctl`***:
- Start
- Stop
- Enable
- Disable

# 1.5 Introduzione al backgrounding e  al foregrounding  in Linux

I processi possono essere eseguiti in due stati: in background e in primo piano. Ad esempio, i comandi eseguiti nel terminale, come "echo" o simili, verranno eseguiti in primo piano, poiché sono gli unici comandi forniti a cui non è stato specificato di essere eseguiti in background. "Echo" è un ottimo esempio, poiché l'output di echo verrà visualizzato in primo piano, ma non in background.

Per eseguire processo in backgroud possiamo aggiungere al comando che vogliamo lanciare l'operatore ***`&`***. Ad esempio se vogliamo lanciare il background il processo generato dal comando ***`echo`*** possiamo scrivere ***`echo "Ciao!" &`***, l'output di questo comando non sarà ***`Ciao!`***, sarà invece l'id del processo che verrà eseguito, ad esempio 17882.

Possiamo fare esattamente lo stesso quando eseguiamo cose come gli script: invece di affidarci all'operatore &, possiamo usarlo ***`Ctrl + Z`*** sulla tastiera per mettere in background un processo. È anche un modo efficace per "mettere in pausa" l'esecuzione di uno script o di un comando.

Ora che abbiamo un processo in esecuzione in background, ad esempio uno script "background.sh", che può essere confermato utilizzando il comando  ***`ps aux`***, possiamo fare marcia indietro e riportare questo processo in primo piano per interagire con esso.

Con il nostro processo in background (eseguito con  ***`Ctrl + Z`*** o l'operatore ***`&`***), possiamo riportarlo in primo piano con il comando ***`fg`***.

## 2 Automazione
Per automazione intendiamo la pianificazione dell'esecuzione di una determinata azione o attività dopo l'avvio del sistema. Ad esempio, l'esecuzione di comandi, il backup di file o l'avvio dei propri programmi preferiti.

Parleremo del comando ***`cron`***, ma più specificamente di come possiamo interagire con esso tramite l'uso di ***`crontabs`*** . Crontab è uno dei processi che viene avviato all'avvio, responsabile della facilitazione e della gestione dei cron job.

Un crontab è semplicemente un file speciale con una formattazione che viene riconosciuta dal ***`cron`*** per eseguire ogni riga passo dopo passo. I crontab richiedono 6 valori specifici:

Valore	Descrizione
- MIN: A che minuto eseguire
- HOUR: A che ora eseguire
- DOM: In quale giorno del mese eseguire
- MON: In quale mese dell'anno eseguire
- DOW: In quale giorno della settimana eseguire l'operazione?
- CMD: Il comando effettivo che verrà eseguito.

Usiamo l'esempio del backup dei file. Potresti voler eseguire il backup dei "Documenti" ogni 12 ore. Utilizzeremmo la seguente formattazione: 

***`0 */12 * * * cp -R /home/Documents /var/backups/`***

Una caratteristica interessante dei crontab è che supportano anche il carattere jolly o asterisco ***`*`***. Se non vogliamo specificare un valore per quel campo specifico, ovvero non ci interessa in quale mese, giorno o anno venga eseguito, ma solo che venga eseguito ogni 12 ore, inseriamo semplicemente un asterisco.

I crontab possono essere modificati utilizzando ***`crontab -e`***, dove puoi selezionare un editor (come Vim) per modificare il tuo crontab.

## 3 Pacchetti

# 3.1 I repository software

Quando gli sviluppatori desiderano inviare software alla comunità, lo inviano a un repository " apt ". Se approvati, i loro programmi e strumenti vengono rilasciati.  Due delle caratteristiche più apprezzabili di Linux emergono qui: l'accessibilità per l'utente e il valore degli strumenti open source.

Sebbene i fornitori di sistemi operativi gestiscano i propri repository, è anche possibile aggiungere repository della community al proprio elenco! Questo consente di estendere le funzionalità del sistema operativo. È possibile aggiungere repository aggiuntivi utilizzando il ***`add-apt-repository`***  o elencando un altro fornitore! Ad esempio, alcuni fornitori avranno un repository più vicino alla loro posizione geografica.

# 3.2 Gestione dei repository

Normalmente utilizziamo il comando ***`apt`*** per installare software sul nostro sistema Ubuntu. Il comando fa parte del software di gestione dei pacchetti, anch'esso chiamato apt. Apt contiene un'intera suite di strumenti che ci permette di gestire i pacchetti e le sorgenti del nostro software, e di

Un metodo per aggiungere repository è usare il comando ***`add-apt-repository`*** illustrato sopra, ma ora spiegheremo  come aggiungere e rimuovere manualmente un repository . Sebbene sia possibile installare software tramite programmi di installazione di pacchetti come dpkg, il vantaggio di apt è che ogni volta che aggiorniamo il nostro sistema, anche il repository che contiene i software che aggiungiamo viene controllato per verificare la presenza di aggiornamenti. 

In questo esempio, aggiungeremo l'editor di testo Sublime Text alla nostra macchina Ubuntu come repository, poiché non fa parte dei repository predefiniti di Ubuntu. Quando aggiungiamo software, l'integrità di ciò che scarichiamo è garantita dall'uso delle cosiddette chiavi GPG (Gnu Privacy Guard). Queste chiavi sono essenzialmente un controllo di sicurezza da parte degli sviluppatori, che affermano: "Ecco il nostro software". Se le chiavi non corrispondono a quelle ritenute attendibili dal sistema e a quelle utilizzate dagli sviluppatori, il software non verrà scaricato.

Quindi, per iniziare, dobbiamo scaricare e aggiungere la chiave GPG, utilizziamo ***`apt-key`*** per considerarla attendibile.  Ora che abbiamo aggiunto questa chiave alla nostra lista di fonti attendibili, possiamo aggiungere il repository del software che ci interessa alla nostra lista di fonti apt. È buona norma avere un file separato per ogni repository di terze parti/community che aggiungiamo.Creiamo un file denominato nostro_sofware.list in /etc/apt/sources.list.d e inseriamo le informazioni del repository del software. Dopo aver aggiunto questa voce, dobbiamo aggiornare apt per riconoscere questa nuova voce: questo si fa usando il comando ***`apt update`*** . Una volta aggiornato con successo, possiamo ora procedere all'installazione del software di cui ci siamo fidati e che abbiamo aggiunto ad apt utilizzando ***`apt install [nostro-software]`***. 

Rimuovere i pacchetti è facile come fare il contrario. Questo processo si esegue utilizzando il comand ***`add-apt-repository --remove ppa:PPA_Name/ppa`*** o eliminando manualmente il file precedentemente aggiunto. Una volta rimosso, possiamo semplicemente usare ***`apt remove [nostro-software]`***.

## 4 Log

Situati nella directory /var/log, questi file e cartelle contengono informazioni di log per le applicazioni e i servizi in esecuzione sul sistema. Il sistema operativo ( SO ) è diventato piuttosto efficiente nel gestire automaticamente questi log, secondo un processo noto come "rotating" (rotazione).

Questi servizi e log sono un ottimo modo per monitorare lo stato di salute del sistema e proteggerlo. Non solo, i log di servizi come un server web contengono informazioni su ogni singola richiesta, consentendo a sviluppatori o amministratori di diagnosticare problemi di prestazioni o indagare sull'attività di un intruso (vedi access.log e error.log).

Naturalmente, esistono altri registri che memorizzano informazioni su come funziona il sistema operativo e sulle azioni eseguite dagli utenti, come i tentativi di autenticazione.


