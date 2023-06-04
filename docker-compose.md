# Dokumentation des Docker Compose File

## Version
```yaml
version: '3.7'
```
## Services
### MariaDB
```
services:
  mariadb:
    image: mariadb
    restart: always
    volumes:
      - /srv/Configs/Databases/Moodle:/var/lib/mysql
    environment:
      - MYSQL_ROOT_PASSWORD=moodle
      - MYSQL_ROOT_USER=root
      - MYSQL_DATABASE=moodle
    networks:
     - moodlenet
```

<br>

> Der Service mariadb verwendet das Image mariadb und wird immer automatisch neu gestartet.
> Die Datenbankdateien werden auf dem Host in /srv/Configs/Databases/Moodle gespeichert. 
> Es werden Umgebungsvariablen für das Root-Passwort, den Root-Benutzer und den Datenbanknamen festgelegt.
> Mariadb läuft im Netzwerk moodlenet.

### Moodle

```
 moodle:
    image: bitnami/moodle:4.2.0
    restart: always
    ports:
      - 80:8080
    environment:
      - MOODLE_DATABASE_HOST=mariadb
      - MOODLE_DATABASE_USER=root
      - MOODLE_DATABASE_PASSWORD=moodle
      - MOODLE_DATABASE_NAME=moodle
    networks:
     - moodlenet
    volumes:
      - /srv/Configs/Moodle:/bitnami/moodle
      - /srv/Configs/MoodleData:/bitnami/moodledata
    depends_on:
      - mariadb
```

<br>

> Der Service moodle verwendet das Image bitnami/moodle:4.2.0 und wird immer automatisch neu gestartet. 
> Der Service ist über den Port 80 erreichbar. Es werden Umgebungsvariablen für den Datenbankhost, 
> den Datenbankbenutzer, das Datenbankpasswort und den Datenbanknamen festgelegt. Zudem werden Volumes 
> für die Moodle-Konfiguration und -Daten definiert. Der Service hängt von mariadb ab, um sicherzustellen, 
> dass die Datenbank verfügbar ist.
> Ausserdem wir dem Service moddle auch noch das Netwerk moodlenet zugewiesen.

### phpMyAdmin

```
  phpmyadmin:
    image: phpmyadmin/phpmyadmin
    links:
      - mariadb
    environment:
      PMA_HOST: mariadb
      PMA_PORT: 3306
      PMA_ARBITRARY: 1
    networks:
     - moodlenet
    restart: always
    ports:
      - 8081:80
networks:
 moodlenet:
```

<br>

> Der Service phpmyadmin verwendet das Image phpmyadmin/phpmyadmin und wird immer automatisch neu gestartet. 
> Der Service ist über den Port 8081 erreichbar. Es wird eine Verbindung zu mariadb hergestellt und Umgebungsvariablen 
> für den Host und den Port von MariaDB festgelegt. Der Service ermöglicht den Zugriff auf die Datenbank über phpMyAdmin.
> Ausserdem wir dem Service phpmyadmin auch noch das Netwerk moodlenet zugewiesen.

> Dieses Docker Compose File stellt eine Moodle-Instanz mit MariaDB-Datenbank und phpMyAdmin bereit. 
> Es ermöglicht die einfache Bereitstellung und Verwaltung einer Moodle-Umgebung.
