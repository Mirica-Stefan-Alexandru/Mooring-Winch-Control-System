# Sistem de Control Mooring Winch (Troliu de Amarare)

Proiect de automatizare realizat in Siemens TIA Portal V18 pentru controlul unui troliu de amarare (Mooring Winch) bazat pe un PLC Siemens S7-1200 si o interfata HMI WinCC.

Sistemul asigura controlul complet al motorului, achizitia semnalelor analogice, moduri de operare avansate (Auto-Tensionare), protectii avansate la suprasarcina si diagnoza in timp real pentru operatiuni marine in conditii de siguranta.

---

## Functionalitati Principale

### 1. Achizitie si Scalare Semnale Analogice
* **Control Joystick:** Preluare intrare si scalare in procentaj de comanda (`-100.0%` .. `100.0%`) cu filtru de zona moarta (Deadband) pentru eliminarea oscilatiilor mecanice.
* **Masurare Tensiune Cablu:** Preluare semnal Load Cell si scalare in forta reala (`0` .. `100 kN`).
* **Masurare Lungime Cablu:** Monitorizarea si calcularea lungimii de cablu derulat (Payout Length).

### 2. Logica de Control Motor & Moduri de Operare
* **Comanda de Baza (Manual):** Start/Stop cu auto-mentinere, determinare automata a sensului de rotatie decuplata de joystick (bazata pe rampa) si interblocaje directionale de siguranta.
* **Management Viteza:** Calcularea referintei de viteza (`0` .. `120 mpm`) cu implementarea rampelor programabile de accelerare si decelerare (`RampFunction_DB`).
* **Auto-Tensionare (Constant Tension):** Sistem in bucla inchisa care mentine automat tensiunea in parama la un Setpoint definit de operator (Vinciul trage/elibereaza automat).
* **Control Cinematic:** Masina de stari (State Machine) pentru tranzitii sigure intre modurile Manual/Auto si comanda interblocata a ambreiajului (Clutch).

### 3. Siguranta, Sarcina si ERS (Emergency Release)
* **Selectie Cablu:** Limitarea dinamica a tensiunii si a vitezei maxime in functie de tipul, diametrul si forta maxima de rupere (MBL) a cablului utilizat.
* **Protectie la Supraturatie (SetSpeed):** La depasirea vitezei setate de operator, sistemul intrerupe comanda motorului (Over-speed Trip) si cupleaza instantaneu frana mecanica de siguranta.
* **Full Tension Release (ERS):** Sistem prioritar de urgenta pentru deblocarea instantanee a franei si fortarea motorului in pay-out rapid pentru a preveni ruperea cablului in caz de socuri extreme.

### 4. Interfata Operator (HMI WinCC)
* **Monitorizare & Operare:** Interfata simpla, moderna (tema Industrial Dark) cu afisaj clar pentru viteza, starea motorului, sageti directionale dinamice si parametrizare.
* **Auto-Testare (Commissioning):** Ecran dedicat pentru diagnoza, generare rampa simulata in PLC pentru joystick si validare status I/O fara actionare fizica.
* **Sistem Alarme (Discrete Alarms):** Bannere tip pop-up si istoric cu declansare pe baza de biti (Word structure) pentru Warning-uri (ex: Load Warning) si defectiuni critice (ex: Load Trip, Over-speed).

---

## Specificatii Tehnice

* **Hardware PLC:** Siemens S7-1200 (CPU 1217C DC/DC/DC)
* **Software:** Siemens TIA Portal V18
* **Limbaje de Programare:** SCL (Structured Control Language) / LAD
* **Arhitectura Codebase:** Data Blocks (DB) individuale, LGF (Library of General Functions), Standardizare Naming Convention (ENG).
* **Interfata Operator:** WinCC HMI Basic / Comfort Panel (Multi-screen Architecture)

---

>##  Integrare Industry 4.0 / IIoT (Post v1.0+)
>Incepand cu versiunile care vor urma lansarii de baza (v1.0+), arhitectura sistemului va face tranzitia catre paradigma **Industry 4.0 (Industrial Internet of Things)**. 
>Sistemul va fi extins cu module avansate de colectare si procesare a datelor (IT/OT), incluzand:
>*  **Integrare Node-RED:** Conectarea PLC-ului la fluxuri de date logice pentru comunicarea facila cu aplicatii de nivel superior.
>*  **Baze de Date in Timp Real:** Stocarea continua si securizata a tuturor parametrilor critici (tensiuni pe Load Cell, turatie, istoric declansari ERS).
>*  **Dashboard-uri Live & Grafice:** Construirea de platforme web centralizate pentru vizualizarea evolutiei masuratorilor sub forma de grafice in timp real.
>*  **Sistem de Detectie Preventiva (Mentenanta Predictiva):** Implementarea algoritmilor software capabili sa detecteze anomalii si uzuri (ex. uzura franei mecanice sau oboseala cablului) prin analizarea tiparelor din istoricul datelor, inainte de a se transforma in defectiuni fizice.

---
