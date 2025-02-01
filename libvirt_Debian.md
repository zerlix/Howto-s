# 1. Einführung in Libvirt

**Libvirt** ist eine Open-Source-Bibliothek und ein Toolset zur Verwaltung von virtuellen Maschinen und Ressourcen wie Speicher und Netzwerken. Es bietet eine einheitliche Schnittstelle für verschiedene Virtualisierungslösungen auf Linux und erleichtert die Automatisierung von Virtualisierungsaufgaben. Ideal für Admins und Entwickler, die VMs effizient verwalten wollen.

### Warum Libvirt ?

* Unterstützt verschiedene Virtualisierungstechnologien wie KVM, QEMU und Xen.
* Einheitliche API für verschiedene Virtualisierungstools.
* Ermöglicht einfache Verwaltung von VMs, Netzwerken und Speicher per CLI oder GUI.
* Weit verbreitet, mit aktiver Community und regelmäßigen Updates.

# 2. Installation von Libvirt

Öffne ein Terminal und installiere Libvirt mit:

```bash
apt update
apt install libvirt-daemon-system libvirt-clients qemu-kvm
```

Nach der Installation startet der Libvirt-Dienst normalerweise automatisch. Du kannst das mit folgendem Befehl prüfen:<br/>
`systemctl status libvirtd`

Falls der Dienst nicht läuft, kannst du ihn starten mit:<br/>
`systemctl start libvirtd`

# 3. Konfiguration von Libvirt

**Konfigurationsdateien verstehen**:<br/>
Libvirt verwendet verschiedene Konfigurationsdateien, um seine Einstellungen zu speichern. Die wichtigsten Dateien sind:
* **/etc/libvirt/libvirtd.conf:**<br/>
Diese Datei enthält die allgemeinen Konfigurationseinstellungen für den Libvirt-Daemon.
* **/etc/libvirt/qemu.conf:**<br/> Hier werden spezifische Einstellungen für die QEMU-Hypervisor-Backend-Konfiguration gespeichert.
* **/etc/libvirt/qemu/*.xml:**<br/> Diese XML-Dateien enthalten die Konfigurationen für jede virtuelle Maschine.

**Netzwerkkonfiguration:**<br/> 
Libvirt bietet verschiedene Netzwerkoptionen für virtuelle Maschinen, einschließlich NAT, Bridged Networking und Host-Only Networking. Die Konfiguration erfolgt normalerweise über das Tool virsh oder die grafische Benutzeroberfläche virt-manager.

**Konfiguration von Libvirt für die Bridge:**<br/>
1. Öffne eine Terminal-Sitzung auf deinem Linux-System.

2. Erstelle eine XML-Datei für die Netzwerkkonfiguration. 
   Du kannst dafür einen Texteditor deiner Wahl verwenden. Zum Beispiel:<br/> `nano /etc/libvirt/qemu/networks/bridge.xml`
3. Füge den folgenden Inhalt in die Datei ein:<br/>
    ```xml
    <network>
      <name>br0</name>
      <forward mode="bridge"/>
      <bridge name="br0"/>
    </network>
    ```
4. Speichere die Datei und schließe den Texteditor.
5. Definiere das Netzwerk mit dem Befehl. <br/>
    `virsh net-define /etc/libvirt/qemu/networks/bridge.xml`
6. Aktiviere das Netzwerk automatisch beim Systemstart<br/>
    `virsh net-autostart br0`
7. Starte das Netzwerk<br/>
    `virsh net-start br0`
8. Überprüfen, ob das Libvirt-Netzwerk korrekt definiert und gestartet ist:
    `virsh net-list --all`

Damit ist die Bridge erfolgreich für die Verwendung durch Libvirt konfiguriert. Du kannst nun virtuelle Maschinen erstellen und sie so konfigurieren, dass sie das br0-Netzwerk verwenden.

# 4. Verwaltung von virtuellen Maschinen mit Libvirt