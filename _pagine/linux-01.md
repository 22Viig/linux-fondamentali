---
layout: page
title: I fondamentali di Linux - Part. 1
args: (primi comandi, argomenti, File System, comandi utili, operatori)
permalink: /linux-01/

---

- [1. I primi comandi](#1-i-primi-comandi)
- [2. Argomenti](#2-argomenti)
- [3. File System](#3-file-system)
- [4. Comandi utili](#4-comandi-utili)
- [5. Operatori](#5-operatori)


## 1 I primi comandi

Il comando ***`pwd`*** (pwd sigla sta per print working directory) ci mostra il percorso della cartella nella quale ci troviamo.

Per spostarci tra le cartelle possiamo usare il comando ***`cd [DIRECTORY]`*** (cd sigla per change directory).

Per visualizzare i contenuti di una cartella (altre cartelle o file) usiamo il comando ***`ls`***.

É importante sapere che il comando ***`man [comando]`***, ad esempio ***`man ls`***, è possibile visualizzare il manuale con tutte le informazioni che riguardano quel comando.

## 2 Argomenti

La maggior parte dei comandi consente di specificare argomenti. Questi argomenti sono identificati da un trattino e da una parola chiave specifica, nota come flag o switch.

Più avanti discuteremo come possiamo identificare quali comandi consentono di fornire argomenti e capiremo esattamente a cosa servono.

Ad esempio per il comando ***`ls`*** è possibile usare il flag ***`-a`*** per vedere anche i file nascosti, comando completo: ***`ls -a`***. Per ogno comando è possibile vedere la lista dei possiibli flag e switches digitando ***`--help`***, ad sempio ***`ls -help`***. 

## 3 File System

Interagire con il File System significa in buona sostanza creare, spostare ed elimiare file e cartelle.
I comandi sono riassunti in questo schema:

***`touch`***	:	Crea file

***`mkdir`***	: Crea una folder

***`cp`***	:	Copia file o folder

***`mv`***	:	Sposta file o folder

***`rm`***	:	Cancella file o folder

***`file`***	:	Determine the type of a file

Possiamo invece usare il comando ***`find`*** per ricercare dei file o cartelle.

## 4 Comandi utili

Uno dei primi comandi che tipicamente si impara è  ***`echo`***, è un comando che serve a  "riecheggiare" una singola frase, non abbiamo bisogno di usare le virgolette doppie, ad esempio  ***`echo Ciao`*** ci mostrarà a terminale:  ***`Ciao`***. Tuttavia, la stringa deve essere racchiusa tra virgolette doppie se sono presenti uno o più spazi, ad esempio ***`echo "Ciao amico!"`*** mostrerà la frase Ciao amico nel terminale. Non è intuitivo capire l'utilizzo di questo comando, sarà più chiaro più avanti.

Il comando ***`grep`*** ci permette di cercare nel contenuto dei file i valori specifici che stiamo cercando.

Il comando ***`wc`*** conta le parole, le linee ed i caratteri di un file.

## 5 Operatori
Gli operatori Linux sono un modo fantastico per approfondire le tue conoscenze su Linux . Ci sono alcuni operatori importanti che vale la pena menzionare. Ne analizzeremo le basi e li suddivideremo in sezioni più piccole.

In sintesi, presenterò i seguenti operatori:

***`&`***: Questo operatore consente di eseguire comandi in background sul terminale.
***`&&`***:	Questo operatore consente di combinare più comandi insieme in un'unica riga del terminale.
***`>`***: Questo operatore è un redirector, ovvero possiamo prendere l'output di un comando (ad esempio usando cat per generare un file) e indirizzarlo altrove.
***`>>`***: Questo operatore svolge la stessa funzione dell'operatore >ma aggiunge l'output anziché sostituirlo (il che significa che non viene sovrascritto nulla).

