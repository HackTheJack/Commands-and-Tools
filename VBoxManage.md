# VirtualBox - VBoxManage

## Semplice guida all'uso
  
Alcuni comandi utili per visualizzare i parametri delle vms

---

#### Uso:

Utilizzare l'utente che ha lanciato virtualbox:

#### Avviare una macchina da console

`VBoxManage startvm kali_64`

```bash
Waiting for VM "kali_64" to power on...
VM "kali_64" has been successfully started.
```

#### Vedere le macchine

`VBoxManage list vms`

```bash
VBoxManage list vms
"kali_64" {e6ae5b4a-e6c5-4a36-be24-f9ce32efd953}
"Rickdiculously Easy" {8df6704d-0723-48d6-89f3-09dff432cb33}
```

---

#### Specifiche di una macchina

`VBoxManage showvminfo kali_64`

```bash
VBoxManage showvminfo kali_64
Name:                        kali_64
Groups:                      /
Guest OS:                    Debian (64-bit)
UUID:                        e6ae5b4a-e6c5-4a36-be24-f9ce32efd953
Config file:                 /home/antonio/VirtualBox VMs/kali_64/kali_64.vbox
Snapshot folder:             /home/antonio/VirtualBox VMs/kali_64/Snapshots
Log folder:                  /home/antonio/VirtualBox VMs/kali_64/Logs
Hardware UUID:               e6ae5b4a-e6c5-4a36-be24-f9ce32efd953
Memory size                  1024MB
Page Fusion:                 disabled
....
```

#### Visualizzare i dhcp server

`VBoxManage list dhcpservers`

```bash
VBoxManage list dhcpservers
NetworkName:    HostInterfaceNetworking-vboxnet0
Dhcpd IP:       192.168.56.100
LowerIPAddress: 192.168.56.101
UpperIPAddress: 192.168.56.254
NetworkMask:    255.255.255.0
Enabled:        Yes
Global Configuration:
    minLeaseTime:     default
    defaultLeaseTime: default
    maxLeaseTime:     default
    Forced options:   None
    Suppressed opts.: None
        1/legacy: 255.255.255.0
Groups:               None
Individual Configs:   None

```

#### Aggiungere dhcp server

`VBoxManage dhcpserver add --netname labTest --ip 10.10.0.1 --netmask 255.255.255.0 --lowerip 10.10.0.2 --upperip 10.10.0.12 --enable`

Attenzione: il dhcpserver è dell'utente che lo lancia, per utilizzarlo la macchina virtualbox deve essere lanciata dallo stesso utente.

---

#### Rimuovere dhcp server

`VBoxManage dhcpserver remove --network=labTest`

---

#### Macchine in funzione

`VBoxManage list runningvms`

```bash
VBoxManage list runningvms
"kali_64" {e6ae5b4a-e6c5-4a36-be24-f9ce32efd953}
"Rickdiculously Easy" {8df6704d-0723-48d6-89f3-09dff432cb33}
```

---

#### Lease del dhcp

`VBoxManage dhcpserver findlease --network=labTest --mac-address=08002725C90C`

Il MAC può essere ricavato con il comando `VBoxManage showvminfo kali_64`

```bash
antonio@kali:/$ VBoxManage dhcpserver findlease --network=labTest --mac-address=08002725C90C
IP Address:  10.10.0.3
MAC Address: 08:00:27:25:c9:0c
State:       acked
Issued:      2020-05-09T22:15:30Z (1589062530)
Expire:      2020-05-09T22:25:30Z (1589063130)
TTL:         600 sec, currently 512 sec left
```

#### Fonti

* `VBoxManage -h`
