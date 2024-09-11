# Speicherorganisation eines Prozesses

Wenn ein Programm auf einem Computer läuft, wird es als **Prozess** ausgeführt. Der Computer kann mehrere Prozesse gleichzeitig ausführen, wechselt jedoch sehr schnell zwischen ihnen, was als **Kontextwechsel** bezeichnet wird. Der Speicher eines Prozesses ist in verschiedene Bereiche aufgeteilt, die unterschiedliche Aufgaben erfüllen:

## 1. Prozess und Kontextwechsel

- **Prozess:** Eine laufende Instanz eines Programms. 
- **Kontextwechsel:** Der Computer wechselt blitzschnell zwischen Prozessen, um den Eindruck zu erwecken, dass mehrere Prozesse gleichzeitig laufen. Dabei wird der Zustand eines Prozesses gespeichert, damit er später an derselben Stelle fortgesetzt werden kann.

**Beispiel:** Wenn du mehrere Aufgaben gleichzeitig erledigst (E-Mails schreiben, Nachrichten lesen, Excel-Berechnungen), wechselst du zwischen diesen Aufgaben und speicherst jeweils den aktuellen Stand.

## 2. Speicheraufteilung eines Prozesses

Der Speicher eines Prozesses ist in verschiedene Bereiche aufgeteilt:

### a) User Stack

- Der **User Stack** speichert wichtige Informationen wie:
  - **Program Counter:** Zeigt an, welche Anweisung im Programm gerade ausgeführt wird.
  - **Register:** Kleine Speicherplätze im Prozessor für temporäre Daten.

Der Stack wächst typischerweise "nach unten" im Speicher, d.h., er nutzt den unbenutzten Speicher darunter.

**Beispiel:** Ein Spiel speichert deinen Fortschritt an einem Checkpoint. Ähnlich speichert der Stack den aktuellen Zustand des Programms.

### b) Shared Library Regions

- Diese Bereiche enthalten **Bibliotheken**, die vom Programm benötigt werden. Bibliotheken sind Sammlungen von Funktionen, die das Programm nutzt, ohne dass es diese selbst programmieren muss. Sie können entweder statisch oder dynamisch eingebunden werden.

**Beispiel:** Ein Programm verwendet eine Bibliothek, um eine Datei zu öffnen, anstatt die Funktion selbst zu programmieren.

### c) Heap

- Der **Heap** ist der Speicherbereich, der dynamisch wächst und schrumpft, wenn das Programm Speicher anfordert oder freigibt. 

**Beispiel:** Ein Bildbearbeitungsprogramm vergrößert den Heap, wenn du ein Bild lädst.

### d) Programmcode und Daten

- Dieser Bereich enthält den **Code des Programms** (die auszuführenden Befehle) und **initialisierte Variablen**, die vom Programm benötigt werden.

**Beispiel:** Der Code, der die Berechnungen in einem Taschenrechner ausführt, befindet sich hier, ebenso wie Variablen wie „Ergebnis = 0“.

## Zusammenfassung

- Der **Prozess** ist eine laufende Instanz eines Programms.
- Der **Kontextwechsel** ermöglicht es dem Computer, schnell zwischen Prozessen zu wechseln.
- Der Speicher eines Prozesses ist aufgeteilt in:
  - **User Stack:** Temporäre Speicherung von Informationen.
  - **Shared Library Regions:** Bibliotheken, die vom Programm genutzt werden.
  - **Heap:** Dynamische Speicheranpassung.
  - **Programmcode und Daten:** Code und initialisierte Variablen des Programms.

Das Verständnis dieser Bereiche hilft bei der Analyse von Sicherheitsproblemen wie **Buffer Overflows**, bei denen zu viele Daten in den Speicher geschrieben werden, was zu Sicherheitsrisiken führen kann.


# Stack (Stapel)

Der Stack ist eine spezielle Art von Speicher, der in der Programmierung verwendet wird. Man kann ihn sich wie einen Stapel von Karten vorstellen, bei dem immer nur die oberste Karte sichtbar und zugänglich ist.

- **Top of the Stack**: Das ist die oberste Karte auf dem Stapel, also die zuletzt hinzugefügte. Im Speicher ist das die Adresse mit dem niedrigsten Wert, da der Stack von oben nach unten wächst.

- **Wachstumsrichtung**: Der Stack wächst, wenn neue Daten hinzugefügt werden, in Richtung niedrigere Speicheradressen. Das bedeutet, dass neue Daten "oben" auf dem Stapel platziert werden, was in der Praxis zu niedrigeren Adressen im Speicher führt.

## Operationen des Stacks

1. **Pushing (Hinzufügen)**
   - **Was ist das?**: Beim Pushen wird eine neue Information oben auf den Stack gelegt. Man kann sich das wie das Hinzufügen einer neuen Karte oben auf den Kartenstapel vorstellen.
   - **Beispiel**: Angenommen, du speicherst einen Wert `42` auf dem Stack. Der Stack, der vorher leer war, sieht nun so aus:
     ```plaintext
     [42]
     ```

2. **Popping (Entfernen)**
   - **Was ist das?**: Beim Poppen wird die oberste Information vom Stack entfernt. Das ist wie das Entfernen der obersten Karte von einem Stapel.
   - **Beispiel**: Wenn du die Karte `42` entfernst, bleibt der Stack leer:
     ```plaintext
     (leer)
     ```

## Beispiel im Programmierkontext

Stellen wir uns vor, du hast eine Funktion `foo()` und eine Funktion `bar()`. Wenn `foo()` `bar()` aufruft, wird die Information, wo das Programm nach dem Abschluss von `bar()` fortfahren soll, auf den Stack gelegt. Das ist wichtig, weil der Stack speichert, welche Funktion gerade aktiv ist und wo die Ausführung wieder hinführen soll, nachdem die Funktion beendet ist.

Hier ist ein einfaches Beispiel:

1. **Aufruf von `foo()`**:
   - Der Stack wird jetzt Informationen über den Aufruf von `foo()` enthalten.

2. **Innerhalb von `foo()` wird `bar()` aufgerufen**:
   - Der Stack speichert, dass `bar()` jetzt ausgeführt wird. Der Rücksprungpunkt von `bar()` nach `foo()` wird ebenfalls gespeichert.

3. **`bar()` beendet seine Ausführung**:
   - Der Stack wird jetzt 


Sicher! Hier ist eine Erklärung der Schlüsselkonzepte aus deiner Auswahl in einfacher Sprache:

---

### **Stack und Stack Pointer (rsp)**

Der **Stack** ist ein Bereich im Speicher, der wie ein Stapel von Platten funktioniert. Er wird genutzt, um Daten temporär zu speichern, z.B. beim Aufruf von Funktionen oder bei der Speicherung von Variablen. Der **Stack Pointer** (`rsp` in der x86-64 Architektur) zeigt auf die oberste Platte des Stapels, also den aktuell höchsten Speicherort.

### **push var**

Die **`push`**-Anweisung wird verwendet, um einen Wert auf den Stack zu legen. Hier ist, was passiert:

1. **Wert speichern:** Der Wert, der in der Variable `var` gespeichert ist, wird auf dem Stack abgelegt.
2. **Stack Pointer anpassen:** Der Stack Pointer (`rsp`) wird um 8 Byte verringert, weil in der x86-64 Architektur der Stack in 8-Byte-Schritten wächst.
3. **Wert schreiben:** Der Wert wird an der neuen Position des Stack Pointers (also oben auf dem Stack) abgelegt.

**Beispiel:**

Angenommen, der Stack Pointer zeigt auf die Speicheradresse `0x7fffffffe000`. Wenn wir `push 10` ausführen, wird:

- Der Stack Pointer auf `0x7fffffffdff8` verringert.
- Der Wert `10` wird an dieser neuen Adresse (`0x7fffffffdff8`) gespeichert.

### **pop var**

Die **`pop`**-Anweisung wird verwendet, um den obersten Wert vom Stack zu entfernen und ihn in eine Variable zu speichern. Hier ist, was passiert:

1. **Wert lesen:** Der Wert, der an der Adresse gespeichert ist, auf die der Stack Pointer (`rsp`) zeigt, wird gelesen.
2. **Wert speichern:** Der gelesene Wert wird in der Variablen `var` gespeichert.
3. **Stack Pointer anpassen:** Der Stack Pointer wird um 8 Byte erhöht, um die oberste Platte des Stapels zu entfernen.

**Beispiel:**

Angenommen, der Stack Pointer zeigt auf die Adresse `0x7fffffffdff8`, wo der Wert `10` gespeichert ist. Wenn wir `pop var` ausführen:

- Der Wert `10` wird aus der Adresse `0x7fffffffdff8` gelesen und in `var` gespeichert.
- Der Stack Pointer wird auf `0x7fffffffe000` erhöht.

### **Stack Frames**

In Programmen, die mehrere Funktionen haben, wird für jede Funktion ein eigener **Stack Frame** erstellt. Dies ist wie ein separater Abschnitt des Stacks für jede Funktion:

- **Stack Frame:** Dieser Bereich des Stacks wird verwendet, um lokale Variablen und Funktionsargumente zu speichern.
- **Zuweisung:** Ein neuer Stack Frame wird erstellt, wenn eine Funktion aufgerufen wird.
- **Freigabe:** Der Stack Frame wird freigegeben, wenn die Funktion beendet ist.

**Beispiel:**

```
int add(int a, int b){

   int new = a + b;

   return new;

}


int calc(int a, int b){

   int final = add(a, b);

   return final;

}


calc(4, 5)
```



## Schlüsselkonzepte in der Funktionsaufruf- und Rückkehrlogik

### 1. Funktionsaufruf und Rückkehr

#### **Funktionsaufruf**

- **Aufruf einer Funktion**: Wenn eine Funktion aufgerufen wird (z.B. `add`), speichert der Prozessor die Adresse der nächsten Anweisung (nach dem Funktionsaufruf) auf dem Stack. Diese Adresse wird benötigt, um nach der Beendigung der Funktion zum richtigen Punkt zurückzukehren.
- **Stack-Frame**: Der Prozessor erstellt einen neuen „Stack-Frame“ für die aufgerufene Funktion (`add`). Dies ist ein Bereich auf dem Stack, in dem die Funktion ihre lokalen Variablen speichert.

  **Beispiel**:
  ```assembly
  callq sym.add
  ```
  Wenn dies in `calc` steht, wird die Adresse der nächsten Zeile (nach `callq`) auf den Stack gelegt und der Code springt zur `add`-Funktion.

#### **Rückkehr aus einer Funktion**

- **Beenden der Funktion**: Wenn die Funktion `add` fertig ist, verwendet sie den Befehl `retq` (Return), um zur Adresse zurückzukehren, die zuvor auf den Stack gelegt wurde. Diese Adresse ist der Punkt, an dem die Funktion `calc` nach dem Funktionsaufruf weitermachen soll.
- **Wiederherstellung des Stacks**: Nach dem Rücksprung wird der Stack-Frame für `add` entfernt und der Prozessor stellt die Register und den Stack-Zustand wieder her, wie sie vor dem Funktionsaufruf waren.

  **Beispiel**:
  ```assembly
  retq
  ```
  Dieser Befehl holt die Rücksprungadresse vom Stack und springt zu dieser Adresse zurück.

### 2. Register und Argumente

- **Register für Argumente**: Wenn eine Funktion Argumente erhält, werden diese in bestimmten Registern gespeichert. In der x86-64 Architektur sind das: `rdi`, `rsi`, `rdx`, `rcx`, `r8`, und `r9`. Diese Register können bis zu 6 Argumente speichern.
- **Return-Wert**: Der Register `rax` wird verwendet, um Rückgabewerte von Funktionen zu speichern.

  **Beispiel**:
  Wenn du eine Funktion `add(a, b)` aufrufst, könnte `a` in `rdi` und `b` in `rsi` gespeichert werden.

### 3. Speichern von Registerwerten

- **Caller-Saved und Callee-Saved**: 
  - **Caller-Saved Register**: Register, die von der aufrufenden Funktion (`calc`) verwendet werden und später wieder benötigt werden, müssen gesichert werden. Die Funktion, die aufgerufen wird, kann diese Register ändern, daher müssen sie von der aufrufenden Funktion gesichert werden. Zu den caller-saved Registern gehören `rax`, `r10`, `r11`.
  - **Callee-Saved Register**: Register wie `rbx`, `r12`, `r13`, `r14` und `rbp` werden von der aufgerufenen Funktion (`add`) gesichert und wiederhergestellt. Das bedeutet, dass `add` sicherstellen muss, dass die Werte in diesen Registern am Ende der Funktion unverändert sind.

  **Beispiel**:
  Wenn `calc` vor dem Funktionsaufruf Register `rax` verwendet, sollte `calc` den Wert von `rax` auf dem Stack speichern und nach dem Rücksprung wiederherstellen.

### Zusammenfassung

1. **Funktionsaufruf**: Die Adresse der nächsten Zeile wird auf dem Stack gespeichert, und ein neuer Stack-Frame wird erstellt.
2. **Funktionsrückkehr**: Die Rücksprungadresse wird vom Stack geholt und der Stack-Frame der Funktion wird entfernt.
3. **Argumente und Register**: Argumente werden in spezifischen Registern gespeichert und Rückgabewerte in `rax`. Register, die von der aufgerufenen Funktion geändert werden können, müssen von der aufrufenden Funktion gesichert werden.

Diese Konzepte sind wichtig, um zu verstehen, wie Funktionen im Speicher verwaltet werden und wie man sicherstellen kann, dass Werte nicht überschrieben werden.


# Endianess

**Endianess** beschreibt die Reihenfolge, in der mehrere Bytes (also 8-Bit-Einheiten) eines mehrbyteigen Datenwertes in der Computer-Speicherordnung abgelegt werden. Verschiedene Computerarchitekturen können unterschiedliche Methoden verwenden, um diese Bytes zu speichern, was zu den Begriffen **Little Endian** und **Big Endian** führt.

### Little Endian

In **Little Endian**-Systemen wird der **weniger bedeutende Byte** (Least Significant Byte, LSB) zuerst gespeichert. Das bedeutet, die kleineren Teile des Wertes kommen zuerst im Speicher, während die größeren Teile später gespeichert werden.

**Beispiel:**

Nehmen wir den Wert `0x12345678`. Hier ist `0x78` der weniger bedeutende Teil (Least Significant Byte), und `0x12` ist der bedeutendste Teil (Most Significant Byte).

In einem Little Endian-System wird dieser Wert so gespeichert:

- `0x78` (erstes Byte)
- `0x56` (zweites Byte)
- `0x34` (drittes Byte)
- `0x12` (viertes Byte)

Also im Speicher: `78 56 34 12`.

### Big Endian

In **Big Endian**-Systemen wird der **bedeutendste Byte** (Most Significant Byte, MSB) zuerst gespeichert. Das bedeutet, die größeren Teile des Wertes kommen zuerst im Speicher, während die kleineren Teile später gespeichert werden.

**Beispiel:**

Für den Wert `0x12345678` wird dieser so gespeichert:

- `0x12` (erstes Byte, Most Significant Byte)
- `0x34` (zweites Byte)
- `0x56` (drittes Byte)
- `0x78` (viertes Byte, Least Significant Byte)

Also im Speicher: `12 34 56 78`.

### Zusammenfassung

- **Little Endian**: Die Bytes werden in der Reihenfolge vom wenig bedeutendsten zum bedeutendsten Byte gespeichert.
- **Big Endian**: Die Bytes werden in der Reihenfolge vom bedeutendsten zum wenig bedeutendsten Byte gespeichert.

Die Wahl der Endianess beeinflusst, wie ein Wert im Speicher gelesen und interpretiert wird. Dies kann insbesondere bei der Datenübertragung zwischen Systemen mit unterschiedlicher Endianess zu Problemen führen, weshalb oft eine Endianess-Konversion notwendig ist.
