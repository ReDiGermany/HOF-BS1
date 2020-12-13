# Übung 9.1: Speichermanagement

a) Sortieren Sie die folgenden Speicher aufsteigend nach der Zugriffzeit, angefangen mit dem schnellsten Zugriff:
	• Random Access Memory (RAM)
	• Magnetische Festplate (HDD)
	• Prozessor Cache
	• Solid-State-Drive (SSD)
	• Prozessor Register

```
• Prozessor Register
• Prozessor Cache
• Random Access Memory (RAM)
• Solid-State-Drive (SSD)
• Magnetische Festplate (HDD)
```

b) Schauen Sie sich die Datei /proc/meminfo an und finden Sie heraus:
	b.a) Wie viel physikalischer Speicher steht der virtuellen Maschine zur Verfügung?
	b.b) Wie viel physikalischer Speicher ist noch frei?
	b.c) Wie viel Swap-Speicher steht zur Verfügung?
	b.d) Wie viel Swap-Speicher wird gerade benutzt?

```bash
$ cat /proc/meminfo
MemTotal:       16696708 kB
MemFree:         6679756 kB
Buffers:           34032 kB
Cached:           188576 kB
SwapCached:            0 kB
Active:           167556 kB
Inactive:         157876 kB
Active(anon):     103104 kB
Inactive(anon):    17440 kB
Active(file):      64452 kB
Inactive(file):   140436 kB
Unevictable:           0 kB
Mlocked:               0 kB
SwapTotal:      30954108 kB
SwapFree:       30626612 kB
Dirty:                 0 kB
Writeback:             0 kB
AnonPages:        102824 kB
Mapped:            71404 kB
Shmem:             17720 kB
Slab:              13868 kB
SReclaimable:       6744 kB
SUnreclaim:         7124 kB
KernelStack:        2848 kB
PageTables:         2524 kB
NFS_Unstable:          0 kB
Bounce:                0 kB
WritebackTmp:          0 kB
CommitLimit:      515524 kB
Committed_AS:    3450064 kB
VmallocTotal:     122880 kB
VmallocUsed:       21296 kB
VmallocChunk:      66044 kB
HardwareCorrupted:     0 kB
AnonHugePages:      2048 kB
HugePages_Total:       0
HugePages_Free:        0
HugePages_Rsvd:        0
HugePages_Surp:        0
Hugepagesize:       2048 kB
DirectMap4k:       12280 kB
DirectMap4M:      897024 kB
```
```
b.a) MemTotal:       16696708 kB
b.b) MemFree:         6679756 kB
b.c) SwapTotal:      30954108 kB
b.d) SwapFree:       30626612 kB
```

c) Finden Sie heraus wie groß eine PAGE auf dem Laborrechner ist mit getconf PAGE_SIZE.
```bash
$ getconf PAGE_SIZE
4096
```
	c.a) Jeder Prozess hat einen eigenen Ordner im /proc/ Verzeichnis. Starten Sie Firefox und suchen Sie sich die pid entsprechend raus. Gehen Sie dann in das Verzeichnis /proc/<pid>/ und geben Sie die Datei stat aus. Die Ausgabe ist eine ganze Reihe Zahlen. Lesen Sie sich man 5 proc unter dem Punkt stat und welcher dieser Zahlen gibt die echte Anzahl an Pages wieder?
```bash
# Da ich im WSL bin, kann ich Firefox nicht starten.
# Daher:
$ nano test.py
# import time

# while(True):
#         time.sleep(1000)
$ python test.py &
$ ps aux | grep python
redi       228  0.0  0.0  21112  4752 tty1     S    14:12   0:00 python test.py
redi       233  0.0  0.0  14120  1148 tty1     S    14:14   0:00 grep test.py
$ cat /proc/228/stat
228 (python) S 7 228 6 1025 0 0 0 0 0 0 3 0 0 0 20 0 1 0 41505 66245066752 1188 18446744073709551615 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0

  # (29) kstkesp  %lu  [PT]
            # The current value of ESP (stack pointer), as found in the kernel stack page for the process.
# edit: (24)
```
	c.b) Schreiben Sie ein Shell-Skript welches die vorherige Aufgabe automatisiert, d.h. Sie übergeben dem Skript die pid und dieses sucht sich automatisch die Anzahl der Pages aus der stat Datei heraus. Falls es die pid nicht gibt, soll eine entsprechende Fehlermeldung ausgegeben werden. Hinweis Bei fast jedem Unix/Linux System ist das Tool awk installiert. Dieses dient	dazu Text aus Dateien zu extrahieren. Mit diesem lässt sich Übung 9.1.cb einfach lösen.
```bash
$ nano GetPages
#!/bin/bash

ID=29
if [[ "$1" -ne "" ]]
then
        if [[ -d "/proc/"$1 ]]
        then
                # cat /proc/$1/stat | tr " " "\n" | head -$ID | tail -1
                # cat /proc/$1/stat | awk '{print $'$ID'}'
                awk '{print $'$ID'}' /proc/$1/stat
        else
                echo "Falsche PID"
        fi
else
        echo "Bitte PID angeben."
fi
$ chmod +x GetPages
$ ./GetPages 228
0
$ ./GetPages 123
Falsche PID
$ ./GetPages
Bitte PID angeben.
```

d) Lesen Sie die man-page von vmstat. Was können Sie mit diesem Tool machen? Starten vmstat 5 in einem Terminal und verfolgen Sie für ein paar Sekunden die Ausgabe. Starten Sie dann Firefox. Welche Veränderung können Sie in der Ausgabe von vmstat erkennen.
```
Wird verschoben, da mein WSL nicht mit spielt.
DESCRIPTION
       vmstat reports information about processes, memory, paging, block IO, traps, disks and cpu activity.

       The  first  report produced gives averages since the last reboot.  Additional reports give information on a sampling period of length delay.  The process and memory reports are instantaneous in either case. 
```

e) Laden Sie sich aus Moodle die Datei uebung9-benchmark herunter. Das Programm erstellt ein Array mit 100 Elemente. Danach misst es die Anzahl der Takte die vergehen wenn man auf ein Element von dem Array zugreift. Führen Sie das Programm ein paar Mal aus. Was können Sie erkennen? Erklären Sie warum dieses Verhalten auftritt? Für Interessierte ist der Quelltext im Moodle ebenfalls verfügbar.
```
30tes element nr 2 geht schneller als 1 da es im cache drin ist
```

f) Erklären Sie kurz was der Translation Lookaside Buffer (TLB) macht?
```

```

g) Laden Sie sich aus Moodle die Datei uebung9-so herunter und schauen Sie sich auch denQuelltext an. Führen Sie das Programm aus. Was passiert? Erklären Sie warum dieses Verhalten auftritt.
```
stackOverflow
Segmentation fault (core dumped)
```

h) Mit dem Programm ulimit können Sie heraus finden welche RessourcenGrenzen in Ihrem System gesetzt sind. Die Option --help zeigt Ihnen die verschiedenen Parameter an. Finden Sie heraus, welche Grenze für den Stack gesetzt sind.
```
$ ulimit -s
8192
```

i) Erklären Sie was ist der Unterschied zwischen dem Stack und dem Heap und welcher von beiden Speicher wird mit Instruktionen vom Prozessor unterstützt?
```
Stack zuerst, heap danach
```

j) Warum müssen Sie den Speicher von lokale Variablen in einer Funktion oder einer Methode nicht wieder freigeben?
```
Der Stackframe wird "weggeschmissen", wenn die funktion fertig ist und lokale Variablen sind nur auf dem Stackframe.
```
