# netcat

## Semplice guida all'uso
  
Netcat è l'evoluzione di telnet. E' in grado di scrivere e leggere dati attraverso connessioni TCP e UDP.

### opzioni

1. -l listen (ascolto sulla porta)
2. -v verbose (mostra le informazioni)
3. -p imposta la porta
4. -e specifica il comando da eseguire dopo la connessione
5. -u utilizza UDP al posto di TCP
6. -z fa la scansione delle porte
7. -n evita la risoluzione dei nomi con DNS

#### Uso come telnet

`nc -v google.com 80`

Si connette al web server  e aspetta un comando, per avere la pagina web:

`GET index.html HTTP/1.1`

```bash
$ nc -v google.com 80
Connection to google.com 80 port [tcp/http] succeeded!
GET index.html HTTP/1.1

HTTP/1.1 302 Found
Location: http://www.google.com/
Cache-Control: private
Content-Type: text/html; charset=UTF-8
X-Content-Type-Options: nosniff
Date: Sat, 18 Aug 2012 06:03:04 GMT
Server: sffe
Content-Length: 219
X-XSS-Protection: 1; mode=block

<HTML><HEAD><meta http-equiv="content-type" content="text/html;charset=utf-8">
<TITLE>302 Moved</TITLE></HEAD><BODY>
<H1>302 Moved</H1>
The document has moved
<A HREF="http://www.google.com/">here</A>.
</BODY></HTML>
```

Per avere l'header

`HEAD / HTTP/1.0`

Gobuster rispetto ad altri (DirBuster e DIRB) essendo implementato in Go risulta essere più veloce.

#### Aprire un socket server

Apre un "canale" di comunicazione tra il server e il client.

Sul server:

`nc -l -p 1234`

Sul client:

`nc localhost`

In questo caso è una chat tra client e server

---

#### Traferimento file

Imposto il listener dove ricevere il file:

`nc -lvp 8080 >./file.txt`

Imposto per inviare il file:

`nc localhost 8080 < ./transfer.txt`

#### Remote shell

Dato l'opzione -e permette di eseguire comandi:

##### Su linux

`nc -v -l -p 7777 -e bin/bash

##### su windows

`nc -v -l -p 8888 -e cmd.exe

### Scansione delle porte

`nc -z -v localhost 1-1000`

`nc -z -v -n 127.0.0.1 1-1000`

#### Fonti

* [articolo 1](https://www.binarytides.com/netcat-tutorial-for-beginners/)

* [articolo 2](https://www.win.tue.nl/~aeb/linux/hh/netcat_tutorial.pdf)

* [articolo 3](https://www.hackingtutorials.org/networking/hacking-with-netcat-part-1-the-basics/)

* [Markdown-Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet#html) Guida per scrivere questo documento
