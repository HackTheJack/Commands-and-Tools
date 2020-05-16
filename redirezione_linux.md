# redirection linux

## Stream

In linux l'input e l'output è gestito con tre flussi:

* standard input (stdin) (0)
* standard output (stdout) (1)
* standard error (stderr) (2)

### Standard input

Se è presente un utente lo standard input fa riferimento all'input da tastiera, lo standard output e lo standard error sono visualizzati sullo schermo.

Per interrompere una richiesta di stdin si usa CTRL-d.

### Standard output

Viene stampato il testo sul terminale

`echo inviato allo standatd output`

### Standard error

Scrive sullo schermo gli errori generati da un programma

## Redirezione del flusso (stream redirection)

### Sovrascrive

`> -standard output`

`< -standard input`

`2> -standard error`

### Accoda

`>> -standard output`

`<< -standard input`

`2>> -standard error`

### /dev/null

è un file speciale per eliminare dati che gli vengono passati

`ls /dev/null`

### 2>&1 cosa significa

File descriptor 1 è lo standard output (stdout)

File descriptor 2 è lo standard error (stderr)

&1 indica che è un file descriptor, senza & sarebbe il file 1

2>&1 indica di ridirigere lo standard error sullo standard output

## Pipe

Viene utilizzato per ridirigere lo stream di un programma verso un altro.
Quando lo standard output di un programma è mandato ad un altro attraverso il pipe viene visualizzato sullo schermo solo il risultato del secondo programma.

Esempio:

`ls | less`

la lista viene visualizza una riga alla volta.

## Filtri

* grep ritorna il testo che corrisponde alla stringa passata a grep

* wc conta caratteri, righe e parole

* tee ridirige lo standard input sia allo standard out che a uno più file

`wc /etc/magic | tee magic_count.txt`

### Fonti

* [Markdown-Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet#html) Guida per scrtivere questo documento

* [stackoverflow](https://stackoverflow.com/questions/818255/in-the-shell-what-does-21-mean)

* [Digital_Ocean](https://www.digitalocean.com/community/tutorials/an-introduction-to-linux-i-o-redirection)
