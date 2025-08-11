---
layout: page
title: I fondamentali di Linux - Part. 2
args: (SSH, Flags e Switches, File System, permessi, directory comuni)
permalink: /linux-02/

---
- [1. Secure Shell - SSH](#1-secure-shell)
- [2. Flags e Switches](#2-flags-e-switches)
- [3. File System](#3-file-system)

## 1 Secure Shell

Secure Shell o SSH è semplicemente un protocollo crittografato tra dispositivi. Utilizzando la crittografia, qualsiasi input inviato in un formato leggibile viene crittografato per essere trasmesso in rete, dove viene poi decrittografato una volta raggiunto il computer remoto.

Secure Shell viene utilizzata per connettersi ad una macchina connessa in rete e abilitata alla connessione mediante il comando ***`ssh`*** seguito dal nome utente dell'account con il quale ci si vuole connettere e dal carattere @ (at) e l'indirizzo IP della macchina. Ad esempio ***`ssh root@[IP-DELLA-MACCHINA]`***. Il comando avvia la connessione, a questo punto la macchina chiede di inserire la password dell'utente. Nota: quando digiti una password in un prompt di accesso SSH non c'è alcun feedback visibile: non vedrai alcun testo o simbolo apparire mentre digiti la password. Tuttavia, funziona comunque, quindi digita semplicemente la password e premi Invio per accedere.

## 2 Flags e Switches

La maggior parte dei comandi consente di specificare argomenti. Questi argomenti sono identificati da un trattino e da una parola chiave specifica, nota come flag o switch.

Più avanti discuteremo come possiamo identificare quali comandi consentono di fornire argomenti e capiremo esattamente a cosa servono.

Quando si utilizza un comando, salvo diversa indicazione, verrà eseguito il comportamento predefinito. Ad esempio,  ls verrà visualizzato il contenuto della directory di lavoro. Tuttavia, i file nascosti non verranno visualizzati. È possibile utilizzare flag e switches (bandiere e opzioni) per estendere il comportamento dei comandi.

Ad esempio per il comando ***`ls`*** è possibile usare il flag ***`-a`*** per vedere anche i file nascosti, comando completo: ***`ls -la`***. Per ogno comando è possibile vedere la lista dei possiibli flag e switches digitando ***`--help`***, ad sempio ***`ls -help`***. Inoltre è importante sapere che comando ***`man [comando]`***, ad esempio ***`man ls`***, è possibile visualizzare il manuale con tutte le informazioni che riguardano quel comando.

## 3 File System

Interagire con il File System significa in buona sostanza creare, spostare ed elimiare file e cartelle.
I comandi sono riassunti in questo schema:

***`touch`***	:	Crea file

***`mkdir`***	: Crea una folder

***`cp`***	:	Copia file o folder

***`mv`***	:	Sposta file o folder

***`rm`***	:	Cancella file o folder

***`file`***	:	Determine the type of a file

## Permessi
Un file o una cartella hanno delle caratteristiche che determinano sia quali azioni sono consentite sia quale utente o gruppo ha la possibilità di eseguire una determinata azione, come ad esempio:
- Leggere
- Scrivere
- Eseguire

Utilizzando il comando ***`ls -lh`*** è possibile vedere i file e le folder con i relativi permessi relative all'utente con il quale si esegue il comando.

Passare da un utente all'altro su un'installazione Linux è semplice grazie al comando ***`su`***. A meno che non siate l'utente root (o non utilizziate i permessi di root tramite sudo), è necessario conoscere due cose per facilitare questa transizione degli account utente:

- L'utente a cui vogliamo passare
- La password dell'utente

Il comando ***`su`*** accetta alcune opzioni che potrebbero interessarti. Ad esempio, l'esecuzione di un comando dopo aver effettuato il login o la specifica di una shell da utilizzare.  Ti consiglio di leggere la pagina man per susaperne di più. Tuttavia, parlerò dell'opzione ***`-l`***.

Semplicemente, fornendo l'opzione ***`-l`*** , avviamo una shell molto più simile all'utente effettivo che accede al sistema: ereditiamo molte più proprietà del nuovo utente, ad esempio variabili di ambiente e simili e ci sposta nella directory home dell'utente con cui ci siamo loggati.

## Directory Comuni

### /etc

Questa directory radice è una delle directory radice più importanti del sistema. La cartella etc (abbreviazione di eccetera) è una posizione comune in cui archiviare i file di sistema utilizzati dal sistema operativo. 

Ad esempio, il file sudoers contiene un elenco di utenti e gruppi che hanno l'autorizzazione a eseguire sudo o un set di comandi come utente root.

I file " passwd " e " shadow " che si trovano nella cartella /etc sono speciali per Linux, in quanto mostrano come il sistema memorizza le password di ciascun utente in un formato crittografato, denominato sha512.

### /var

La directory "/var", dove "var" è l'abbreviazione di "dati variabili", è una delle principali cartelle radice di un'installazione Linux . Questa cartella memorizza i dati a cui si accede o che vengono scritti di frequente da servizi o applicazioni in esecuzione sul sistema. Ad esempio, i file di log dei servizi e delle applicazioni in esecuzione vengono scritti qui ( /var/log ) o altri dati non necessariamente associati a un utente specifico (ad esempio, database e simili).

### /root

A differenza della directory /home , la cartella /root  è in realtà la directory home dell'utente di sistema "root". Questa cartella non ha altro significato se non quello di essere la directory home dell'utente "root". Tuttavia, vale la pena menzionarla, poiché si presume logicamente che questo utente abbia i propri dati in una directory come " /home/root " per impostazione predefinita.  

### /tmp

Si tratta di una directory radice univoca presente in un'installazione Linux . Abbreviazione di " temporanea ", la directory /tmp è volatile e viene utilizzata per archiviare dati a cui è necessario accedere solo una o due volte. Analogamente alla memoria del computer, una volta riavviato il computer, il contenuto di questa cartella viene cancellato.

È utile sapere che qualsiasi utente può scrivere in questa cartella per impostazione predefinita. Ciò significa che, una volta che abbiamo accesso a una macchina, questa diventa un ottimo posto per archiviare elementi.