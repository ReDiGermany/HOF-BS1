# Übung 2.1: Erkundung des Dateisystems

*ACHTUNG!* Folgende Syntax wird hier benutzt: 
```bash
# Alles in den Boxen sind Kommandos & Antworten aus der Maschine! (so sehen Kommentare aus)
$ Kommandos fangen mit $ an
der rest sind Antworten.
```

a) Wechseln Sie in Ihr Heimatverzeichnis mit cd ~ und überprüfen Sie das Verzeichniss mit pwd.

```bash
# Da ich dieses System privat auch nutze, mache ich alles im "uni" Unterverzeichnis!
$ cd ~/uni
$ pwd
/home/redi/uni
```

b) Listen Sie den Inhalt Ihres Heimatverzeichnisses mit ls, ls -l, ls -a, und
ls -la auf.

```bash
$ ls -l
total 0
$ ls -a
.  ..
$ ls -la
total 0
drwxr-xr-x 1 redi redi 4096 Nov  7 14:54 .
drwxr-xr-x 1 redi redi 4096 Nov  7 14:54 ..
$
```

c) Schauen Sie sich die Dokumentation von dem Befehl ls mit dem folgenden
Befehl an: man ls.
```bash
$ man ls
# {pager ansicht von man ls}
```

d) Wie groß ist die Datei /usr/share/doc/zip/copyright?
```bash
$ ls -l /usr/share/doc/zip/copyright
-rw-r--r-- 1 root root 3815 Aug 16  2015 /usr/share/doc/zip/copyright
# Die Datei ist also 3815 byte groß
```

# Übung 2.2: Elementare Datei- und Verzeichnisoperationen

a) Gehen Sie wieder zurück in Ihr Heimatverzeichnis. Welcher Befehl bringt
Sie schnell zurück?
```bash
$ cd ~/uni
```
b) Legen Sie mit mkdir 1.uebung ein neues Verzeichnis an.
```bash
$ mkdir 1.uebung
```

c) Kopieren Sie die Datei copyright aus Aufgabe 3.4, in dieses Verzeichnis mit
dem Befehl cp <quelle> <ziele>
```bash
$ cp /usr/share/doc/zip/copyright 1.uebung
```

d) Versuchen Sie die selbe Datei noch einmal in das gleiche Verzeichnis zu kopieren, benutzen Sie zusätzlich die Optionen -i -v, also cp -iv. Überschreiben Sie die vorhandene Datei nicht.
```bash
$ cp /usr/share/doc/zip/copyright 1.uebung
$ cp -i /usr/share/doc/zip/copyright 1.uebung
cp: overwrite '1.uebung'? n
$ cp -v /usr/share/doc/zip/copyright 1.uebung
'/usr/share/doc/zip/copyright' -> '1.uebung'
$cp -iv /usr/share/doc/zip/copyright 1.uebung
cp: overwrite '1.uebung'? n
```

e) Kopieren Sie die selbe Datei in das gleiche Verzeichnis unter dem Namen
copyleft mit nur einem Befehl.
```bash
$ cp /usr/share/doc/zip/copyright 1.uebung/copyleft
```

f) Benennen Sie die Datei copyleft um in copyfoo mit dem mv-Befehl: mv <quelle>
<ziel>
```bash
$ mv 1.uebung/copyleft 1.uebung/copyfoo
```

g) Löschen Sie die Datei copyfoo mit dem Befehl rm <datei>
```bash
$ rm 1.uebung/copyfoo
```

h) Die Datei copyright enthält lesbaren Text. Schauen Sie sich den Inhalt mit
den Befehlen cat und less an. Was ist der Unterschied zwischen den beiden
Befehlen?
```bash
$ cat 1.uebung/copyright
This is the Debian prepackaged version of "zip", Info-Zip's fast, portable,
zipfile compression utility.

This package is currently maintained by Santiago Vila <sanvila@debian.org>
and built from sources obtained from:

ftp://ftp.info-zip.org/pub/infozip/src/zip30.tgz

The changes were fairly minimal, and consisted solely of adding
various debian/* files to the distribution.

Copyright and license:

This is version 2007-Mar-4 of the Info-ZIP license.
The definitive version of this document should be available at
ftp://ftp.info-zip.org/pub/infozip/license.html indefinitely and
a copy at http://www.info-zip.org/pub/infozip/license.html.


Copyright (c) 1990-2007 Info-ZIP.  All rights reserved.

For the purposes of this copyright and license, "Info-ZIP" is defined as
the following set of individuals:

   Mark Adler, John Bush, Karl Davis, Harald Denker, Jean-Michel Dubois,
   Jean-loup Gailly, Hunter Goatley, Ed Gordon, Ian Gorman, Chris Herborth,
   Dirk Haase, Greg Hartwig, Robert Heath, Jonathan Hudson, Paul Kienitz,
   David Kirschbaum, Johnny Lee, Onno van der Linden, Igor Mandrichenko,
   Steve P. Miller, Sergio Monesi, Keith Owens, George Petrov, Greg Roelofs,
   Kai Uwe Rommel, Steve Salisbury, Dave Smith, Steven M. Schweda,
   Christian Spieler, Cosmin Truta, Antoine Verheijen, Paul von Behren,
   Rich Wales, Mike White.

This software is provided "as is," without warranty of any kind, express
or implied.  In no event shall Info-ZIP or its contributors be held liable
for any direct, indirect, incidental, special or consequential damages
arising out of the use of or inability to use this software.

Permission is granted to anyone to use this software for any purpose,
including commercial applications, and to alter it and redistribute it
freely, subject to the above disclaimer and the following restrictions:

    1. Redistributions of source code (in whole or in part) must retain
       the above copyright notice, definition, disclaimer, and this list
       of conditions.

    2. Redistributions in binary form (compiled executables and libraries)
       must reproduce the above copyright notice, definition, disclaimer,
       and this list of conditions in documentation and/or other materials
       provided with the distribution.  The sole exception to this condition
       is redistribution of a standard UnZipSFX binary (including SFXWiz) as
       part of a self-extracting archive; that is permitted without inclusion
       of this license, as long as the normal SFX banner has not been removed
       from the binary or disabled.

    3. Altered versions--including, but not limited to, ports to new operating
       systems, existing ports with new graphical interfaces, versions with
       modified or added functionality, and dynamic, shared, or static library
       versions not from Info-ZIP--must be plainly marked as such and must not
       be misrepresented as being the original source or, if binaries,
       compiled from the original source.  Such altered versions also must not
       be misrepresented as being Info-ZIP releases--including, but not
       limited to, labeling of the altered versions with the names "Info-ZIP"
       (or any variation thereof, including, but not limited to, different
       capitalizations), "Pocket UnZip," "WiZ" or "MacZip" without the
       explicit permission of Info-ZIP.  Such altered versions are further
       prohibited from misrepresentative use of the Zip-Bugs or Info-ZIP
       e-mail addresses or the Info-ZIP URL(s), such as to imply Info-ZIP
       will provide support for the altered versions.

    4. Info-ZIP retains the right to use the names "Info-ZIP," "Zip," "UnZip,"
       "UnZipSFX," "WiZ," "Pocket UnZip," "Pocket Zip," and "MacZip" for its
       own source and binary releases.
$ less 1.uebung/copyright
# {pager mit dem content von 1.uebung/copyright}
# => Cat gibt den Inhalt der Datei komplett aus, less nutzt einen Pager dafür. 
```

i) Löschen Sie das Verzeichnis 1.uebung mit dem Befehle: rm -r 1.uebung. Was
bedeutet die Option -r? Schauen Sie dazu in der man-Page nach.
```bash
$ rm -r 1.uebung
$ man rm
# ... {man rm snuppet}
# -r, -R, --recursive
#              remove directories and their contents recursively
# ...
# -r löscht alle Datein und Ordner in dem Ordner
```

# Übung 2.3: Dateirechte
a) Gehen Sie wieder zurück in Ihr Heimatverzeichnis und legen Sie ein neues
Verzeichnis mit dem Namen 2.uebung an und wechseln Sie in dieses.
```bash
$ mkdir 2.uebung
$ cd 2.uebung/
```

b) Legen Sie mit touch eine neue leere Datei an: touch neuedatei.txt.
```bash
$ touch neuedatei.txt
```

c) Welche Rechte besitzt die Datei neuedatei.txt und wie ist die dafür die Kurzfassung?
```bash
$ ls -l neuedatei.txt
-rw-r--r-- 1 redi redi 0 Nov  7 15:18 neuedatei.txt
# Alle können lesen, Benutzer kann schreiben und niemand kann ausführen.
# das erste Zeichen kann - oder d sein und definiert ob es ein Ordner oder eine Datei ist.
# die nächsten 3 Zeichen definieren die Rechte für den aktuellen Benutzer.
# die Zeichen 5-7 definieren die Rechte für die Gruppe in der der Benutzer drin ist 
# die Zeichen 8-10 definieren die Rechte für den Rest der Benutzer auf dem System
# Dabei stehen die Zeichen jeweils für R (read), W (write), X (execute)
```

d) Ändern Sie mit chmod die Rechte dieser Datei so, dass der Besitzer, die Gruppe
und alle Anderen alle Rechte an dieser Datei besitzen.
```bash
$ chmod 777 neuedatei.txt
$ ls -l neuedatei.txt
-rwxrwxrwx 1 redi redi 0 Nov  7 15:18 neuedatei.txt
```

e) Ändern Sie den Besitzer dieser Datei mit dem Befehl sudo chown nobody neuedatei.txt.
```bash
$ sudo chown nobody neuedatei.txt
[sudo] password for redi:
```

f) Ändern Sie die Gruppe dieser Datei auf nogroup mit dem Befehl sudo chgrp nogroup neuedatei.txt. Prüfen Sie mit ls ob alles funktioniert hat
```bash
$ ls -l neuedatei.txt
-rwxrwxrwx 1 nobody nogroup 0 Nov  7 15:18 neuedatei.txt
```

g) Löschen Sie den Ordner 2.uebung wieder
```bash
$ cd ..
$ rm -r 2.uebung/
```

# Übung 2.4: Texteditor

a) Gehen Sie wieder zurück in Ihr Heimatverzeichnis und legen Sie ein neues
Verzeichnis mit dem Namen 3.uebung an und wechseln Sie in dieses.
```bash
$ cd ~/uni
$ mkdir 3.uebung
$ cd 3.uebung/
```

b) Erstellen Sie mit vim vim.txt eine neue Datei und schreiben Sie ein paar Testdaten hinein. Speichern Sie diese Datei wieder und beenden Sie vim.
```bash
$ vim vim.txt
> askld ajsdkl ajösdk [esc] :wq [enter]
```

c) Starten Sie das Tutorial für vim über den Befehl vimtutor de und bearbeiten
Sie die Aufgaben bis Lektion 1.4.
```bash
$ vimtutor de
# dieses vim stinkt! ich nutze weiter nano DansGame
```

d) Erstellen Sie mit emacs emacs.txt eine weitere Datei und schreiben ebenfalls
einige Testdaten in diese Datei. Speichern Sie die Datei und beenden Sie
Emacs.
```bash
$ emacs emacs.txt
# dieses emacs stinkt noch viel mehr!
```

e) Öffnen Sie emacs nochmals und starten Sie das Tutorial über die Tastenkombination +h t. Lernen Sie die ersten Grundzüge von Emacs.
```bash
# hier streike ich
```

f) Löschen Sie den Ordner 3.uebung wieder.
```bash
$ cd ..
$ rm -r 3.uebung/
```

# Übung 2.5: Filter und Weiterleitungen

a) Gehen Sie wieder zurück in Ihr Heimatverzeichnis und legen Sie ein neues
Verzeichnis mit dem Namen 4.uebung an und wechseln Sie in dieses.
```bash
$ cd ~/uni
$ mkdir 4.uebung
$ cd 4.uebung/
```

b) Schauen Sie sich die Ausgabe des Kommandos uname -a am Bilschirm an.
```bash
$ uname -a
Linux ReDiBook2 4.4.0-19041-Microsoft #488-Microsoft Mon Sep 01 13:43:00 PST 2020 x86_64 GNU/Linux
```

c) Leiten Sie die Ausgabe des Kommandos uname -a in die Datei kernel.txt und
überprüfen Sie den Inhalt mit dem cat-Befehl.
```bash
$ uname -a > kernel.txt
$ cat kernel.txt
Linux ReDiBook2 4.4.0-19041-Microsoft #488-Microsoft Mon Sep 01 13:43:00 PST 2020 x86_64 GNU/Linux
```

d) Was macht der Befehl uptime?
```bash
$ uptime
 15:37:54 up 50 min,  0 users,  load average: 0.52, 0.58, 0.59
# Wir sehen die Zeit, wie lange die Maschine an ist, wie viele zusätzliche Benutzer online sind und den load average (what ever das ist. hat glaub ich was mit den festplatten zutun)
```

e) Schreiben Sie Ausgabe von uptime an das Ende der Datei kernel.txt und überprüfen Sie wieder den Inhalt.
```bash
$ uptime >> kernel.txt
$ cat kernel.txt
Linux ReDiBook2 4.4.0-19041-Microsoft #488-Microsoft Mon Sep 01 13:43:00 PST 2020 x86_64 GNU/Linux
 15:38:59 up 51 min,  0 users,  load average: 0.52, 0.58, 0.59
```

f) Schauen Sie sich den Inhalt der Verzeichnisse / und /XYZ mit dem Befehl ls / /XYZ an. Sie erhalten zusätzlich eine Fehlermeldung, weil das Verzeichnis /XYZ nicht existiert.
```bash
$ ls / /XYZ
ls: cannot access '/XYZ': No such file or directory
/:
bin  boot  dev  etc  home  init  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
```

g) Wiederholen Sie den Befehl und fügen Sie die Standardausgabe an das Ende
der Datei kernel.txt.
```bash
$ ls / /XYZ >> kernel.txt
ls: cannot access '/XYZ': No such file or directory
```

h) Wiederholen Sie den Befehl noch einmal und schreiben alles in eine neue
Datei error.txt. Überprüfen Sie wieder den Inhalt mit cat.
```bash
$ ls / /XYZ > error.txt 2>&1
$ cat error.txt
ls: cannot access '/XYZ': No such file or directory
/:
bin
boot
dev
etc
home
init
lib
lib64
media
mnt
opt
proc
root
run
sbin
srv
sys
tmp
usr
var
```

i) Geben Sie den Inhalt von kernel.txt mit dem cat-Befehl aus und filtern mit
grep die Ausgabe so dass nur die Zeilen angezeigt werden in denen das Wort
Linux vorkommt.
```bash
$ cat kernel.txt | grep Linux
Linux ReDiBook2 4.4.0-19041-Microsoft #488-Microsoft Mon Sep 01 13:43:00 PST 2020 x86_64 GNU/Linux
```

j) Geben Sie den Inhalt von kernel.txt mit dem cat-Befehl aus zählen die Anzahl der Zeilen mit wc -l
```bash
$ cat kernel.txt | wc -l
23
```

k) Löschen Sie den Ordner 4.uebung wieder.
```bash
$ cd ..
$ rm -r 4.uebung/
```
