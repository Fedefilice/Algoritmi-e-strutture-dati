Albero binario radicato. 
- **struttura** completa fino al penultimo livello
	le foglie partono sempre da sinistra
- Gli elementi sono memorizzati nei nodi, indicati con una $chiave(v)$
	i = nodi percorsi per arrivare alla casella dalla radice, conto anche il nodo di cui devo trovare la posizione nell'array
	figlio Dx = 2i
	figlio Sx = 2i + 1 
	padre = i/2, arrotondato per difetto
![[Heap.png | 350]]

## Proprietà: 
- MAX è nella radice
- $chiave(padre(v)) ≥ chiave(v)$
- n = numero di nodi
- $h = O(\log n)$ → albero binario

related: [[Tree]]
#Heap 

## Max-heap methods:

`Max-heapify` maintains max-heap property

---
The heap data structures is defined by two properties:
1. It's a complete binary tree
2. the values are partially ordered
	Non c'è necessariamente una relazione tra il valore di un nodo e quello dei suoi fratelli. è possibile che i valori del sottoalbero Sx siano maggiori di quelli nel sottoalbero Dx.
	Nel BST invece gli elementi sono totalmente ordinati.

There are two heap variants:
- **Max-heap:** elemento i $\le$ genitore → heap sort
- **Min-heap:** elemento i $\ge$ genitore → priority queue

heap **logical representation**(tree structure) $\neq$ **physical implementation**(array based)

---
# Priority Queue
Collezione di oggetti organizzata per importanza o priorità

Struttura dati che può essere implementata in diversi modi, tra cui un Heap

## Metodi comuni a entrambe le implementazioni:

```c++
template <class Item>
void exch(Item& A, Item& B) //scambio due valori
{
    Item t = A; 
    A = B; 
    B = t;
}

//mantenere proprieta heap dopo inserimento di un nuovo elemento. MaxHeap
template <class Item>
void fixUp(Item a[], int k) //k = numero di elementi
{
    //k>1 -> controlla se elemento è radice. se è radice esci
    while (k > 1 && a[k / 2] < a[k]) // a[k/2]<a[k] controlla se padre < figlio. se falso esci.
    {
        exch(a[k], a[k / 2]); 
        k = k / 2; // update per confronto con genitore successivo
    }
}

//ripristinare la proprieta dell'heap dopo la rimozione radice(elemento max)
//radice spostata a foglia
template <class Item>
void fixDown(Item a[], int k, int N) //k = 1, N = N - 1
{
    while (2 * k <= N) //eseguito n/2 volte
    {
        int j = 2 * k; //primo figlio sx di radice
        if (j < N && a[j] < a[j + 1]) j++; //figlio sx < figlio dx -> dx maggiore, confronto con padre
        if (!(a[k] < a[j])) break; //se elemento padre (k) >= (j) figlio -> gia ripristinato, fine ciclo
        exch(a[k], a[j]); //sposto elemento piu piccolo k verso il fondo 
        k = j; //confronto con i figli successivi
    }
}

//ordinare un array a[] in modo decrescente. 
//Inserisce gli elementi dell'array nella coda di priorità ausiliaria e li estrae uno alla volta, riportando l'array in ordine.
template <class Item>
void PQsort(Item a[], int l, int r) //array, indice inizio, indice fine.
  { int k;
    PQ<Item> pq(r-l+1);  //creo una pr_queue
    for (k = l; k <= r; k++) pq.insert(a[k]); //inserisco elementi nella queue
    for (k = r; k >= l; k--) a[k] = pq.getmax(); //estraggo il max e inserisco in a
//ordine decrescente
  }
```

---
## Array priority queue implementation:

Basata su un array dinamico.
Max-Heap

```c++
template <class Item>
class aPQ    // array based priority queue
  {
    private:
      Item *pq; //puntatore che contiene l'indirizzo di memoria contenuto nell'array
      int N;
    public:
      aPQ(int maxN) //constructor
    { 
        pq = new Item[maxN]; 
        N = 0; 
    }
        
	  ~aPQ() { delete[] pq; } // Destructor
	  
      int empty() const { return N == 0; } 
      //const indica che il metodo non cambia il contenuto
      
	  // inserisce un elemento
      void insert(Item item) { pq[N++] = item; }
        
	  // extract max element
      Item getmax()
        { int max = 0;
          for (int j = 1; j < N; j++)
            if (pq[max] < pq[j]) max = j;
          exch(pq[max], pq[N-1]);  
          return pq[--N];
        }
  };
```

---
## Heap priority queue implementation:

Basata su un heap binario. Max-Heap.
Gli elementi vengono organizzati all'interno di un array come un heap binario, in cui l'elemento massimo è posizionato alla radice dell'heap. 

```c++
template <class Item>
class PQ // heap based priority queue
  {
    private:
      Item *pq; 
      int N;
    public:
      PQ(int maxN)
        { pq = new Item[maxN+1]; N = 0; }
        
	  ~PQ() { delete[] pq; } // Destructor
	  
      int empty() const
        { return N == 0; }
        
      void insert(Item item)
        { pq[++N] = item;  fixUp(pq, N); }
        
      Item getmax()
        { 
          exch(pq[1], pq[N]); //scambio ultimo elemento con max
          fixDown(pq, 1, N-1); 
          return pq[N--]; 
        }
  };
```
