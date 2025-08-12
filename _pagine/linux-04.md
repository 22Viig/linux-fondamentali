---
layout: page
title: I fondamentali di Linux - Part. 4
args: (scripting)
permalink: /linux-04/

---
- [1. Scripting](#1-scripting)

## 1 Scripting

Uno script di shell non è altro che un insieme di comandi.  Gli scripting ci aiutano ad automatizzare le attività. Prima di imparare a scrivere uno script, dobbiamo sapere che, sebbene le shell Linux abbiano funzionalità di scripting, ciò non significa che sia possibile creare uno script solo utilizzando una shell. Lo scripting può essere eseguito anche in vari linguaggi di programmazione.

Il primo passo è aprire il terminale e selezionare una shell. Proviamo con la shell bash, quella predefinita e ampiamente utilizzata nella maggior parte delle distribuzioni.

A differenza degli altri comandi che digitiamo nella shell, dobbiamo prima creare un file utilizzando un qualsiasi editor di testo per lo script. Il file deve avere estensione .sh, l'estensione predefinita per gli script bash. 

Ogni script dovrebbe iniziare da shebang. Shebang è una combinazione di alcuni caratteri aggiunti all'inizio di uno script, iniziando con #!seguito dal nome dell'interprete da utilizzare durante l'esecuzione dello script. Dato che stiamo scrivendo il nostro script in bash, definiamolo come interprete nello shebang. 

La priam riga del nostro script sarà quindi: ***`!#/bin/bash`***.

## Variabili


Una variabile memorizza un valore al suo interno. Supponiamo di dover utilizzare più volte nel tuo script valori complessi, come un URL, un percorso di file, ecc. Invece di memorizzarli e scriverli ripetutamente, puoi memorizzarli in una variabile e utilizzare il nome della variabile ogni volta che ne hai bisogno.

Lo script seguente visualizza una stringa sullo schermo: "Ehi, come ti chiami?". Questo avviene tramite il comando ***`echo`***. La seconda riga dello script contiene il codice ***`read name`***. ***`read`*** viene utilizzato per ricevere input dall'utente ed ***`name`*** la variabile in cui l'input verrà memorizzato. L'ultima riga viene utilizzata ***`echo`*** per visualizzare la riga di benvenuto per l'utente, insieme al suo nome memorizzato nella variabile ***`$name`***.

```
# Defining the Interpreter 
#!/bin/bash
echo "Hey, what’s your name?"
read name
echo "Welcome, $name"
```

Per eseguire lo script, dobbiamo prima assicurarci che abbia i permessi di esecuzione. Per concedere questi permessi allo script, possiamo digitare il seguente comando nel nostro terminale:

***`chmod +x first_script.sh`***

Ora che lo script ha i permessi di esecuzione, usa ***`./`*** "prima del nome dello script" per eseguirlo. Usiamo ***`./`***  prima dello script per eseguirlo anziché digitare direttamente il nome dello script, perché ***`./`***  indica alla shell di eseguire il file presente nella directory corrente. Se non si specifica ***`./`***  prima del nome dello script, la shell cercherà lo script nella variabile d'ambiente PATH (che contiene tutte le directory tranne quella corrente) e non troverà lo script definito in nessuna di queste directory, generando un errore. Il terminale seguente mostra lo script in cui abbiamo utilizzato le variabili:

## Loop

Un ciclo, come suggerisce il nome, è qualcosa che si ripete. 

Ecco un esempio:

```
# Defining the Interpreter 
#!/bin/bash
for i in {1..10};
do
echo $i
done
```

La prima riga contiene la variabile ***`i`*** che itererà da 1 a 10 ed eseguirà il codice seguente ogni volta. ***`do`*** indica l'inizio del codice del ciclo e ***`done`*** indica la fine. Tra di essi, deve essere scritto il codice che vogliamo eseguire nel ciclo. Il ciclo ***`for`*** prenderà ogni numero tra parentesi e lo assegnerà alla variabile ***`i`*** a ogni iterazione. Il ciclo ***`echo i`*** visualizzerà il valore di questa variabile a ogni iterazione.

## Istruzioni condizionali

Le istruzioni aiutano a eseguire un codice specifico solo quando una condizione è soddisfatta; in caso contrario, è possibile eseguire un altro codice. 

Ecco un esempio:

```
# Defining the Interpreter 
#!/bin/bash
echo "Please enter your name first:"
read name
if [ "$name" = "Riccardo" ]; then
        echo "Ciao $name! Sei autorizzato ad entrare."
else
        echo "Mi spiace $name, non sei autorizzato ad entrare."
fi
```

Lo script sopra riportato accetta il nome dell'utente come input e lo memorizza in una variabile (approfondita nella sezione Variabili). L'istruzione condizionale inizia con if e confronta il valore di quella variabile con la stringa Stewart; se corrisponde, mostrerà il segreto all'utente, altrimenti no. Il carattere fi viene utilizzato per terminare la condizione.

## Commenti
Un commento è una frase che scriviamo nel nostro codice solo per motivi di comprensione. Si scrive con un simbolo # seguito da uno spazio e dalla frase che dovete scrivere. 

```
# Defining the Interpreter 
#!/bin/bash
# Chiedo all'utente di inserire il nome
echo "Inserisci il tuo nome:"

#Leggo il nome
read name

#Verifico se il nome è uguale a "Riccardo" scrivo che è autorizzato ad entrare
if [ "$name" = "Riccardo" ]; then
        echo "Ciao $name! Sei autorizzato ad entrare."

#Altrimenti scivo che non è autorizzato
else
        echo "Mi spiace $name, non sei autorizzato ad entrare."
fi
```

