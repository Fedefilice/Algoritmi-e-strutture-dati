Per confrontare l'efficienza di due algoritmi è necessario basarsi su un modello di calcolo astratto.

Tra quelli importanti, ma non più utilizzati ci sono:
- macchina di Turing
- macchina a registri (von Newman)
- macchina a puntatori

## Macchina di Turing - TM:
Ideata nel 1936 da Alan Turing.

è basata su due componenti:
- Nastro infinito
- Testina di lettura e scrittura

La TM si basa sul cambiamento di stato: dopo aver letto il contenuto della posizione corrente sul nastro, la macchina è in grado di cambiare stato (spostarsi L-R, scrivere, rimanere fermo)

Automa a stati finiti deterministico 
- stati finiti: ha azioni finite che puo compiere → spostarsi, scrivere
- deterministico: può compiere una sola azione alla volta

Automa più potente - Tesi di Church-Turing

Problemi: Troppo a basso livello, non realistica 

## Macchina di Von Newman:
1945, Von Newman. Anche detta macchina a registri.

Componenti:
- Unità di Input
- Unità di Output
- CPU - Central Processing Unit: elabora le istruzioni del programma
	CU - Control Unit
	ALU - Aritmethical Logical Unit
- Memoria: memorizza dati e programma 

Problemi: 
- assume algoritmi sequenziali deterministici
- assume una macchina che possa manipolare valori di dimensione qualsiasi in tempo costante
- la versione della memoria è piatta, non gerarchica