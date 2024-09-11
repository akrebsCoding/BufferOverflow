# CPU Architektur Übersicht

* CPU-Komponenten

    - Control Unit (Steuerwerk):
        Holt Anweisungen aus dem Hauptspeicher.
        Die Adresse der nächsten auszuführenden Anweisung wird im Register Instruction Pointer (IP) gespeichert.
            In 32-Bit-Systemen als EIP bezeichnet.
            In 64-Bit-Systemen als RIP bezeichnet.

    - Arithmetic Logic Unit (ALU):
        Führt die aus dem Speicher geholten Anweisungen aus.
        Die Ergebnisse werden in den Registern oder im Speicher abgelegt.

    - Registers (Register):
        Schneller Speicher innerhalb der CPU.
        Speichert wichtige Daten für den schnellen Zugriff und die Ausführung von Anweisungen.

* Speicher und I/O-Geräte

    - Memory (Hauptspeicher / RAM):
        Beinhaltet den Code und die Daten eines Programms.
        Der Code und die Daten werden beim Start eines Programms in den Speicher geladen.

    - I/O Devices (Ein-/Ausgabegeräte):
        Geräte, die mit dem Computer interagieren, wie Tastaturen, Mäuse, Bildschirme, Drucker, Festplatten und USB-Sticks.

* Ablauf der Programmausführung

    - Ein Programm wird in den Hauptspeicher geladen.
    - Die Steuerwerk holt eine Anweisung nach der anderen aus dem Speicher, gesteuert durch den Instruction Pointer.
    - Die ALU führt die Anweisung aus, und die Ergebnisse werden in Registern oder im Speicher abgelegt.

# Regsiter Übersicht


* Instruction Pointer (IP/EIP/RIP)
  - **Funktion**: Enthält die Adresse der nächsten auszuführenden Anweisung.
  - **Entwicklung**:
    - **Intel 8086**: 16-bit Register (IP)
    - **32-bit Systeme**: 32-bit Register (EIP)
    - **64-bit Systeme**: 64-bit Register (RIP)

* General-Purpose Registers (EAX/RAX, EBX/RBX, ECX/RCX, EDX/RDX, ESP/RSP, EBP/RBP, ESI/RSI, EDI/RDI, R8-R15)
    - **EAX/RAX (Accumulator Register)**:
      - **Verwendung**: Speichern von Ergebnissen arithmetischer Operationen.
      - **Adressierung**: 
        - EAX (32-bit), RAX (64-bit)
        - AX (16-bit), AL (8-bit niedrig), AH (8-bit hoch)
      
    - **EBX/RBX (Base Register)**:
      - **Verwendung**: Speichern der Basisadresse für Offsets.
      - **Adressierung**:
        - EBX (32-bit), RBX (64-bit)
        - BX (16-bit), BH (8-bit hoch), BL (8-bit niedrig)
      
    - **ECX/RCX (Counter Register)**:
      - **Verwendung**: Zähloperationen wie Schleifen.
      - **Adressierung**:
        - ECX (32-bit), RCX (64-bit)
        - CX (16-bit), CH (8-bit hoch), CL (8-bit niedrig)
      
    - **EDX/RDX (Data Register)**:
      - **Verwendung**: Multiplikations- und Divisionoperationen.
      - **Adressierung**:
        - EDX (32-bit), RDX (64-bit)
        - DX (16-bit), DH (8-bit hoch), DL (8-bit niedrig)
      
    - **ESP/RSP (Stack Pointer)**:
      - **Verwendung**: Zeigt auf das Ende des Stacks.
      - **Adressierung**: ESP (32-bit), RSP (64-bit)
      
    - **EBP/RBP (Base Pointer)**:
      - **Verwendung**: Zugriff auf über den Stack übergebene Parameter.
      - **Adressierung**: EBP (32-bit), RBP (64-bit)
      
    - **ESI/RSI (Source Index Register)**:
      - **Verwendung**: Stringoperationen, verwendet Offset mit dem Data Segment (DS).
      - **Adressierung**: ESI (32-bit), RSI (64-bit)
      
    - **EDI/RDI (Destination Index Register)**:
      - **Verwendung**: Stringoperationen, verwendet Offset mit dem Extra Segment (ES).
      - **Adressierung**: EDI (32-bit), RDI (64-bit)
      
    - **R8-R15**:
      - **Verwendung**: Allgemeine Register in 64-bit Systemen.
      - **Adressierung**:
        - R8 (64-bit), R8D (32-bit)
        - R8W (16-bit), R8B (8-bit)



    #### Status Flag Register (EFLAGS/RFLAGS)
    - **32-bit (EFLAGS)** für 32-bit-Systeme, **64-bit (RFLAGS)** für 64-bit-Systeme.
    - Enthält mehrere 1-bit Flags, die den Status einer ausgeführten Instruktion anzeigen.

    Wichtige Flags:
    - **Zero Flag (ZF)**: Setzt sich auf 1, wenn das Ergebnis der letzten Instruktion 0 war.
    - **Carry Flag (CF)**: Setzt sich auf 1, wenn das Ergebnis der letzten Instruktion zu groß oder zu klein für das Zielregister ist.
    - **Sign Flag (SF)**: Setzt sich auf 1, wenn das Ergebnis negativ ist (oder das höchstwertigste Bit = 1).
    - **Trap Flag (TF)**: Setzt sich auf 1, wenn der Prozessor im Debugging-Modus ist (Schritt-für-Schritt-Ausführung).

    #### Segmentregister
    - **Segmentregister** (16-bit) teilen den Speicher in verschiedene Abschnitte auf.

    Wichtige Register:
    - **Code Segment (CS)**: Zeigt auf den Code-Abschnitt im Speicher.
    - **Data Segment (DS)**: Zeigt auf den Daten-Abschnitt des Programms im Speicher.
    - **Stack Segment (SS)**: Zeigt auf den Stack des Programms im Speicher.
    - **Extra Segments (ES, FS, GS)**: Zeigen auf zusätzliche Datenabschnitte.

    #### Allgemeine Register
    - Register für Datenverarbeitung und Adressierung (z.B. **RAX**, **RBX**, **RCX**, etc.).
    - Registersätze variieren je nach Architektur (32-bit/64-bit).

    #### Überblick
    - **EFLAGS/RFLAGS**: Statusanzeige der CPU-Befehle.
    - **Segmentregister**: Organisation des Speichers in Abschnitte.
    - **Allgemeine Register**: Datenverarbeitung und Adressierung.


# Memory Übersicht

### Übersicht der Speicherseiten in einem Windows-Betriebssystem

Beim Laden eines Programms in den Speicher sieht das Programm eine abstrahierte Ansicht des Speichers, die auf seine spezifischen Bedürfnisse zugeschnitten ist. Die genaue Art und Weise, wie das Betriebssystem diese Abstraktion durchführt, wird hier nicht weiter vertieft. Stattdessen wird die Sichtweise des Programms auf den Speicher betrachtet, insbesondere relevant für die Reverse-Engineering von Malware.

#### Speicherabschnitte

1. **Code:**
   - **Inhalt:** Programmcode, der in der Textsektion einer Portable Executable (PE)-Datei gespeichert ist.
   - **Eigenschaften:** Enthält Anweisungen, die von der CPU ausgeführt werden. Dieser Bereich hat Ausführungsrechte.

2. **Data:**
   - **Inhalt:** Initialisierte Daten, die konstant bleiben und nicht verändert werden, wie globale Variablen.
   - **Eigenschaften:** Teil der PE-Datei, bleibt während der Programmausführung konstant.

3. **Heap:**
   - **Inhalt:** Dynamische Daten, die zur Laufzeit erstellt und gelöscht werden.
   - **Eigenschaften:** Speicher wird zur Laufzeit für Variablen zugewiesen und bei deren Löschung wieder freigegeben. Daher der Name „dynamischer Speicher“.

4. **Stack:**
   - **Inhalt:** Lokale Variablen, übergebene Argumente und Rücksprungadressen.
   - **Eigenschaften:** Wichtig für die Steuerflusskontrolle des Programms. Malware zielt häufig auf den Stack ab, um den Steuerfluss zu manipulieren.

Die Reihenfolge und Anordnung der Abschnitte können variieren, z.B. kann der Code-Bereich unter dem Data-Bereich liegen.

# STACK Layout

### Überblick: Der Stack in der x86-Architektur

Der Stack ist ein wichtiger Teil des Speichers eines Programms und speichert u. a. Argumente, lokale Variablen und den Kontrollfluss des Programms. Er arbeitet nach dem **LIFO-Prinzip** (Last In, First Out), bei dem das zuletzt gespeicherte Element zuerst wieder entnommen wird. Zwei CPU-Register verwalten den Stack:

- **Stack Pointer (ESP/RSP):** Zeigt auf das oberste Element des Stacks und passt sich bei jedem Push (Hinzufügen) oder Pop (Entfernen) an.
- **Base Pointer (EBP/RBP):** Bleibt innerhalb einer Funktion konstant und dient als Referenz für lokale Variablen und Argumente.

### Stack-Layout

1. **Old Base Pointer (EBP):** Speichert den Base Pointer der aufrufenden Funktion.
2. **Return-Adresse:** Zeigt auf die Adresse, zu der nach der Funktion zurückgekehrt wird.
3. **Argumente:** Werden auf den Stack gelegt, bevor die Funktion startet.

### Funktion Prolog & Epilog

- **Prolog:** 
  - Initialisiert den Stack für die Funktion.
  - Argumente, Return-Adresse und der alte Base Pointer werden auf den Stack gelegt.
  - Der Base Pointer wird auf den aktuellen Stack Pointer gesetzt.

- **Epilog:** 
  - Stellt die alte Umgebung wieder her, indem der alte Base Pointer und die Return-Adresse vom Stack geladen werden.
  
### Stack-Überlauf (Buffer Overflow)

Ein Stack-Buffer-Overflow überschreibt die Return-Adresse, um den Programmfluss zu kapern. Dies ist eine häufige Technik in der Malware-Analyse.
