# Übung 3.1: Weitere Kommandos

### FCK! Typo im Dateinamen DansGame

*ACHTUNG!* Folgende Syntax wird hier benutzt: 
```bash
# Alles in den Boxen sind Kommandos & Antworten aus der Maschine! (so sehen Kommentare aus)
$ Kommandos fangen mit $ an
der rest sind Antworten.
```

a) Probieren Sie die folgenden Befehle aus (der Befehl yes muss mit Ctrl+c
abgebrochen werden) und informieren Sie sich über die Bedeutung der einzelnen Kommandos und dessen Optionen:

* printenv |less
```bash
$ printenv |less
```
* export | wc
```bash
$ export | wc
     19      81    3813
```
* who
```bash
$ who
```
* whoami
```bash
$ whoami
redi
```
* yes
```bash
$ yes
# uhm :D lots of y
```
* yes \`whoami\`
```bash
$ yes
# lots of redi
```
* seq 1 12
```bash
$ seq 1 12
1
2
3
4
5
6
7
8
9
10
11
12
```
* seq -s \ 1 12
```bash
$ seq -s \ 1 12
1 12 13 14 15 16 17 18 19 110 111 112
```
* seq -s \| -w 1 12
```bash
seq -s \| -w 1 12
01|02|03|04|05|06|07|08|09|10|11|12
```
* grep \`whoami\` /etc/passwd
```bash
$ grep `whoami` /etc/passwd
redi:x:1000:1000:,,,:/home/redi:/bin/bash
```

# Übung 3.2: Sort, uniq und awk

a) Laden Sie sich aus Moodle die Datei famous.tar.gz herunter. Diese Datei ist
komprimiert und muss erst entpackt werden. Mit tar xfzv <dateiname> können Sie die Datei entpacken.

Ich habe die Datei auf meiner Website unter __https://static.redigermany.de/famous.tar.gz__ zur vefügung gestellt und nutze diese URL für ein wget
```bash
$ wget https://static.redigermany.de/famous.tar.gz
--2020-11-07 16:31:09--  https://static.redigermany.de/famous.tar.gz
Resolving static.redigermany.de (static.redigermany.de)... 85.13.162.234
Connecting to static.redigermany.de (static.redigermany.de)|85.13.162.234|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 319 [application/x-gzip]
Saving to: ‘famous.tar.gz’

famous.tar.gz                                100%[===========================================================================================>]     319  --.-KB/s    in 0s

2020-11-07 16:31:09 (1.72 MB/s) - ‘famous.tar.gz’ saved [319/319]
$ tar xfzv famous.tar.gz
famous.txt
```

b) Schauen Sie sich die Datei an. In dieser Datei befinden sich wichtige Persönlichkeiten der Informatik.
```bash
$ cat famous.txt
4. Torvalds, Linus
6. Tanenbaum, Andrew
5. Hopper, Grace
13. Stallman, Richard
3. Thompson, Ken
7. Hamilton, Margaret
8. Goldwasser, Shafi
1. Ritchie, Dennis
2. Bellovin, Steven
12. Raymond, Eric
16. Cox, Alan
15. Thompson, Ken
9. Bellovin, Steven
11. Turing, Alan
14. Lovelace, Ada,
10. Hopper, Grace
```

c) Wie Sie feststellen werden, ist diese Datei unsortiert. Finden Sie heraus wie
Sie mit sort die Datei numerisch aufsteigend sortieren können.
```bash
$ cat famous.txt | sort -n
1. Ritchie, Dennis
2. Bellovin, Steven
3. Thompson, Ken
4. Torvalds, Linus
5. Hopper, Grace
6. Tanenbaum, Andrew
7. Hamilton, Margaret
8. Goldwasser, Shafi
9. Bellovin, Steven
10. Hopper, Grace
11. Turing, Alan
12. Raymond, Eric
13. Stallman, Richard
14. Lovelace, Ada,
15. Thompson, Ken
16. Cox, Alan
```

d) In der Datei befinden sich doppelte Einträge. Wenn die Ausgabe von sort
an uniq über eine Pipe weitergeleitet wird, warum verschwinden dann die
doppelten Einträge nicht?
```bash
$ cat famous.txt | sort -n | uniq
1. Ritchie, Dennis
2. Bellovin, Steven
3. Thompson, Ken
4. Torvalds, Linus
5. Hopper, Grace
6. Tanenbaum, Andrew
7. Hamilton, Margaret
8. Goldwasser, Shafi
9. Bellovin, Steven
10. Hopper, Grace
11. Turing, Alan
12. Raymond, Eric
13. Stallman, Richard
14. Lovelace, Ada,
15. Thompson, Ken
16. Cox, Alan
# es verschwindet nichts, da die ersten Zeichen (in dem Fall die Nummerierung) unterschiedlich sind und uniq nur genau gleiche Zeilen heraus filtert
```

e) Finden Sie einen Weg (z.B. mit awk) um sich nur die Vornamen und Namen
ohne die Nummer ausgeben zu lassen.
```bash
$ awk '{print $2$3}' famous.txt
Torvalds,Linus
Tanenbaum,Andrew
Hopper,Grace
Stallman,Richard
Thompson,Ken
Hamilton,Margaret
Goldwasser,Shafi
Ritchie,Dennis
Bellovin,Steven
Raymond,Eric
Cox,Alan
Thompson,Ken
Bellovin,Steven
Turing,Alan
Lovelace,Ada,
Hopper,Grace
```

f) Wenn Sie jetzt den Befehl von Aufgabe (e) wieder an sort und an uniq weiterleiten (über eine Pipe) verschwinden die doppelten Einträge.
```bash
$ cat famous.txt | awk '{print $2$3}' | sort | uniq
Bellovin,Steven
Cox,Alan
Goldwasser,Shafi
Hamilton,Margaret
Hopper,Grace
Lovelace,Ada,
Raymond,Eric
Ritchie,Dennis
Stallman,Richard
Tanenbaum,Andrew
Thompson,Ken
Torvalds,Linus
Turing,Alan
```

g) Leiten Sie die Ausgabe von der vorherigen Aufgabe wieder an nl, damit die
Zeilen neu nummeriert werden.
```bash
$ cat famous.txt | awk '{print $2$3}' | sort | uniq | nl
     1  Bellovin,Steven
     2  Cox,Alan
     3  Goldwasser,Shafi
     4  Hamilton,Margaret
     5  Hopper,Grace
     6  Lovelace,Ada,
     7  Raymond,Eric
     8  Ritchie,Dennis
     9  Stallman,Richard
    10  Tanenbaum,Andrew
    11  Thompson,Ken
    12  Torvalds,Linus
    13  Turing,Alan
```

h) Leiten Sie die Ausgabe von der vorherigen Aufgabe in eine Datei um mit dem
Namen famous-new.txt. Die Datei sollte jetzt wie folgt aussehen:
```bash
$ cat famous.txt | awk '{print $2$3}' | sort | uniq | nl > famous-new.txt
```

i) Packen Sie die Datei erneut in famour-new.tar.gz mit tar -cvzf famous-new.tar.gz famous-new.txt.
```bash
$ tar -cvzf famous-new.tar.gz famous-new.txt
famous-new.txt
```
# Übung 3.3: Fragen

a) Schreiben Sie ein Kommando, das Ihnen anzeigt, wie viele Benutzer gerade
eingeloggt sind, und zwar in der Form: n users
```bash
$ uptime | awk '{print $4" users"}'
0 users
```

b) Mit welchem Befehl können Sie sich anzeigen lassen in welchem Ordner Sie
sich befinden?
```bash
$ pwd
/home/redi/uni
```

c) Mit welchem Befehl kommen Sie ins Wurzelverzeichnis /?
```bash
$ cd /
```

d) Wenn Sie sich in / befinden, wie können Sie Dateien aus Ihrem Heimatverzeichnis ansehen, ohne in das Verzeichnis zu wechseln?
```bash
$ ls ~/uni
famous-new.tar.gz  famous-new.txt  famous.tar.gz  famous.txt
```

e) Wie können Sie sich alle Dateien (auch versteckte Dateien) in einem Verzeichnis ansehen?
```bash
$ ls -a ~/uni
.  ..  famous-new.tar.gz  famous-new.txt  famous.tar.gz  famous.txt
# mit ~
```

f) Mit welchem Befehl können Sie die Ausgabe eines Linux Kommandos einfach zeilenweise filtern?
```bash
$ ls -la ~/uni | grep new
-rw-r--r-- 1 redi redi  315 Nov  7 16:41 famous-new.tar.gz
-rw-r--r-- 1 redi redi  280 Nov  7 16:40 famous-new.txt
# mit grep
```

g) Mit welchem Befehl können Sie die ausgegebenen Zeilen zählen?
```bash
$ ls -la ~/uni | grep new | wc -l
2
```
