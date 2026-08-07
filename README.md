# Sistem de Control Mooring Winch (Troliu de Amarare)

Proiect de automatizare realizat in Siemens TIA Portal V18 pentru controlul unui troliu de amarare (Mooring Winch) bazat pe un PLC Siemens S7-1200 si o interfata HMI WinCC.

Sistemul asigura controlul complet al motorului, achizitia semnalelor analogice, compensarea dinamica a sarcinii, protectii mecanice si monitorizare in timp real.

---

## Functionalitati Principale

### 1. Achizitie si Scalare Semnale Analogice
* **Control Joystick:** Preluare intrare `IW2` si scalare in procentaj de comanda (`-100.0%` .. `100.0%`) cu filtru de zona moarta (*Deadband* intre `-5%` si `5%`) pentru eliminarea oscilatiilor.
* **Măsurare Tensiune Cablu:** Preluare intrare Celula de Sarcina / Load Cell (`IW0`) si scalare in forta reala (`0` .. `100 kN`).

### 2. Logica de Control Motor
* **Comanda Baza:** Control Start / Stop si determinarea automata a sensului de rotatie (Tragere / Eliberare cablu) in functie de pozitia joystick-ului.
* **Management Viteza:** Profilare viteza din joystick cu rampe programabile de accelerare si decelerare pentru prevenirea socurilor mecanice.
* **Interblocaje:** Protectie la schimbarea brusca a sensului de mers fara oprire prealabila.

### 3. Protectie si Compensare Sarcina (Safety & Load)
* **Compensare Dinamica:** Ajustarea automata a vitezei maxime de tragere/eliberare in functie de greutatea masurata pe cablu (sarcina mare = viteza redusa).
* **Protectie la Supraturatie (SetSpeed):** Monitorizarea limitei de viteza sigure. La depasirea parametrului `SetSpeed`, se declanseaza oprirea automata a motorului (*Over-speed Trip*) si cuplarea imediata a franei mecanice de siguranta.
* **Praguri de Tensiune:** Generare semnale de avertizare (`Limita_Warning` la `80 kN`) si oprire de urgenta (`Limita_Trip` la `95 kN`).

### 4. Interfata Operator (HMI WinCC)
* **Ecran Monitorizare:** Afisare in timp real pentru viteza motorului, pozitia joystick-ului, tensiunea din cablu si starea franei.
* **Parametrizare:** Campuri numerice pentru ajustarea pragurilor de viteza (`SetSpeed`) de catre operator.
* **Sistem Alarme:** Banner si istoric de alarme pentru notificarea rapida a depasirilor de limite sau a validarilor de Trip/E-Stop.

---

## Specificatii Tehnice

* **Hardware PLC:** Siemens S7-1200 (CPU 1217C DC/DC/DC)
* **Software:** Siemens TIA Portal V18
* **Limbaje de Programare:** SCL / Ladder (LAD)
* **Interfata Operator:** WinCC HMI Basic / Comfort Panel
