# Übung 6.1: Systemaufrufe (system calls)

a) Machen Sie sich mit dem Programm strace vertraut und lesen Sie dazu die
man-page. Was bedeuten die Optionen -e, -f und -p?
```bash
$ man strace
No manual entry for strace
$ strace
-bash: strace: command not found
$ sudo apt install strace
[sudo] password for redi:
$ man strace
# -e ist der parameter, für filterungen
# -f beinhaltet auch sub prozesse, die gestartet werden
# -p definiert die Prozess ID von einem laufenden prozess
```

b) Laden Sie sich aus Moodle das statisch kompilierte Programm hello-world
herunter und führen Sie es aus. Nutzen Sie nun strace um die Systemaufrufen
von hello-world heraus zu finden. Leiten Sie die Ausgabe von strace dazu in
die Datei hello-world-strace.txt um und analysieren Sie diese:
a) Mit welchem Systemaufruf startet das Programm hello-world? Warum?
```bash
$ chmod +x hello-world
# eigentlich ./hello-world
$ strace ./hello-world
execve("./hello-world", ["./hello-world"], 0x7fffe425b690 /* 20 vars */) = 0
arch_prctl(0x3001 /* ARCH_??? */, 0x7fffc22e43a0) = -1 EINVAL (Invalid argument)
brk(NULL)                               = 0x195c000
brk(0x195d1c0)                          = 0x195d1c0
arch_prctl(ARCH_SET_FS, 0x195c880)      = 0
uname({sysname="Linux", nodename="ReDiBook2", ...}) = 0
readlink("/proc/self/exe", "/home/redi/uni/uebung6/hello-wor"..., 4096) = 34
brk(0x197e1c0)                          = 0x197e1c0
brk(0x197f000)                          = 0x197f000
fstat(1, {st_mode=S_IFCHR|0660, st_rdev=makedev(0x4, 0x1), ...}) = 0
ioctl(1, TCGETS, {B38400 opost isig icanon echo ...}) = 0
write(1, "Hello, World\n", 13Hello, World
)          = 13
exit_group(0)                           = ?
+++ exited with 0 +++
# execve("./hello-world", ["./hello-world"], 0x7fffe425b690 /* 20 vars */) = 0
# wird zum starten verwendet
$ strace -o hello-world-strace.txt ./hello-world
Hello, World
$ cat hello-world-strace.txt
execve("./hello-world", ["./hello-world"], 0x7fffc6cb20c0 /* 20 vars */) = 0
arch_prctl(0x3001 /* ARCH_??? */, 0x7fffd2840640) = -1 EINVAL (Invalid argument)
brk(NULL)                               = 0xd04000
brk(0xd051c0)                           = 0xd051c0
arch_prctl(ARCH_SET_FS, 0xd04880)       = 0
uname({sysname="Linux", nodename="ReDiBook2", ...}) = 0
readlink("/proc/self/exe", "/home/redi/uni/uebung6/hello-wor"..., 4096) = 34
brk(0xd261c0)                           = 0xd261c0
brk(0xd27000)                           = 0xd27000
fstat(1, {st_mode=S_IFCHR|0660, st_rdev=makedev(0x4, 0x1), ...}) = 0
ioctl(1, TCGETS, {B38400 opost isig icanon echo ...}) = 0
write(1, "Hello, World\n", 13)          = 13
exit_group(0)                           = ?
+++ exited with 0 +++
```
b) Mit welchem Systemaufruf wird eine Zeichenkette auf dem Bildschirm
ausgegeben? Was bedeuten die 3 Parameter von diesem Systemaufruf?
```bash
write(1, "Hello, World\n", 13Hello, World
)          = 13
# es ist: write(output channel, output string, string length raw string) = string length
```

c) Laden Sie sich aus Moodle das statisch kopilierte Programm uebung6-raetsel
herunter und führen Sie es aus. Leider gibt das Programm ein Fehler aus und
die Fehlermeldung ist nicht gerade aussagekräftig. Finden Sie heraus warum
das Programm einen Fehler ausgibt. Wie könnte man das Problem möglichst
einfach beheben?
```bash
$ chmod +x uebung6-raetsel
$ ./uebung6-raetsel
ERROR!
$ strace ./uebung6-raetsel
execve("./uebung6-raetsel", ["./uebung6-raetsel"], 0x7fffd5ae6440 /* 20 vars */) = 0
brk(NULL)                               = 0x7fffdb10d000
access("/etc/ld.so.preload", R_OK)      = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/etc/ld.so.cache", O_RDONLY|O_CLOEXEC) = 3
fstat(3, {st_mode=S_IFREG|0644, st_size=60478, ...}) = 0
mmap(NULL, 60478, PROT_READ, MAP_PRIVATE, 3, 0) = 0x7fcc9d3e1000
close(3)                                = 0
openat(AT_FDCWD, "/lib/x86_64-linux-gnu/libc.so.6", O_RDONLY|O_CLOEXEC) = 3
read(3, "\177ELF\2\1\1\3\0\0\0\0\0\0\0\0\3\0>\0\1\0\0\0\260A\2\0\0\0\0\0"..., 832) = 832
fstat(3, {st_mode=S_IFREG|0755, st_size=1824496, ...}) = 0
mmap(NULL, 8192, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0x7fcc9d3d0000
mmap(NULL, 1837056, PROT_READ, MAP_PRIVATE|MAP_DENYWRITE, 3, 0) = 0x7fcc9d200000
mprotect(0x7fcc9d222000, 1658880, PROT_NONE) = 0
mmap(0x7fcc9d222000, 1343488, PROT_READ|PROT_EXEC, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x22000) = 0x7fcc9d222000
mmap(0x7fcc9d36a000, 311296, PROT_READ, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x16a000) = 0x7fcc9d36a000
mmap(0x7fcc9d3b7000, 24576, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x1b6000) = 0x7fcc9d3b7000
mmap(0x7fcc9d3bd000, 14336, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_ANONYMOUS, -1, 0) = 0x7fcc9d3bd000
close(3)                                = 0
arch_prctl(ARCH_SET_FS, 0x7fcc9d3d1500) = 0
mprotect(0x7fcc9d3b7000, 16384, PROT_READ) = 0
mprotect(0x7fcc9d421000, 4096, PROT_READ) = 0
mprotect(0x7fcc9d417000, 4096, PROT_READ) = 0
munmap(0x7fcc9d3e1000, 60478)           = 0
brk(NULL)                               = 0x7fffdb10d000
brk(0x7fffdb12e000)                     = 0x7fffdb12e000
openat(AT_FDCWD, "/tmp/betriebssysteme1-sose-2020.txt", O_RDONLY) = -1 ENOENT (No such file or directory)
fstat(1, {st_mode=S_IFCHR|0660, st_rdev=makedev(0x4, 0x1), ...}) = 0
ioctl(1, TCGETS, {B38400 opost isig icanon echo ...}) = 0
write(1, "ERROR!\n", 7ERROR!
)                 = 7
exit_group(1)                           = ?
+++ exited with 1 +++

# meine Lösung:
$ touch /tmp/betriebssysteme1-sose-2020.txt
$ ./uebung6-raetsel
Sie haben das Rätsel erfolgreich gelöst! Glückwunsch!
```

d) Installieren Sie sysdig auf die virtuelle Maschine, falls es noch nicht installiert
ist. Was ist der Unterschied zwischen strace und sysdig?
```bash
# wird verschoben, da ich sysdig nicht installieren kann
```

a) Starten Sie sysdig und filtern Sie die Ausgabe auf den Systemaufruf
chdir. Öffnen Sie ein weiteres Terminal und wechseln Sie das Verzeichnis. Was sehen Sie in der Ausgabe von sysdig?
```bash
# wird verschoben, da ich sysdig nicht installieren kann
```

# Übung 6.2: Prozesse

## Grundlegendes

a) Unter Linux sind viele Prozesse zur gleichen Zeit gestartet. Wie kann man
die Prozesse eindeutig unterscheiden?

```bash
# anhand der PID (Prozess ID)
```
b) Wenn der Computer oder die virtuelle Maschine gestartet werden, wird ein
Prozess als Erstes gestartet. Was ist das für ein Prozess und was ist dessen
Aufgabe? Wie heißt der Prozess konkret bei aktuellen Linux-Distributionen?
```bash
# PID 1 ist der init prozess. Er startet (bzw initialisiert) alle anderen Prozesse auf dem System.
```

## Prozesse Kommandos

a) Ihr Systemadministrator fragt Sie bitte alle Ihre laufenden Prozesse zu schicken.
Welches Kommando würde das erledigen?
```bash
$ ps ux
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
redi         7  0.0  0.0  18352  5680 tty1     S    14:07   0:00 -bash
redi      4147  0.0  0.0  16640  1776 tty1     R    14:48   0:00 ps ux
```

b) Mit welchem Kommando kann man alle auf dem System laufenden Prozesse
anzeigen, unabhängig von dem Benutzer?
```bash
$ ps aux
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.0  0.0   8936   312 ?        Ssl  14:07   0:00 /init
root         6  0.0  0.0   8940   228 tty1     Ss   14:07   0:00 /init
redi         7  0.0  0.0  18352  5680 tty1     S    14:07   0:00 -bash
root       406  0.0  0.0  19816  1116 ?        Ss   14:15   0:00 /usr/sbin/sshd
redi      4140  0.0  0.0  16640  1780 tty1     R    14:47   0:00 ps aux
```

c) Was zeigt Ihnen das Kommando pstree an?
```bash
$ pstree
init─┬─init───bash───pstree
     ├─sshd
     └─{init}
# ich würde behaupten, wir sehen die prozess call liste (wer welchen prozess aufgerufen hat). In meinem fall hat die init die prozess init aufgerufen, die bash aufruft in der ich dann pstree aufgerufen habe. in den nächsten spalten sieht man dann die services und wahrscheinlich was die dann aufrufen
```

d) Geben Sie sleep 5 in Ihr Terminal ein und warten Sie bis die 5 Sekunden
abgelaufen sind. Geben Sie nun sleep 5 & ein. Was hat sich geändert?
```bash
$ sleep 5
$ sleep 5 &
[1] 4150
# beim 2ten aufruf wird das der prozess in den Hintergrund geschoben.
```

e) Erhöhen Sie nun die Wartezeit auf 10 und starten Sie den Prozess wieder in
den Hintergrund. Geben Sie jetzt fg ein. Was ist nun passiert?
```bash
$ sleep 10 &
[2] 4151
[1]   Done                    sleep 5
$ fg
sleep 10
# Ich sehe die Liste der Prozesse, die im hintergrund läuft inkl. der PIDs (bzw. Done wenn der Prozess fertig ist) und ggf. die kommandos.
# mit fg schiebe ich alles in den vordergrund. jetzt muss ich die 10 sec warten
```

f) Öffnen Sie ein Terminal und starten Sie das Programm htop. Öffnen Sie nun
ein weiteres Terminal und versuchen heraus zu finden welche PID das Programm htop aktuell hat.
```bash
$ htop
$ ps -C htop
  PID TTY          TIME CMD
 4344 tty1     00:00:00 htop
# 4344 ist die aktuelle PID
```

a) Nutzen Sie das Programm kill um den Prozess zu beenden.
```bash
$ kill 4344
```

g) Recherchieren Sie was unter Linux Signale sind und was haben die mit dem
Befehl kill zu tun?
```bash
$ man 7 signal
First the signals described in the original POSIX.1-1990 standard.

   Signal     Value     Action   Comment
   ──────────────────────────────────────────────────────────────────────
   SIGHUP        1       Term    Hangup detected on controlling terminal
                                 or death of controlling process
   SIGINT        2       Term    Interrupt from keyboard
   SIGQUIT       3       Core    Quit from keyboard
   SIGILL        4       Core    Illegal Instruction
   SIGABRT       6       Core    Abort signal from abort(3)
   SIGFPE        8       Core    Floating point exception
   SIGKILL       9       Term    Kill signal
   SIGSEGV      11       Core    Invalid memory reference
   SIGPIPE      13       Term    Broken pipe: write to pipe with no
                                 readers
   SIGALRM      14       Term    Timer signal from alarm(2)
   SIGTERM      15       Term    Termination signal
   SIGUSR1   30,10,16    Term    User-defined signal 1
   SIGUSR2   31,12,17    Term    User-defined signal 2
   SIGCHLD   20,17,18    Ign     Child stopped or terminated
   SIGCONT   19,18,25    Cont    Continue if stopped
   SIGSTOP   17,19,23    Stop    Stop process
   SIGTSTP   18,20,24    Stop    Stop typed at terminal
   SIGTTIN   21,21,26    Stop    Terminal input for background process
   SIGTTOU   22,22,27    Stop    Terminal output for background process
# .... man kann damit das killen eines prozesses erzwingen
```

h) Ein Linux-Prozess hat ein Nice-Wert von 19. Wird es damit mehr Ressourcen
bekommen als die anderen Prozesse?
```bash
# nein. je höher (von -20 bis 19), desto weniger priorität bekommt der prozess. und somit bekommt es weniger Ressourcen als andere
```
i) Welcher Nice-Wert wird standardmäßig unter Linux vergeben?
```bash
# standard ist 0
```

j) Starten Sie nochmal in einem Terminal htop und ändern Sie den Nice-Wert
von dem laufenden Programm auf -20. Welches Kommando ist dafür notwendig?
```bash
$ sudo renice -20 {pid}
```