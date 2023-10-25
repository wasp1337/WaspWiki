
###### stachan 24.03.2021

---

## config-register

`0x2142` Router verwirft Konfiguration bei Reload, gut für Password Recovery
`0x2102` Normalbetrieb

![](https://i.imgur.com/yg2sazc.png)

---

## squeeze

`squeeze flash` bereinigt Flash, löscht Crashinfos

---

## Images verwalten per TFTP

### Vorbereitung

```
show version
dir
show flash
```

* Am PC *tftpd64.exe* installieren (https://tftpd64.software.informer.com/download/?lang=de)
* Ordner für Images einstellen (*Browse*)

![](https://i.imgur.com/K7bn6gK.png)

* Router und PC direkt über ein LAN Kabel verbinden
* Ports statisch konfigurieren
* Korrektes Interface in Tftpd64 auswählen

### Image lokal sichern

`copy flash: tftp:`

![](https://i.imgur.com/McD3tUM.png)

Source filename = Name des Images
Remote Host = TFTP Server (der PC)
Destination filename bestätigen, soll den Namen behalten

### Image Upload

copy tftp: flash:

![](https://i.imgur.com/YK3bfXN.png)

---
