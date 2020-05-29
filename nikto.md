![Nikto](https://www.ceos3c.com/wp-content/uploads/2019/11/word-image.jpeg)


## Guida all'uso

**Nikto** è uno scanner per la ricerca di vulnerabilità in un **server Web**.

In questa guida vediamo i principali comandi utilizzati.
Per una guida completa, si suggerisce la lettura della [documentazione ufficiale](https://cirt.net/nikto2-docs/)

---

### Scansione normale

Per fare una scansione di un host sulla porta 80 basta lanciare il comando

`nikto -h <indizzo-IP>`

Esempio:

```bash
nikto -h 10.10.10.111
- Nikto v2.1.6
===========================================================================
+ Target IP:          10.10.10.111
+ Target Hostname:    10.10.10.111
+ Target Port:        80
+ Start Time:         2020-05-11 17:39:31 (GMT2)
===========================================================================
+ Server: Apache/2.4.29 (Ubuntu)
+ The anti-clickjacking X-Frame-Options header is not present.
+ The X-XSS-Protection header is not defined. This header can hint to the user agent to protect against some forms of XSS
+ The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type
+ No CGI Directories found (use '-C all' to force check all possible dirs)
+ Apache/2.4.29 appears to be outdated (current is at least Apache/2.4.37). Apache 2.2.34 is the EOL for the 2.x branch.
+ IP address found in the 'location' header. The IP is "127.0.1.1".
+ OSVDB-630: The web server may reveal its internal or real IP in the Location header via a request to /images over HTTP/1.0. The value is "127.0.1.1".
+ Web Server returns a valid response with junk HTTP methods, this may cause false positives.
+ OSVDB-10944: : CGI Directory found
+ OSVDB-10944: /cdn-cgi/login/: CGI Directory found
+ OSVDB-3233: /icons/README: Apache default file found.
+ 10293 requests: 0 error(s) and 10 item(s) reported on remote host
+ End Time:           2020-05-11 18:15:12 (GMT2) (2141 seconds)
===========================================================================
+ 1 host(s) tested
```

---

### Scansione su più porte

Nel caso si vogliano analizzare altre porte si deve usare il flag `-p`

`nikto -h <indizzo-IP> -p [port 1], [port 2], [port 3]`


---

### Tuning

L'opzione Tuning permette di ridurre e specificare i test che si vogliono effettuare

`nikto -T [option(s)] -h <indizzo-IP>`

E' possibile negare le opzioni utilizzando il comando `x` seguito dal numero del test che non si vuole effettuare

`nikto -T -x[option(s)] -h <indizzo-IP>`

Valide opzioni sono:

| Parametro   |      Risultato      |
|----------|:-------------|
|1   |  Interesting File / Seen in logs|
|2   |  Misconfiguration / Default File|
|3   |  Information Disclosure / File utili ad un attacco|
|4   |  Injection (XSS/Script/HTML)|
|5   |  Remote File Retrieval – All’interno di file root|
|6   |  Denial of Service|
|7   |  Remote File Retrieval – Server Wide|
|8   |  Command Execution / Remote Shell|
|9   |  SQL Injection|
|0   |  File Upload|
|a   |  Escludere l’autenticazione|
|b   |  Software Identification|
|c   |  Remote Source Inclusion|
|d   |  WebService|
|e   |  Administrative Console|
|x   |  Inverte l’opzione Tuning (-t) ossia tutte le tipologie di scansioni tranne quella indicata dopo x|


Esempio:

Eseguire _solo_ un Denial of Service test:
`nikto -T 6 -h https://www.dominio.xyz`
Eseguire tutti i test _tranne_ Denial of Service:
`nikto -T x 6 -h https://www.dominio.xyz`


---

### Scansione su più host utilizzando un file testuale

Se si vuole scansionare più host, è possibile utilizzare un file contenete la lista di tali host

`nikto -h lista_host.txt`

dove `lista_host.txt` può avere il seguente formato:

```
192.168.0.1:443
http://192.168.0.1:8080/
192.168.0.3
```

NOTA: se nessuna porta è specificata, si assume che essa sia la `80`.


---

### Utilizzare un Proxy

Se la macchina su cui si lancia Nikto può accedere alla macchina da attaccare solo tramite Proxy, possiamo effettuare il test utilizzando l'opzione `-useproxy`

Esempio:

`nikto -h localhost -useproxy http://localhost:8080/`


#### Fonti
* [Documentazione ufficiale](https://cirt.net/nikto2-docs/)
* [Nikto](https://www.manuscavelli.it/nikto/)
* [Github](https://github.com/sullo/nikto)
