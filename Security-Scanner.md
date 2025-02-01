# 1. Web Security Scanner (Allgemeine Sicherheitstests)

* OWASP ZAP (Open Source) - https://www.zaproxy.org/
    * Automatisierter Security-Scanner für Webanwendungen
    * Findet XSS, SQL-Injection, Directory Traversal, CSRF und mehr
    * CLI-Modus für CI/CD-Integration

* Burp Suite (Freemium) - https://portswigger.net/burp
    * Man-in-the-Middle (MITM)-Proxy für Web-Sicherheitstests
    * Automatische und manuelle Schwachstellenanalyse
    * Kostenlose Version hat eingeschränkte Funktionen

* Nikto (Open Source) - https://cirt.net/Nikto2
    * Scannt veraltete Software, unsichere Konfigurationen und Standard-Passwörter
    * Findet bekannte Sicherheitslücken in Webservern (Apache, Nginx, # etc.)

# 2. SQL-Injection & XSS Scanner
* SQLmap (Open Source) - https://sqlmap.org/
    * Automatisiert das Finden und Ausnutzen von SQL-Injection-Schwachstellen
    * Kann Datenbank-Hashes extrahieren und Benutzerrechte testen

* XSSer (Open Source) -https://xsser.03c8.net/
    * Automatisierter Cross-Site-Scripting (XSS) Scanner
    * Findet Reflected, Stored und DOM-basierte XSS-Lücken

# 3. Wordpress Security Scanner
* WPScan  (Open Source) - https://wpscan.com/
    * Findet usichere Plugins, Themes und Standard-Passwörter in WordPress
    * Nutzt eine große Datenbank mit bekannten WordPress-Sicherheitslücken

# 4. Infrastruktur- und Netzwerksicherheit

* Nmap (Open Source) - https://nmap.org/
    * Erkennt offene Ports und Dienste, die Angreifer ausnutzen könnten
    * Mit nmap --script vuln <IP> kannst du Sicherheitslücken testen

* OpenVAS (Open Source) - https://greenbone.github.io/docs/latest/
    * Vollständiger Schwachstellen-Scanner für Server und Netzwerke
    * Findet unsichere Konfigurationen und veraltete Software


# 5. CI/CD Security 
* Trivy (Open Source) -https://trivy.dev/
    * Scannt Docker-Container, Dateien und Abhängigkeiten auf Sicherheitslücken

* 6. Snyk (Freemium) - https://snyk.io/de/
    Findet unsichere Abhängigkeiten in Composer, npm, pip, Maven