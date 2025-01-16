# Übersicht der wichtigsten Linux Befehle
Hier findet ihr eine Übersicht der wichtigsten Linux-Befehle.

## Datei- und Verzeichnisverwaltung
* `ls` – Listet Dateien und Verzeichnisse:
  * `ls -l` – Detaillierte Ansicht.
  * `ls -a` – Zeigt versteckte Dateien an.
* `cd` – Wechselt das Verzeichnis:
  * `cd /pfad/zum/verzeichnis` – Navigiere zu einem bestimmten Ordner.
  * `cd ..` – Gehe ein Verzeichnis nach oben.
* `pwd` – Zeigt das aktuelle Verzeichnis an.
* `mkdir` – Erstellt ein Verzeichnis:
  * `mkdir neuer_ordner`.
* `rm` – Löscht Dateien und Verzeichnisse:
  * `rm datei` – Löscht eine Datei.
  * `rm -r ordner` – Löscht einen Ordner rekursiv.
* `cp` – Kopiert Dateien oder Verzeichnisse:
  * `cp quelle ziel`.
  * `cp -r ordner1 ordner2`.
* `mv` – Verschiebt oder benennt Dateien um:
  * `mv` quelle ziel.
* `touch` – Erstellt eine leere Datei:
  * `touch datei.txt.`
* `find` – Sucht Dateien im Dateisystem:
  * `find / -name dateiname`.


## Textdateien und Inhalte
* `cat` – Zeigt den Inhalt einer Datei:
  * `cat datei.txt`.
* `less` – Zeigt den Inhalt einer Datei seitenweise:
  * `less datei.txt`.
* `head` – Zeigt die ersten Zeilen einer Datei:
  * `head -n 10 datei.txt`.
* `tail` – Zeigt die letzten Zeilen einer Datei:
  * `tail -n 10 datei.txt`.
  * `tail -f log.txt` – Zeigt Änderungen in Echtzeit.
* `grep` – Sucht Text in Dateien:
  * `grep "Suchbegriff" datei.txt`.
* `nano` – Einfache Textbearbeitung im Terminal.
* `vi` – NICHT einfache Textbearbeitung im Terminal. ;)


## Benutzer- und Berechtigungen
* `whoami` – Zeigt den aktuellen Benutzer an.
* `id` – Zeigt Benutzer- und Gruppen-IDs.
* `chmod` – Ändert Berechtigungen:
  * `chmod 755 datei`.
* `chown` – Ändert den Besitzer einer Datei:
  * `chown benutzer:gruppe datei`.
* `sudo` – Führt Befehle als Administrator aus.


## Netzwerk
* `ping` – Prüft die Verbindung zu einem Host:
  * `ping google.com`.
* `curl` – Holt Inhalte von einer URL:
  * `curl -O https://example.com/datei`.
* `wget` – Download von Dateien aus dem Internet:
  * `wget https://example.com/datei`.
* `ifconfig` – Zeigt Netzwerkinformationen (veraltet, ersetzt durch ip a).
* `ip` – Moderner Netzwerkbefehl:
  * `ip a` – Zeigt IP-Adressen.


## Prozesse verwalten
* `ps` – Zeigt laufende Prozesse:
  * `ps aux`.
* `kill` – Beendet Prozesse:
  * `kill -9 PID` (ersetze PID durch die Prozess-ID).
* `htop` – Interaktiver Prozess-Manager (falls installiert).

## Paketverwaltung
* `apt` (Debian/Ubuntu) nur mit root rechte oder sudo:
  * `apt update` – Aktualisiert die Paketliste.
  * `apt upgrade` – Aktualisiert installierte Pakete.
  * `apt install` paketname – Installiert ein Paket.
  * `apt remove` paketname – Entfernt ein Paket.

## Allgemeine Systeminformationen
* `uname -a` – Zeigt Kernel-Version und Systemarchitektur.
* `hostnamectl` – Zeigt Hostnamen und Kernel-Informationen.
* `lsb_release -a` – Informationen über die Linux-Distribution (z. B. Ubuntu, Debian).

## CPU-Informationen
* `lscpu` – Details zur CPU (Anzahl der Kerne, Architektur, Taktfrequenz).
* `cat /proc/cpuinfo` – Ausführliche Informationen zu den CPU-Kernen.
* `nproc` – Zeigt die Anzahl der verfügbaren CPU-Kerne.

## RAM (Arbeitsspeicher)
* `free -h` – Zeigt den aktuellen RAM- und Swap-Speicherverbrauch in einer human-lesbaren Form.
* `cat /proc/meminfo` – Detaillierte RAM-Statistiken.
* `vmstat` – Informationen über Speicher, CPU-Auslastung und mehr.

## Festplatten und Speicher
* `df -h` – Übersicht über die Dateisysteme und deren Speicherplatz.
* `lsblk` – Details zu den Blockgeräten (Partitionen und Datenträger).
* `du -sh /pfad/zum/verzeichnis` – Speicherplatzverbrauch eines Verzeichnisses.
* `iostat` – Festplatten- und CPU-Statistiken.

## Netzwerk
* `ip a` – Zeigt Netzwerkschnittstellen und IP-Adressen.
* `ss -tuln` – Zeigt offene Ports und Sockets.
* `ifconfig` (oder ip addr) – Informationen über Netzwerkadapter.
* `netstat` -anp – Verbindungen und Netzwerkschnittstellen.

## Systemauslastung und Performance
* `top` – Echtzeit-Übersicht über CPU- und RAM-Auslastung.
* `htop` – Erweiterte Version von top mit einer benutzerfreundlicheren Oberfläche.
* `uptime` – Zeigt die Systemlaufzeit und die durchschnittliche Auslastung (Load Average).

## Prozesse und Dienste
* `ps aux` – Zeigt alle laufenden Prozesse.
* `systemctl status dienstname` – Status eines bestimmten Dienstes.
* `service --status-all` – Übersicht aller Dienste.

## Hardware-Informationen
* `lshw` – Detaillierte Informationen zu Hardware (Root-Rechte erforderlich).
* `lsblk` – Details zu Datenträgern und Partitionen.
* `lspci` – Informationen über PCI-Geräte (z. B. Grafikkarte).
* `lsusb` – Informationen über USB-Geräte.

## Weitere nützliche Tools
* `glances` – Übersichtliches Monitoring-Tool (muss installiert werden).
* `iotop` – Überwachung der I/O-Operationen.
* `dstat` – Echtzeit-Statistiken zu CPU, RAM, Netzwerk und mehr.


