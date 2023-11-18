Sequenza finita di istruzioni, ognuna con un significato chiaro e che possono essere eseguite in un lasso di tempo e una quantità di memoria definiti, atte a risolvere un problema.
Deve essere #Efficiente e #Efficace

Deve essere abbastanza preciso da essere capito dagli esseri umani.
Per un computer c'è la necessità di un programma, che è scritto in un linguaggio rigoroso.

- es. ricerca lineare: esamina gli elementi uno alla volta per trovare un elemento specifico 
- per strutture dati diverse possono essere necessari algoritmi risolutivi diversi

## Caratteristiche algoritmo:
### Efficacia:
Il problema deve essere risolto con successo
#Efficace

### Efficienza:
Capacità di risultare efficaci utilizzando il quantitativo di risorse minimo durante la soluzione del problema.

Le risorse critiche rispetto a cui si misura l'efficienza di un algoritmo sono:
- Tempo di esecuzione
- Memoria utilizzata

#### Soluzione efficiente:
- risolve il problema entro il budget di memoria e tempo prestabilito
- è più efficiente delle soluzioni già presenti

#### Perchè è importante:	
I computer stanno diventando sempre più potenti. Mentre questo accade, noi tentiamo di risolvere problemi più complessi che prima erano impossibili, perchè necessitavano di più potenza di calcolo. Problemi più complessi necessitano di più potenza di calcolo, il che necessita di programmi sempre più efficienti.

- analizzare l'efficienza di un programma
- Progettare algoritmi efficienti 
#Efficiente 

#### Speeding up a program by code tuning:
code tuning is optimizing a program to make it run faster or require less storage
- focus on the major time consuming parts of the code, a lot of times it comes from a better data structure or algorithm
- use special tools to gather timing statistics
- check if the optimizations improve the program

always tune the algorithm first and then the code

## Misurare l'efficienza di un algoritmo:
Per confrontare l'efficienza di due algoritmi è necessario basarsi su un modello di macchina astratta. [[Modelli di calcolo astratti]]
Utilizzeremo il modello basato sulla notazione asintotica

Per comparare l'efficienza due soluzioni di uno stesso problema, essi non possono essere scritti in linguaggio di programmazione e eseguiti perché:
- un programma potrebbe essere scritto in modo più efficiente dell'altro
- i casi di test potrebbero favorire un algoritmo
- nessun algoritmo rientra nel budget di risorse

Per ovviare a questi problemi, prima di scrivere il programma si analizza l'algoritmo tramite l'[[Analisi asintotica]].

Per misurare l'ordine di efficienza si utilizza dell'algoritmo basata sulle $n$ istanze in input.
Si misura l'efficienza, sotto forma di Tempo impiegato(t) o Memoria utilizzata(m).

Tra gli algoritmi di cui misureremo l'efficienza ci sono gli [[Algoritmi di ordinamento]] e gli [[Algoritmi di ricerca]]

### I tre casi importanti:
Per quanto riguarda l'efficienza di un algoritmo possiamo analizzare tre casi significativi:
- Caso migliore: $T_{best}=min(t)$
	Comunemente è il meno utilizzato perchè potrebbe accadere raramente ed è troppo ottimistico per definire correttamente il tempo di esecuzione di un algoritmo
- **Caso Peggiore:** $T_{worst} = MAX(t)$
	maggiormente utilizzato. Sai per certo che l'algoritmo performerà almeno così.
	è utile nella maggior parte dei casi, ma soprattutto nei casi in cui se l'algoritmo impiegasse molto tempo ad eseguire verrebbero causate ripercussioni inaccettabli.
- Caso medio: $T_{avg}=\sum t_{i}$
	difficile da calcolare, bisogna ricorrere alle probabilità.
	Non è sempre possibile calcolarlo

### Space/time tradeoff principle:
puoi ridurre il tempo di esecuzione, ma si alzerà la quantità di spazio richiesto, e viceversa.
Si può diminuire lo spazio riverso comprimendo o codificando l'informazione, ma decomprimerla richiederà molto tempo

### Disk-base space/time tradeoff principle:
meno spazio è necessario per eseguire un programma, più il programma sarà eseguito velocemente. il tempo per leggere informazioni dalla memoria di sistema è molto maggiore rispetto al tempo di computaziones

## Obiettivi principali nel design di programmazione :
- creare un algoritmo facile da comprendere, programmare e debuggare
- creare un algoritmo che utilizzi efficientemente le risorse del computer

## Estimating:
Estimatin is useful but not a subsitution for a detailed analysis of the problem. 
for example if the estimate indicates that the solution is not possible for various reasons, a further analysis becomes probably unnecessary.

1. Determine the major parameters that affect the problem
2. Derive an equation that relates the parameters to the problem
3. Select values for the parameters and apply the equation to yield an estimated solution

Always do it in two different, independent ways to make sure there are no mistakes → estimate directly, estimate what goes into the system
