Algoritmi che non utilizzano solo confronti, ma anche operazioni diverse in base al tipo di dato specifico.
# 1. Integer sort:
Ordinare $n$ numeri interi nell'array X di intervallo $[1, k]$.

**Funzionamento:**
creo un array Y di contatori di dimensione k+1 inizializzati a 0.
ogni volta che un valore compare, il contatore nella casella corrispettiva aumenta di uno.

![[Pasted image 20230411161319.png | 450]]

Nel caso generale si prevedono:
- possibilità di duplicati
- massimo valore dell'intervallo che non coincide con la lunghezza dell'array da ordinare ($k\neq n$)
### Analisi:
- inizializzazione $Y = O(k)$
- Calcolo valori dei puntatori: $O(n)$ 
- tempo totale per ricostruire $X$: $O(n+k)$

Se $k=n$ e non ci sono duplicati il tempo richiesto è $O(1)$
- la sequenza è già prestabilita (1, 2, 3, ..., n)


# 2. Bucket sort:
- elementi da ordinare sono generici record 
- un bucket è una lista di liste

``` 
bucketSort() 
  create N buckets that can contain a range of values
  for all the buckets:
    1. initialize each bucket with 0 values
    2. put elements into buckets matching the range
    3. sort elements in each bucket

  gather elements from each bucket
end bucketSort
```

Inserisco gli elementi ordinati in un array

![[sort.png]]

tempo O(n+k)

# 3. Radix sort:
- ordinare interi in $[1, k]$ quando il massimo valore $k >> n$

utilizza bucket sort 
(ogni numero di ogni cifra significativa è un bucket)

Ordina lavorando sul numero di cifre significative:
ordina tutti i numeri secondo la prima cifra significativa, poi ordina le decine.

![[radix sort.png | 400]]

### Analisi: 
- numero esecuzioni di bucket sort: $O(\log_b k)$
- costo esecuzione bucket sort: $O(n+b)$

costo totale: $O((n+b) \log_b k)$
b → base 

se $k<n$ conviene bucket sort O(n) rispetto a radix O(n log k)
se $k>n$ O(n log k) puo essere peggiore di O(n log n) con k>>n

### Ottimizzazione:
la base b va scelta opportunamente

$b=\Theta(n)$ → $O(n log(k)/log(n))$ 
se $k=O(n^c), c = cost$ → tempo lineare
