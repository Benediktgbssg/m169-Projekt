# SQL Dump
### Folgender Befehl muss in der Ubuntu-Shell auf der alten Moodle-VM ausgeführt werden:
```
sudo mysqldump -u root -p moodle > moodle_dump.sql
```
Mit diesem Befehl wird ein SQL-Dump der Moodle-Datenbank erstellt. Die Daten werden aus der Datenbank gelesen und in die Datei `moodle_dump.sql` geschrieben. Der Befehl erstellt die Datei automatisch. 

Zu beachten ist, dass für diesen Vorgang zwei Passwörter erforderlich sind (beide Male das Riethüsli Standardpasswort). Zum einen das Passwort des VM-Benutzers (aufgrund des `sudo`-Befehls) und zum anderen das Passwort der Datenbank.

## Speicherort des Dump-Files

Der SQL-Dump wird im Home-Verzeichnis abgespeichert. Die Datei wird dann für das Migrieren auf die neue Docker-Infrastruktur benötigt.
