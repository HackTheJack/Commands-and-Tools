# Scansione porte

Il tool più utilizzato è nmap con le seguenti opzioni:

* -sU: UDP Scan

* TIMING: -T<0-5>: Set timing template (higher is faster)

* -A: Enable OS detection, version detection, script scanning, and traceroute

* -sS scansione di tipo TCP SYN

* -v: Increase verbosity level (use -vv or more for greater effect)

* -sV: Probe open ports to determine service/version info

* -O: Enable OS detection

* -p port ranges Only scan specified ports

* -Pn: Treat all hosts as online -- skip host discovery

* --min-rate \<number\>: Send packets no slower than \<number\> per second

* -sn: Ping Scan - disable port scan

## Differenti approcci
  
### nmap 192.168.2.2

This option scans all reserved TCP ports on the machine

### nmap -sS -sU -T4 -A -v 192.168.2.2

### nmap -O -sV 192.168.2.2

### nmap -Pn -p- -sV 10.0.1.9

## In due fasi

* ports = $(nmap -p- --min-rate=1000 -T4 10.10.10.27 | grep ^[0-9] | cut -d '/' -f 1 | tr '\n' ',' | sed s/,$//)

* nmap -sC -sV -p$ports 10.10.10

Suddividiamo in varie fasi:

1. nmap -p- --min-rate=1000 -T4 10.10.10.27

```bash
nmap -p- --min-rate=1000 -T4 10.10.0.2
Starting Nmap 7.80 ( https://nmap.org ) at 2020-05-19 21:59 CEST
Nmap scan report for 10.10.0.2
Host is up (0.00036s latency).
Not shown: 65528 closed ports
PORT      STATE SERVICE
21/tcp    open  ftp
22/tcp    open  ssh
80/tcp    open  http
9090/tcp  open  zeus-admin
13337/tcp open  unknown
22222/tcp open  easyengine
60000/tcp open  unknown
MAC Address: 08:00:27:BF:52:95 (Oracle VirtualBox virtual NIC)

Nmap done: 1 IP address (1 host up) scanned in 10.45 seconds
```

2. nmap -p- --min-rate=1000 -T4 10.10.0.2 | grep ^[0-9]

grep seleziona le righe che cominciano con numeri

```bash
nmap -p- --min-rate=1000 -T4 10.10.0.2 | grep ^[0-9] 
21/tcp    open  ftp
22/tcp    open  ssh
80/tcp    open  http
9090/tcp  open  zeus-admin
13337/tcp open  unknown
22222/tcp open  easyengine
60000/tcp open  unknown
```

3. nmap -p- --min-rate=1000 -T4 10.10.0.2 | grep ^[0-9] || cut -d '/' -f 1 |

cut taglia la stinga dove trova '/' e -f recupera il primo pezzo

```bash
21
22
80
9090
13337
22222
60000
```

4. nmap -p- --min-rate=1000 -T4 10.10.0.2 | grep ^[0-9] | cut -d '/' -f 1 | tr '\n' ','

tr sostituisce il ritorno a capo con la ','





#### Fonti

* [Markdown-Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet#html) Guida per scrtivere questo documento
