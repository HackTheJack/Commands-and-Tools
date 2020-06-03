# Redirezione su Linux/Unix

## Streams

In un sistema Linux/Unix _input_ e _output_ sono gestiti con tre flussi:

* _standard input_ (`stdin`) (0)

Lo __standard input__ è lo stream da cui un programma legge i dati di input

* _standard output_ (`stdout`) (1)

Lo __standard output__ è lo stream su cui un programma scrive i dati in output

* _standard error_ (`stderr`) (2)

Lo __standard error__ è lo stream su cui un programma scrive i messaggi di errore o diagnostica


## Redirezione del flusso (_stream redirection_)

### Sovrascrivere

`>` _standard output_

`<` _standard input_

`2>` _standard error_

### Accodare

`>>` _standard output_

`<<` _standard input_

`2>>` _standard error_


### Redirezione dello _stderr_ su _stdout_

`&` rappresenta il _file descriptor_ associato ad un comando o ad un file.

Una delle possibilità permesse è la redirezione di uno stream in un altro. In particolare vediamo come redirigere lo _standard error_ su quello di _output_ in modo da essere processati insieme.

Mettiamo di voler cercare il file _profile.conf_.

`find / -name profile.conf > results 2>&1`

In questo caso abbiamo scritto il risultato del comando `find` in un file _results_, reindirizzando sia lo `stdin` e lo `stdout` nel file.

Senza la redirezione, lo `stderr` sarebbe stato visualizzato sullo schermo.

## Pipe

Viene utilizzato per ridirigere lo _stream_ di un programma verso un altro.
Quando lo _standard output_ di un programma è mandato ad un altro attraverso il pipe viene visualizzato sullo schermo solo il risultato del secondo programma.

Esempio:

`ls | less`

L'output di `ls` diventa l'input del comando `less`. In questo modo l'output finale è quello di `less`

## Filtri (TODO improve)

* `grep` ritorna il testo che corrisponde alla stringa passata a grep

* `wc` conta caratteri, righe e parole

* `tee` ridirige lo standard input sia allo standard out che a uno più file

`wc /etc/magic | tee magic_count.txt`

### Fonti

* [Markdown-Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet#html) Guida per scrtivere questo documento

* [stackoverflow](https://stackoverflow.com/questions/818255/in-the-shell-what-does-21-mean)

* [Digital_Ocean](https://www.digitalocean.com/community/tutorials/an-introduction-to-linux-i-o-redirection)
