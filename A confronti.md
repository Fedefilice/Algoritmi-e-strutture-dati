Sono algoritmi basati sul confronto tra oggetti.
**Lower bound:**
- $\Omega(n\log n)$ è lower bound al numero di confronti richiesti per ordinare n oggetti nei modelli a confronti
- nel caso in cui l'insieme è già ordinato(caso migliore) un algoritmo avrà un lower bound di $\Omega (n)$ confronti

---
# Algoritmi quadratici
I meno efficienti, il caso peggiore è $O(n²)$, cioè tutti i confronti possibili

## 1. Bubble sort - O(n²)
Confronta valori adiacenti, se non sono in ordine li scambia.
Dopo una scansione in cui non viene effettuato nessuno scambio l’array è ordinato.

Bubble sort (A, n = lunghezza A)
for (i=0 to i=n-1)
	if (A\[i] < A\[i+1]) scambia A\[i] ⇔ A\[i+1]

### Analisi:
- dopo al massimo $n-1$ cicli, l'array è ordinato
- al ciclo $k$ si fanno $n-k$ confronti
$$\sum_{k=1}^{n-1}(n-k) = \sum_{k=1}^{n-1}i= \Theta(n^2)$$
![[bubble sort.png | 450]]


## 2. Selection sort - O(n²)
Cerca l'elemento più piccolo non ordinato e lo porta nella posizione k+1 → un confronto in meno per ogni ciclo.

### Analisi: 
- Ricerca ogni volta il minimo in un insieme che si riduce a ogni modifica di $n-1$
- Al confronto k i confronti saranno $n-k-1$

$$\sum_{k=1}^{n-1}(n-k-1) = \sum_{k=1}^{n-1}i= O(n^2)$$
![[selection sort.png | 450]]


## 3. Insertion sort - O(n²)
L'algoritmo inserisce gli elementi nella parte disordinata nel posto giusto di quella ordinata.
- Ha un approccio incrementale: estende l'ordinamento da $k$ a $k+1$ elementi
- inserisce l'elemento $k+1$ nella posizione corretta rispetto a quelli ordinati

### Analisi:
- L'inserimento dell'elemento $k$ nella posizione corretta richiede $k-1$ confronti
- è necessario fare $n-1$ inserimenti
$$\sum_{k=1}^{n-1}i= \Theta(n^2)$$
![[Insertion sort.png | 500]]




---
# Algoritmi ottimi
O(n log n), il miglior tempo ottenibile con il metodo del confronto

## 1. Heap sort:
Funziona come il selection sort, risolvendo il problema maggiore, cioè la ricerca del minimo $O(n)$

Si usa una struttura dati ad albero chiamata #Heap, che consente di estrarre il MAX(o min) in $T(n)=O(\log n)$ ad ogni interazione. 
Inoltre la generazione della struttura e la cancellazione di un elemento devono essere veloci.

### Costruzione Heap:
- Costruisco un albero binario con gli elementi in ordine qualsiasi
- utilizzo un codice ricorsivo $T(n)=O(n)$
	Order_Tree(heap H)
		if (H vuoto) return
		else
			Order_Tree(sottoalbero Sx H)
			Order_Tree(sottoalbero Dx H)
			fixHeap (radice di H, H)
### Estrazione del massimo:
Per ordinare i valori estraggo MAX dall'heap e lo inserisco nell'array associato.
- Estrai $chiave(radice)$
- Copia nella radice l'elemento nell'ultimo livello a Dx ed elimina la chiave 
### Fix Heap:
Riordino l'albero ottenuto in modo tale da riottenere un Heap.
- Tutti i nodi apparte la radice soddisfano le proprietà di orinamento
- cerco il MAX figlio di $k$, scambio le due chiavi

fixHeap(radice k, heap H)
	if (k = foglia) return
	else
		u = massimo figlio di k
		if (chiave(k) < chiave(u))
			scambia chiave(k) e chiave(u)
			fixHeap(u, H)

### Analisi:
- costruisce heap → $O(n)$
- estrae il MAX $n-1$ volte → $O(n \log n)$
- inserisce MAX in lista → $O(1)$
$T(n) = O(n + n \log n) =O(n \log n)$

Utilizzo addizionale di memoria

per risparmiare più memoria si utilizza la struttura **"Heap rafforzata"** in cui le foglie nell'ultimo livello sono tutte a SX, quindi la dimensione del vettore associato sarà esattamente $n$
- non è bisogno l'utilizzo di una lista per memorizzare i dati perchè va già bene sottoforma di albero binario

## 2. Quick sort- O(n log n):
- Divide: 
	sceglie un elemento come pivot e divide valori più piccoli da quelli piu grandi del pivot. 
	in questo modo l'elemento pivot sarà nella sua posizone giusta
	divide la lista in sottoliste da ordinare, sceglie un nuovo pivot ricorsivamente fino ad ottenere n insiemi di dim=1
- Impera:
	unisce gli elementi in un singolo array

- Caso peggiore: $\Theta(n^2)$
- Caso medio e migliore: $O(n\log n)$
![[quicksort.png| 400]]
in quest'immagine si vede come alla fine gli elementi singoli sono ordinati e vanno solo inseriti in un array 

## 3. Merge sort - O(n log n):
Algoritmo ricorsivo
1. Divide:
	Divide ricorsivamente gli array fino ad avere array di un solo elemento.
2. Merge-ordina:
	l'ordinamento viene fatto implicitamente durante la procedura di merge. array di dim=1 si assume ordinato.
	- Si fondono due array estraendo il minimo tra il primo valore dei due array. 
	- il valore estratto viene copiato nell'array di unione dei due. si ripete questo processo fino ad ottenere un unico array, che sarà ordinato

### Analisi:
- Numero confronti:
	divide: $2C(\frac{n}{2})$
	merge: $O(n)$
	Tot: $C(n)=O(n \log n)$
- Memoria: Utilizza più memoria perchè serve un array ausiliario di dimensione n dove memorizzare il risultato dei merge
	$S(n)=2n$

![[Merge sort.png | 250]]