# Übung 5.1: Shell-Programmierung 2

a) Modifizieren Sie die Ihr Programm von Aufgabe 4.1 c) so um dass der Dateiname nicht eingelesen wird, sondern als Argument an das Skript erfolgt. Wenn kein oder die falsche Anzahl an Argumente übergeben wurde, soll dies vorher über eine Fehlermeldung abgefangen werden.
```bash
#!/bin/bash

FILE=$1

if [[ "$FILE" == "" ]]
then
        echo "Bitte Datei angeben!"
        exit
fi

if [ -f $FILE ]
then
        echo $FILE" ist eine Datei"
elif [ -d $FILE ]
then
        echo $FILE" ist ein Ordner"
else
        echo $FILE" existiert nicht"
fi
file $FILE
```

a.a) Modifizieren Sie nochmals das Script und zwar diesmal so dass es mit einer beliebigen Anzahl an Parametern funktioniert. Das bedeutet, man kann das Skript auch mit 2 oder mehreren Dateien als Parameter aufrufen.
```bash
#!/bin/bash

if [ $# -lt 1 ]
then
        echo "Bitte Datei angeben!"
        exit
fi

for FILE in $@
do
	if [ -f $FILE ]
	then
	        echo $FILE" ist eine Datei"
	elif [ -d $FILE ]
	then
	        echo $FILE" ist ein Ordner"
	else
	        echo $FILE" existiert nicht"
	fi
	file $FILE
	echo ""
done
```

b) Schreiben Sie ein Shell-Skript was cat /etc/shadow ausführt und den Rückgabewert auswertet. Je nach dem ob der Befehl erfolgreich war, soll eine entsprechende Meldung ausgegeben werden.
```bash
#!/bin/bash
cat /etc/shadow > /dev/null 2>&1

if [[ $? -eq 0 ]]
then
        echo "Okay!"
else
        echo "Keine Rechte!"
fi
```

c) Schreiben Sie ein Shell-Skript welches die Dateien in einem Verzeichnis zählt. Diese Funktionalität soll als Funktion ausgelagert werden, so dass man im Skript nur noch file_count /etc/ angeben muss. Testen Sie Ihre Funktion mit drei Verzeichnissen Ihrer Wahl.
```bash
#!/bin/bash

file_count() {
        FILE=$1
        COUNT=$(ls -l $FILE | wc -l)
        echo "In "$FILE" gibt es "$COUNT" Datein"
}
file_count /etc/
file_count /
file_count ~
```

d) Schreiben Sie ein Shell-Skript welches im aktuellen Verzeichnis alle Dateinamen die auf *.jpg enden umbenennt in YYYY-MM-DD-*.jpg. Wenn sich beispielsweise ein Bild test.jpg im aktuellen Verzeichnis befindet und heute der 13. November 2019 ist, dann würde das Skript den Dateinamen von test.jpg in 2019-11-13-test.jpg ändern. Das aktuelle Datum bekommt man über den date befehl. Lesen Sie die man-page wie Sie das Datum vorgegeben Format bekommen.
```bash
#!/bin/bash
DATE=$(date +%F)

for file in *.jpg
do
        mv $file $DATE"-"$file
done
```

e) Schreiben Sie eine eigenen Variante von rm mit dem Namen rm-trash. Diese soll statt einer Datei oder ein Verzeichnis zu löschen diese in einem TrashOrdner verschieben. Dieser Trash-Ordner ist abhängig vom Benutzer und befindet sich in dem relativen Pfad .local/share/Trash/files/. Falls sich Dateien in dieser Ordner befinden, sollen die Dateien nach dem Verschieben angezeigt und gefragt werden ob der Mülleimer gelöscht werden soll. Bei y soll der Inhalt des Ordners gelöscht werden, falls nicht, eben nicht.
```bash
#!/bin/bash

dir=$HOME/\.local/share/Trash/files/
mkdir -p $dir
mv $@ $dir
if [[ $(ls -1 $dir | wc -l) -ne 0 ]]
then
        ls -1 $dir
        read -p "Papierkorb löschen? [y/n] " del
        if [[ "$del" == "y" ]]
        then
                rm -r $dir
                echo "Alles gelöscht"
        else
                echo "Nicht löschen."
        fi
else
        echo "Nichts gelöscht."
fi
```
