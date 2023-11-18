#tabella_accesso_diretto estesa con *funzioni hash* che permettono di utilizzare degli elementi diversi da interi come indici.

Implementazione specifica del tipo dato dizionario utilizzando le funzioni hash

Struttura dinamica, Il suo pro è la ricerca:
caso medio T(n)=O(1)
caso peggiore T(n)=O(n)

spazio necessario O(k), con k=numero di chiavi utilizzate

l'insieme U contiene solo il sottoinsieme k con le chiavi (elementi qualsiasi ordinati) che tramite una funzione hash puntano ai valori

![[hash function.png| 500]]

l'insieme delle chiavi è illimitato → a causa della funzione, due chiavi potrebbero puntare allo stesso valore → collisione

# Funzione hash: 
Funzione che serve a convertire gli indici, che non sono necessariamente numeri interi a numeri interi

dato U = insieme ordinato di indici(chiavi),
	funzione $h: U → [0, m-1]$ che associa a un elemento $u\in U$, un indice nella tabella hash
elemento con chiave $e$ è in posizione $v[h(k)]$

## Collisioni:
Problema che sorge quando inserisco un nuovo elemento con chiave $u$, e nella tabella esiste un elemento con chiave $v$ tale che l'indice associato alle due chiavi coincide $h(u)=h(v)$
- il nuovo elemento dovrebbe sovrascrivere il vecchio

**Cause:**
- funzione hash sbagliata per cui per due chiavi distinte l'indice è uguale
- scelta di chiavi sbagliata

**Evitare collisioni:**
- usare funzione hash perfetta, cioè iniettiva
	$\forall u, v \in U: u\neq v → h(u) \neq h(v)$
	è difficile che si verifichi perché per accadere, il numero di chiavi deve essere minore del numero di celle dell'array associato $|U|\le m$

Spesso usare una funzione perfetta non è possibile o non conviene → si possono usare funzioni non perfette a patto che la probabilità di collisioni sia bassa e il comportamento delle collisioni sia prevedibile

**Ridurre collisioni:** 
funzione che distribuisce in modo uniforme le chiavi in U
- Uniformità semplice:
	P(k) = probabilità che la chiave k sia presente nel dizionario.
	La probabilità che la cella sia occupata deve essere tale che ogni cella ha la stessa probabilità di essere utilizzata, cioè: $$Q_i = \sum_{k:h(k)=i} P(k) = \frac{1}{m}$$se Qi = 1/m la funzione gode di uniformità semplice

**Risolvere collisioni:** due metodi classici #domanda 
1. **Liste di collisione**, assumo di avere una lista di liste invece che i singoli elementi, quando c'è una collisione si aggiunge un elemento allo stesso indice nella lista nidificata
2. **Indirizzamento aperto**, gli elementi sono contenuti in una tabella in cui se una cella è occupata se ne cerca un altra
	n < m, il fattore di carico < 1
	bisogna definire una funzione di scansione c che cerca la cella vuota
	- scansione lineare $c(k, i) =(k(k)+i) mod \space m,\space per\space 0\le i <m$ 
		gestisce male lo spazio, perché crea lunghe sequenze di caselle piene mentre altre sono vuote
	- hashing doppio: gestisco il passo di incremento con una funzione hash. cosi se due chiavi collidono la sequenza di scansione sarà diversa
		$c(k, i)= (h_1 (k)+ih_2(k))mod\space m, \space con \space 0\le i<m,\space k_1,\space h_2$ funzioni hash

## Scegliere una funzione hash:
Assumiamo l'equiprobabilità dei vari casi anche se non è realmente così
1. Metodo della divisione:
	$h(k) = k \space modulo \space m$ 
	- nella maggior parte dei casi è una buona scelta
	- la scelta di m è importante, numero primo
2. Metodo del ripiegamento:
	$h(k)=f(k1, k2, ..., ki)$
	divido la chiave k in sotto parti e si sceglie una funzione a piu variabili con dominio {0, m-1}

Tempo richiesto per operazioni elementari (search, insert, delete): $T(n)=O(1)$


## `delete:`
non possiamo marcare come vuota la cella dell'elemento cancellato perché il search si fermerebbe in quella casella, cosi scombinando la funzione hash.

risolviamo il problema creando un campo canc da inserire nelle celle in cui si cancella un elemento. 
search non si ferma quando trova canc
insert invece si ferma e inserisce in quella cella