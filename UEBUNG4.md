# Übung 4.1: Shell-Programmierung 1

a) Schreiben Sie ein Shell-Skript was Shell Scripting is Fun auf dem Bildschirm
ausgibt.
```bash
#!/bin/bash

echo "Shell Scripting is Fun"
```

a.a) Modifizieren Sie nun das Skript so, dass der Text Shell Scripting is Fun in einer Variable steht und nur diese ausgegeben wird.
```bash
#!/bin/bash

MYVAR="Shell Scripting is Fun"
echo $MYVAR
```

a.b) Erweitern Sie das Skript um eine Abfrage nach dem Vornamen, der in eine weitere Variable gespeichert wird und danach ebenfalls ausgegeben wird.
```bash
#!/bin/bash

read -p "Vorname: " NAME
MYVAR="Shell Scripting is Fun"
echo $MYVAR
echo $NAME
```

a.c) Modifizieren Sie das Skript so, dass der Text Shell Scripting is Fun und der Name nur ausgegeben wird, wenn Ihr Vorname eingegeben wurde. Ansonsten soll es zu keiner Ausgabe kommen.
```bash
#!/bin/bash

read -p "Vorname: " NAME

if [ "$NAME" != "" ]
then
        MYVAR="Shell Scripting is Fun"
        echo $MYVAR
        echo $NAME
fi
```

b) Schreiben Sie ein neues Shell-Skript welches die Tiere Hund, Katze, Biber,
Schwein, Schaf separat auf einer Zeile ausgibt. Nutzen Sie dafür Schleifen.
```bash
#!/bin/bash

for pet in Hund Katze Biber Schwein Schaf
do
        echo $pet
done
```

c) Schreiben Sie ein Shell-Skript welches den Benutzer nach einem Dateinamen
fragt und in eine Variable speichert. Ihr Skript soll nun prüfen ob es bei diesem Dateinamen um eine normale Datei oder um ein Verzeichnis handelt. Je
nach dem soll eine entsprechende Meldung ausgegeben werden. Trifft beides nicht zu, soll ebenfalls eine entsprechende Meldung ausgegeben werden.
Ganz am Ende soll mittels dem file Befehl überprüft werden um welchen
Typ es sich handelt.
```bash
#!/bin/bash

read -p "Dateiname: " FILE

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

d) Schreiben Sie eine eigene ls-Variante mit dem Namen ls-txt, welche nur
Dateien auflistet die mit *.txt enden. Die Bedienung soll über eine Variable definiert werden. Jede *.txt-Datei soll geprüft werden ob dieser größer
als 10 Bytes ist. Nur dann soll diese ausgegeben werden. Kopieren Sie diese Datei in /usr/local/bin und testen Sie ob Ihr Programm auch in anderen
Verzeichnissen funktioniert.
```bash
#!/bin/bash

for FILE in *.txt
do
        size=$(ls -l $FILE | awk '{print $5}')
        if [[ $size -gt 10 ]]
        then
                echo $FILE" "$size
        else
                echo $FILE" zu klein"
        fi
done
```
