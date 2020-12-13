# Übung 10.1: Dateisysteme
a) Nennen Sie fünf verschiedene Dateisysteme.
```
FAT32, NTFS, APFS+, EXT1-4, FAT16 
```

b) Erklären Sie kurz was ein Bootloader ist und warum man diesen braucht?
```
Der Bootloader ist das Stück Software, welches den MBR lädt.
```

c) Prüfen Sie auf dem Laborrechner welches Dateisystem für die Partition /home benutzt wird.
Hinweis: Der Befehl mount zeigt Ihnen alle eingebundenen Geräte und Partitionen an. Mit dem Befehl kann man auch neue Geräte einbinden.
```bash
$ mount
rootfs on / type lxfs (rw,noatime)
none on /dev type tmpfs (rw,noatime,mode=755)
sysfs on /sys type sysfs (rw,nosuid,nodev,noexec,noatime)
proc on /proc type proc (rw,nosuid,nodev,noexec,noatime)
devpts on /dev/pts type devpts (rw,nosuid,noexec,noatime,gid=5,mode=620)
none on /run type tmpfs (rw,nosuid,noexec,noatime,mode=755)
none on /run/lock type tmpfs (rw,nosuid,nodev,noexec,noatime)
none on /run/shm type tmpfs (rw,nosuid,nodev,noatime)
none on /run/user type tmpfs (rw,nosuid,nodev,noexec,noatime,mode=755)
binfmt_misc on /proc/sys/fs/binfmt_misc type binfmt_misc (rw,relatime)
tmpfs on /sys/fs/cgroup type tmpfs (rw,nosuid,nodev,noexec,relatime,mode=755)
cgroup on /sys/fs/cgroup/devices type cgroup (rw,nosuid,nodev,noexec,relatime,devices)
C:\ on /mnt/c type drvfs (rw,noatime,uid=1000,gid=1000,case=off)

# hm... :D lxfs?
```

d) Erstellen Sie eine neue Datei mit dem Namen blocksize.txt und schreiben Sie hello hinein. Prüfen Sie dann mit du -h wie groß die Datei ist. Erklären Sie warum diese Datei so groß ist.
```
Wegen den Meta Informationen.
```

e) Für was ist das erste Byte in der Partitionstabelle zuständig? Welche Möglichkeiten gibt es hier?
```
Es gibt 0x00 oder 0x80.
0x80 ist eine bootbare Partition, 0x00 nicht.
```

f) Wir erinnern uns, dass unter Linux/Unix alles eine Datei ist. Auch Peripheriegeräte wie Festplatten oder Partitionen werden über spezielle Dateien in /dev/ angesprochen. Prüfen Sie welches Gerätename für die Partition / benutzt wird. Mit sudo dumpe2fs -h </dev/gerätename> können Sie den Superblock der Partition auslesen. Wie viele Blöcke und Inodes sind noch frei?
```
geht nicht weil WSL
```

g) Mit fdisk -l <device> (ohne Nummer am Ende) können Sie sich die Partitionstabelle der Festplatte anzeigen lassen. Wie sieht die Partitionstabelle auf der virtuellen Maschine aus?
```bash
$ fdisk -l
fdisk: cannot open /proc/partitions: No such file or directory
```

h) Was ist der Master Boot Record (MBR) und was passiert wenn dieser versehentlich gelöscht wurde? Könnte man diesen theoretisch wieder herstellen?
```
Der MBR kümmert sich um die Bootreihenfolge der Betriebssysteme und lässt den Benutzer entscheiden, welches Betriebssystem gebootet wird.
Ja kann man mithilfe eines live systems.
```

i) Warum ist Fragmentierung notwendig?
```
Fragmentierung und notwendig, damit man den Speicherplatz vollständig nutzen kann und der nicht nach 5gb schon voll ist, weil es keine groß genugen lücken auf der Festplatte gibt.
```

j) Mit dem Befehl stat können Sie die I-Node Informationen von einer Datei anzeigen lassen. Rufen Sie stat blocksize.txt auf und studieren Sie die Ausgabe. Bei den Angaben zu der Anzahl der Blöcke sind physikalische Blöcke zu je 512 bytes gemeint. Warum ist der Wert 8?
```
?
$ stat blocksize.txt
  File: blocksize.txt
  Size: 6               Blocks: 0          IO Block: 4096   regular file
Device: 2h/2d   Inode: 10133099161738075  Links: 1
Access: (0644/-rw-r--r--)  Uid: ( 1000/    redi)   Gid: ( 1000/    redi)
Access: 2020-12-13 19:52:40.057010600 +0100
Modify: 2020-12-13 19:52:40.058022800 +0100
Change: 2020-12-13 19:52:40.058022800 +0100
 Birth: -
```

k) Welche zwei Zugriffsarten auf Dateien innerhalb eines Dateisystems kennen Sie? Welche davon sollten effizient sein?
```
Keine Ahnung, was gemeint ist.
```