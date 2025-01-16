## Setze eine ACL für das Verzeichnis 
Die folgende Commandos sorgen dafür, dass der Benutzer zerlix und die Gruppe www-data für neu erstellte Dateien im Verzeichnis /var/www automatisch die richtigen Berechtigungen erhalten.
```bash
#!/bin/bash

# Benutzer und Gruppe definieren
USER="www-data"
GROUP="www-data"

# Verzeichnis, auf das die ACLs angewendet werden
TARGET_DIR="/var/www"

# Standard-ACLs für Verzeichnisse setzen (rwx)
setfacl -d -m u:$USER:rwx $TARGET_DIR
setfacl -d -m g:$GROUP:rwx $TARGET_DIR

# Standard-ACLs für Dateien setzen (rw-)
setfacl -d -m u:$USER:rw- $TARGET_DIR
setfacl -d -m g:$GROUP:rw- $TARGET_DIR

# Rekursiv für alle bestehenden Verzeichnisse die ACLs setzen (rwx)
find $TARGET_DIR -type d -exec setfacl -m u:$USER:rwx -m g:$GROUP:rwx {} \;

# Rekursiv für alle bestehenden Dateien die ACLs setzen (rw-)
find $TARGET_DIR -type f -exec setfacl -m u:$USER:rw- -m g:$GROUP:rw- {} \;

# Optional: Masken-Berechtigungen für Dateien auf rw- setzen (um das x zu verhindern)
setfacl -d -m mask::rw- $TARGET_DIR

# Setzen des setgid-Flags für das Verzeichnis, damit neue Dateien die Gruppe des Verzeichnisses übernehmen
chmod g+s $TARGET_DIR

echo "ACLs für Verzeichnisse und Dateien im Verzeichnis $TARGET_DIR wurden gesetzt."
echo "Das setgid-Flag wurde gesetzt, sodass neue Dateien die Gruppe des Verzeichnisses übernehmen."