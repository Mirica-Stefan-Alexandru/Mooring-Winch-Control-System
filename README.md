# Sistem de Control Mooring Winch (Troliu de Amarare)

Proiect de automatizare realizat in Siemens TIA Portal V18 pentru controlul unui troliu de amarare (Mooring Winch) folosind un PLC S7-1200 si interfata HMI WinCC.

## Functionalitati principale:
* **Scalare semnale analogice:** Prelucrare intrari pentru Joystick (`IW2` -> -100..100%) si Celula de Sarcina / Load Cell (`IW0` -> 0..100 kN) folosind `NORM_X` si `SCALE_X`.
* **Procesare zona moarta (Deadband):** Filtrarea semnalului de la joystick pentru eliminarea oscilatiilor in pozitia neutra (-5%..5%).
* **Monitorizare praguri de siguranta:** Generare semnale de avertizare (`Limita_Warning` la 80 kN) si oprire de urgenta (`Limita_Trip` la 95 kN).
* **Control automat al tensiunii:** Reglare PID pentru mentinerea tensiunii constante in cablu.
