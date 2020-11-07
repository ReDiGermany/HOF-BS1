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