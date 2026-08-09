# Sistem de Control Mooring Winch (Troliu de Amarare)

Proiect de automatizare realizat in Siemens TIA Portal V18 pentru controlul unui troliu de amarare (Mooring Winch) bazat pe un PLC Siemens S7-1200 si o interfata HMI WinCC.

Sistemul asigura controlul complet al motorului, achizitia semnalelor analogice, protectii avansate la suprasarcina si diagnoza in timp real pentru operatiuni marine in conditii de siguranta.

---

## Functionalitati Principale

### 1. Achizitie si Scalare Semnale Analogice
* **Control Joystick:** Preluare intrare si scalare in procentaj de comanda (-100.0% .. 100.0%) cu filtru de zona moarta (Deadband) pentru eliminarea oscilatiilor mecanice.
* **Masurare Tensiune Cablu:** Preluare semnal Load Cell si scalare in forta reala (0 .. 100 kN).

### 2. Logica de Control Motor
* **Comanda de Baza:** Start/Stop cu auto-mentinere, determinare automata a sensului de rotatie (Tragere / Eliberare) si interblocaje directionale de siguranta.
* **Management Viteza:** Calcularea referintei de viteza (0..120 mpm) cu implementarea rampelor programabile de accelerare si decelerare.

### 3. Siguranta, Sarcina si ERS (Emergency Release)
* **Selectie Cablu:** Limitarea dinamica a tensiunii si a vitezei maxime in functie de tipul si diametrul cablului utilizat.
* **Protectie la Supraturatie (SetSpeed):** La depasirea vitezei setate de operator, sistemul intrerupe comanda motorului (Over-speed Trip) si cupleaza frana mecanica.
* **Full Tension Release (ERS):** Sistem de urgenta pentru deblocarea instantanee a franei (pay-out) pentru a preveni ruperea cablului in caz de socuri extreme.

### 4. Interfata Operator (HMI WinCC)
* **Monitorizare & Operare:** Interfata simpla, moderna cu afisaj clar pentru viteza, starea motorului, sageti directionale dinamice si parametrizare.
* **Auto-Testare (Commissioning):** Ecran dedicat pentru diagnoza, generare rampa simulata pentru joystick si validare status I/O fara actionare fizica.
* **Sistem Alarme:** Bannere tip pop-up si istoric cu declansare pe baza de biti (Word structure) pentru Warning-uri si defectiuni critice.

---

## Specificatii Tehnice

* **Hardware PLC:** Siemens S7-1200 (CPU 1217C DC/DC/DC)
* **Software:** Siemens TIA Portal V18
* **Limbaje de Programare:** SCL (Structured Control Language) / LAD
* **Interfata Operator:** WinCC HMI Basic / Comfort Panel (Multi-screen Architecture)
