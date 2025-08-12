---
layout: page
title: I fondamentali di Linux - Prima di iniziare
args: (Il terminale, la Shell)
permalink: /linux-00-init/

---

- [1. Il terminale](#1-il-terminale)
- [2. Argomenti](#2-la-shell)


## 1 Il terminale

Il terminale è un'interfaccia testuale che permette agli utenti di interagire direttamente con il sistema operativo ed i programmi installati. Invece di cliccare su icone e menu (come in Windows o macOS), nel terminale si scrivono comandi.

Le principali funzioni del terminale sono:

- ***Eseguire comandi o programmi***: come aprire file, spostare cartelle, installare/eseguire programmi.
- ***Automatizzare operazioni***: tramite script.
- ***Controllare il sistema***: monitorare processi, gestire utenti, configurare reti.
- ***Accedere da remoto***: ad altri computer via SSH.



## 2 La SHELL

La shell è il programma che interpreta i comandi scritti nel terminale. È il "cervello" dietro il terminale.

Le principali funzioni del terminale sono:

- ***Interpretare comandi***: traduce ciò che scrivi in azioni per il sistema.
- ***Gestire variabili e script***: puoi scrivere script per automatizzare compiti.
- ***Personalizzare l’ambiente***: prompt, alias, funzioni.

Esistono diversi tipi di Shell pre-installati nelle distribuzioni Linux. Per vedere quali Shell sono presenti è possibile usare il comando ***`echo $SHELL`*** oppure ***`cat /etc/shells`***

Esempi di SCHELL:

- /bin/sh
- /bin/bash
- /usr/bin/bash
- /bin/rbash
- /usr/bin/rbash
- /bin/dash
- /usr/bin/dash
- /usr/bin/tmux
- /usr/bin/screen
- /bin/zsh
- /usr/bin/zsh

È possibile scegliere quale Shell utillizare specificando il nome della Shell nel terminale, ad esempio ***`zsh`*** per impostare la Shell zsh nel terminale.

Se vuoi cambiare in modo permanente la tua shell predefinita, puoi usare il comando: ***`chsh -s /usr/bin/zsh`***

### BASH - Bourne Again Shell

Bash è una shell ampiamente utilizzata con funzionalità di scripting.
Offre una funzione di completamento tramite Tab, il che significa che se stai completando un comando, puoi premere il tasto Tab sulla tastiera. Il comando verrà completato automaticamente in base a una possibile corrispondenza o ti verranno forniti più suggerimenti per completarlo.
Bash conserva un file cronologico e registra tutti i comandi. Puoi usare i tasti freccia su e giù per usare i comandi precedenti senza doverli digitare di nuovo. Puoi anche digitare ***`history`*** per visualizzare tutti i comandi precedenti.

### Friendly Interactive Shell

Anche la Friendly Interactive Shell (Fish) non è predefinita nella maggior parte delle distribuzioni Linux . Come suggerisce il nome, si concentra maggiormente sulla facilità d'uso rispetto ad altre shell. Alcune delle funzionalità principali di Fish sono elencate di seguito:

Offre una sintassi molto semplice, adatta anche agli utenti principianti.
A differenza di bash, ha la correzione ortografica automatica per i comandi che scrivi.
È possibile personalizzare il prompt dei comandi con alcuni temi interessanti utilizzando fish.
La funzione di evidenziazione della sintassi di Fish colora le diverse parti di un comando in base al loro ruolo, migliorandone la leggibilità. Inoltre, ci aiuta a individuare gli errori grazie ai colori distintivi.
Fish fornisce anche funzionalità di scripting, completamento tramite tabulazione e cronologia dei comandi, come le shell menzionate in questa attività.
Guscio Z

### Z Shell (ZSH)

ZSH non è installata di default nella maggior parte delle distribuzioni Linux . È considerata una shell moderna che combina le funzionalità di alcune shell precedenti. Di seguito sono elencate alcune delle funzionalità principali di zsh:

Zsh fornisce il completamento avanzato tramite tabulazione ed è anche in grado di scrivere script.
Proprio come i pesci, fornisce anche la correzione ortografica automatica per i comandi.
Offre un'ampia personalizzazione che potrebbe renderlo più lento rispetto ad altre shell.
Offre inoltre il completamento tramite tabulazione, la funzionalità di cronologia dei comandi e numerose altre funzionalità.


La scelta della shell Linux migliore dipende dall'utilizzo che se ne fa e dalle sue caratteristiche. Le shell illustrate in questa sezione sono solo alcune delle numerose shell disponibili in Linux . È possibile confrontare le caratteristiche di queste diverse shell e scegliere quella più adatta alle proprie esigenze.




