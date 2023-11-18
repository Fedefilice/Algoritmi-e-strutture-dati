## - Rappresentazione indicizzata:
I dati sono contenuti in array che possono essere di un tipo dato qualsiasi. (allocazione statica)
Si può accedere a qualsiasi elemento tramite l'indice della cella in tempo costante $T(n)=\lambda$, con $\lambda=costante$.

### Pro:
Accesso veloce ai dati con indice

### Contro:
dimensione fissa (staticità), riallocare un array intero per aggiungere un elemento al di sopra del numero massimo di elementi!

## - Rappresentazione collegata:
I dati sono contenuti in record, numerati per indirizzo di memoria, collegati con puntatori.
I record allocati e distrutti singolarmente e dinamicamente.

### Pro:
Dimensione variabile (dinamicità)

### Contro:
- Accesso non sequenziale ai dati (Due record vicini, possono avere indirizzi di memoria non contigui) → non posso applicare la ricerca binaria in ogni caso
- utilizzo aggiuntivo di memoria per i puntatori collegati ai record

---
# Doubling-halving:
Tecnica di riallocazione di array non ordinati per `insert` e `delete` di elementi che diventano O(1). per rappresentazione indicizzata.
(tecnica per diminuire il numero di volte di riallocazione di un array)

$n$ = elementi nella collezione
$h$ = dimensione array, con $n\le h \le 4n$

 - se $n=0 → h = 1$
 - se $n>h$ si rialloca l'array con dimensione $h=2h$ 
 - se $n<\frac{h}{4}$ si rialloca l'array con dimensione $h=\frac{h}{2}$

  in questo modo 
  - le riallocazioni impiegano $T(n)=\Omega(n)$ 
  - la memoria necessaria è $S(n)=\Theta(h)=\Theta(n)$

Related: [[Struttura dati]]