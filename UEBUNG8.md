# Übung 8.1: Scheduling für Multiprozessor- und Echtzeit-Systeme
a) Welcher Scheduling-Algorithmus wird in fast allen Desktop-Betriebssysteme
(z.B. Windows, MacOS und Linux) eingesetzt?
```
MFQ
```

b) Erklären Sie wie ein Spinlock funktioniert?
```
Mechanismus zur Prozesssynchronisierung.
Ein Spinlock sperrt eine Datei für weitere Aufrufe, sobald auf diese zugegriffen wurde. Das dient dem Datenverlust, da sonst 2 oder mehr Prozesse die Datei gleichzeitig überschreiben würden. (Aktives warten)
Atomare Operation (spezielle variablen typen)
```

c) Was besagt das Mooresches Gesetz und wie ist aktuell die Entwicklung?
```
Mooresches Gesetz besagt, dass die Entwicklung der Rechenleistung in einem bestimmten Intervall verdoppelt. Aktuell kann man aber belegen, dass dieser Anstieg nicht mehr so ist. Daher stirbt dieses Gesetz langsam aus. (Siehe z.B. 30er Serie von NVidia)
Aktuelle Entwicklung: Mehr Kerne in Prozessoren statt mehr Leistung pro Kern
```

d) Was ist der Unterschied zwischen präemptiver und nicht-präemptiver SchedulingAlgorithmen?
```
präemptive algorithmen können unterbrochen werden
nicht-präemptiver  algorithmen können nicht unterbrochen werden
```

e) Welche zwei grundsätzlichen Kategorien gibt es für Echtzeit Scheduler?
```
Online (dynamische priorität) und Offline (statische priorität) Scheduler.
Offline: kennen die Ausführzeit jedes prozesses vor der Ausführung und können sie so Priorisieren.
Online: können Priorisierung dynamisch anpassen um eine höhere Auslasung zu generieren.
```

f) Zeichnen Sie ein Task-Zeit-Diagramm (0–24) für Rate Monotonic Scheduling
(RMS) und berechnen Sie die Auslastung des Prozessors für die folgenden
Prozessinformationen:

| Task | Release (r) | Execution (e) | Deadline (d) | Period (p) |
| --- | --- | --- | --- | --- |
| t1 | 0 | 2 | 6 | 6 |
| t2 | 0 | 1 | 5 | 5 |
| t3 | 0 | 3 | 10 | 10 |
```
t1 _##___##____##____##____
t2 #____#____#____#____#___
t3 ___##___#__#__#_#____###

(2÷6)+(1÷5)+(3÷10)=0,83333333333333333333333333333333
```

g) Zeichnen Sie ein Task-Zeit-Diagramm (0–20) für Earliest Deadline First (EDF)
und Least Laxity First (LLF) für die nachfolgenden Prozessinformationen.

| Task | Release (r) | Execution (e) | Deadline (d) | Period (p) |
| --- | --- | --- | --- | --- |
| t1 | 0 | 1 | 3 | 3 |
| t2 | 0 | 1 | 4 | 4 |
| t3 | 0 | 2 | 5 | 5 |
```
EDF
t1 #___#_#___#__#_#___#
t2 _#___#___#____#_#___
t3 __##___##__##____##_

LLF
t1 #___#_#___#__#_#___#
t2 _#___#___#____#___#_
t3 __##___##__##___##__
```
