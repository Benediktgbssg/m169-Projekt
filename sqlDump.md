# SQL Dump

In diesem Markdown-Dokument wird erklärt, wie man einen SQL-Dump der Moodle-Datenbank erstellt.

## Befehl:

sudo mysqldump -u root -p moodle > moodle_dump.sql


Mit diesem Befehl wird ein SQL-Dump der Moodle-Datenbank erstellt. Die Daten werden aus der Datenbank gelesen und in die Datei `moodle_dump.sql` geschrieben. Der Befehl erstellt die Datei automatisch. 

Bitte beachten Sie, dass für diesen Vorgang zwei Passwörter erforderlich sind. Zum einen das Passwort des VM-Benutzers (aufgrund des `sudo`-Befehls) und zum anderen das Passwort der Datenbank.

## Speicherort des Dump-Files

Der SQL-Dump wird im Home-Verzeichnis abgespeichert. Sie können die Datei `moodle_dump.sql` verwenden, um die Struktur und alle Daten der Moodle-Datenbank wiederherzustellen.
