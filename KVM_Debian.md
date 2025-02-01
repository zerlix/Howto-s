# Installation von KVM unter Debian 12 "Bookworm"
In diesem Tutorial zeige ich dir, wie du KVM unter Debian 12 installierst. KVM (Kernel-based Virtual Machine) ist eine Virtualisierungslösung für Linux, mit der du mehrere virtuelle Maschinen auf einem einzigen Rechner laufen lassen kannst. Das Ganze nutzt die Virtualisierungserweiterungen von Intel (VT-x) oder AMD (AMD-V), um eine schnelle und effiziente Umgebung bereitzustellen.

Mit KVM kannst du verschiedene Betriebssysteme und Anwendungen sauber voneinander getrennt in virtuellen Maschinen ausführen. Das bringt mehr Flexibilität, bessere Ressourcennutzung und macht dein Setup insgesamt skalierbarer. Lass uns direkt loslegen! 🚀

# Systemvoraussetzungen
Dieses Howto setzt voraus, dass du Debian 12 (Bookworm) mit einer minimalen Installation ohne grafische Oberfläche verwendest.

Bevor du KVM installierst, solltest du sicherstellen, dass dein Prozessor die nötigen Virtualisierungserweiterungen unterstützt. KVM läuft nur auf Intel- oder AMD-Prozessoren, die VT-x (bei Intel) oder AMD-V (bei AMD) bieten.

Um das zu überprüfen, kannst du folgendes Shell-Skript ausführen. Es sucht nach den passenden CPU-Flags (vmx für Intel, svm für AMD). Falls diese vorhanden sind, bedeutet das, dass dein Prozessor die Hardware-Virtualisierung unterstützt. Zusätzlich prüft das Skript, ob die notwendigen Kernelmodule für KVM bereits geladen sind.


```bash
#!/bin/bash

# Überprüfen, ob die CPU die Virtualisierung unterstützt
if grep -E "(vmx|svm)" /proc/cpuinfo > /dev/null; then
    echo "Die CPU unterstützt KVM."
else
    echo "Die CPU unterstützt kein KVM."
    exit 1
fi

# Überprüfen, ob die KVM-Module geladen sind
if lsmod | grep kvm > /dev/null; then
    echo "Die KVM-Module sind geladen."
else
    echo "Die KVM-Module sind nicht geladen. Bitte stellen Sie sicher, dass Sie das richtige Kernelmodul 
          für Ihre CPU und Virtualisierungsumgebung installiert haben und versuchen Sie es erneut."
    exit 1
fi

exit 0
```

Speicher das Skript in einer Datei mit der Endung .sh, zum Beispiel `cpu_kvm_check.sh`. Anschließend kannst du es ausführen, um zu checken, ob deine CPU KVM unterstützt.

Neben den CPU-Flags braucht die KVM-Installation auf Debian 12 auch das Laden von Kernelmodulen. Dazu gehört das Modul `kvm.ko`, das die Kernvirtualisierungsinfrastruktur bereitstellt, sowie ein prozessorspezifisches Modul wie `kvm-intel.ko` (bei Intel) oder `kvm-amd.ko` (bei AMD). Diese Module müssen verfügbar und geladen werden, damit du KVM nutzen kannst. Achte darauf, dass deine Linux-Kernelkonfiguration diese Module enthält und sie problemlos geladen werden können.

Wichtig: Die Virtualisierungsfunktionen müssen auch im BIOS/UEFI aktiviert sein. Falls die CPU-Flags fehlen oder die Virtualisierung im BIOS/UEFI deaktiviert ist, lässt sich KVM leider nicht verwenden.

# Konfiguration einer Netzwerkbrücke (Bridge)
Eine Netzwerkbrücke ermöglicht es virtuellen Maschinen, direkt mit dem physischen Netzwerk zu kommunizieren, als wären sie eigenständige Maschinen. Das ist besonders praktisch, wenn du möchtest, dass deine virtuellen Maschinen von anderen Geräten im Netzwerk erreicht werden können oder wenn du bestimmte Netzwerkdienste darauf bereitstellen willst.

Um eine Netzwerkbrücke unter Debian einzurichten, geh einfach wie folgt vor:
1. Ermittle deine physische Schnittstelle:<br/>
    Benutze den Befehl `ip -f inet a s`, um deine physische Schnittstelle zu finden. Diese könnte zum Beispiel `enp4s0 `oder `eth0 `heißen.
2. Installiere bridge-utils:<br/>
    Stell sicher, dass das Paket bridge-utils installiert ist, da du es zur Verwaltung von Netzwerkbrücken brauchst. Installier es einfach mit diesem Befehl:
    `apt-get install bridge-utils`
3. Aktualisiere die Datei `/etc/network/interfaces`:<br/>
    Achte darauf, dass in der Datei nur die Loopback-Schnittstelle (lo) aktiv ist. Alles, was mit deiner physischen Schnittstelle (z.B. enp4s0) zu tun hat, sollte entfernt werden.
    Beispielinhalt für die Datei  `/etc/network/interfaces`:
    ```bash
    # This file describes the network interfaces available on your system
    # and how to activate them. For more information, see interfaces(5).
    source /etc/network/interfaces.d/*
    # The loopback network interface
    auto lo
    iface lo inet loopback
    ```