# Apache unter Debian Linux


## VirtualHost


```bash	
<VirtualHost *:80>
    ServerAdmin webmaster@example.com
    ServerName laravel.lab
    ServerAlias www.laravel.lab
    DocumentRoot /mnt/raid/var/www/laravel.lab/public

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined

    <Directory /mnt/raid/var/www/laravel.lab/public>
        Options Indexes FollowSymLinks MultiViews
        AllowOverride All
        Require all granted
    </Directory>

    # Schutz für das Projektverzeichnis
    <Directory /mnt/raid/var/www/laravel.lab>
        Options -Indexes
        Require all denied
    </Directory>
</VirtualHost>

```
Aktivierung des VHosts:

```bash
a2ensite example.com.conf
systemctl reload apache2
```
