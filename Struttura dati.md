Esistono diversi modi di organizzare e memorizzare dati nel computer.
Una struttura dati è una collezione di dati strutturata e organizzata in un modo preciso a cui sono associate operazioni.
- diverse strutture dati memorizzano e organizzano i dati in modi diversi
- descriveremo l'efficienza di strutture dati in base a due caratteristiche: Spazio e Tempo richiesto

Ogni struttura dati ha vantaggi e svantaggi.
Non c'è una struttura dati migliore dell'altra in tutto e per tutto, quelle che hanno prestazioni peggiori non vengono più utilizzate.
- [[Elementari]]
- [[Complesse]]

## Selezionare una struttura dati:
Per risolvere efficientemente un problema bisogna trovare la struttura dati migliore per il contesto:
1. Analizza il problema per determinare le operazioni di base che vanno supportate. (inserire, eliminare, ordinare, trovare dati nella struttura dati)
2. Quantifica i limiti di risorse obiettivi per ogni operazione.
3. Seleziona la struttura dati che rientra meglio nelle condizioni.

è un approccio dato-centrico.

è bene rispondere a queste domande durante la scelta della struttura dato:
1.  I dati sono inseriti:
	Tutti all'inizio → applicazione statica
	Alcuni sono inseriti durante le applicazioni
2.  C'è bisogno di cancellare dati? 
3. I dati sono processati:
	In ordine predefinito 
	è possibile cancellare alcuni dati specifici

#cpp
## Tecniche di rappresentazione di dati:
Un tipo dato ha una forma logica e una fisica:
- **Logica**: Un Abstract Data Type (ADT) è il tipo dato con i suoi metodi, senza la specifica di come andrà fatta l'implementazione. per un ADT esistono diverse implementazioni, ottimali e non
- **Fisica**: implementazione del tipo dato come struttura dati

A data structure is the implementation for an ADT 
- ADT + implementation → class
- each operation of ADT → method
- Object → instance of class, something that is created and takes up storage during the execution of a program
