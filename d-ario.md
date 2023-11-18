# Alberi 2-3:
Albero in cui ogni nodo interno ha 2 o 3 figli e tutti i cammini radice-foglia hanno la stessa lunghezza.
l'altezza è $\Theta log(n)$.  

ammettendo grado > 2 possiamo usare due operazioni alternative per #domanda
1. **separazioni**(split)
2. **fusioni**(fusion)

- chiavi e elementi sono assegnate alle foglie → chiavi in ordine crescente da Sx a Dx nelle foglie
- nei nodi interni ci sono due informazioni: 
	1. S\[v] = max chiave nel sottoalbero Sx di v
	2. M\[v] = max chiave nel sottoalbero centrale di v.

## Metodi:
`Insert:` O(log n) dobbiamo inserire u e individuiamo il genitore v
- v ha 2 figli: aggiungo u come terzo figlio mantenendo l'ordinamento (puo essere necessario aggiornare S e M)
- v ha 3 figli: separiamo il nodo in due con l'operazione di split.
	creiamo un nuovo nodo w e calcoliamo la posizione di u rispetto ai tre figli di v. 2 foglie con chiavi minime = figli w, le altre 2 di v.
	inserisco w come fratello di v. se ci sono 4 figli reitero il processo.
`Delete:` ci sono 3 casi: - O(log n) nel caso peggiore
- v = radice, la cancelliamo ottenendo un albero vuoto
- padre di v ha 3 figli, eliminiamo v e aggiorniamo S e M
- padre di v ha 2 figli, se padre di v = radice eliminiamo v e l'altro nodo = radice. 
	altrimenti usiamo l'operazione di fuse: w = padre, v=nodo da cancellare, l = fratello Dx di v. se l ha tre figli spostiamo figlio Sx di l come figlio Dx di w 
![[Pasted image 20230712171419.png | 200]]
	se l ha 2 figli attacchiamo il figlio rimasto di w come Sx di l e cancelliamo w
![[Pasted image 20230712171711.png | 200]]
`Search:` k da cercare - O(log n)
	se $k\le$ S cerco ricorsivamente nel sottoalbero Sx
	se $S \le k \le M$ cerco nel sottoalbero centrale
	se $k \ge M$ cerco in sottoalbero Dx

---
# B-Alberi:
Estensione di binary tree e alberi 2-3.
Struttura dati ottimizzata per minimizzare le operazioni di lettura e scrittura per la memoria secondaria (HDD-SSD).
utilità
- memoria secondaria lenta (ottimizzazione ancora più importante)
- la maggior parte dei dati sono memorizzati nell'hard disk

Minimizzare operazioni: L'hard disk quando accede a un dato, carica tutti i dati con vicinanza spaziale
L'idea è quindi quella di aumentare l'informazione a carico di ciascun nodo e il grado del nodo, rendendolo proporzionale a B

B è il blocco di dati che sfrutta la località spaziale

sia un intero $t \ge 2$ detto minimo, proporzionale a B,
un B-albero di grado minimo t è un albero con le seguenti proprietà:
1. tutte le foglie hanno la stessa profondità (come in albero 2-3)
2. ogni nodo v != radice ha k(v) chiavi ordinate con $t-1\le k \le 2t-1$. quindi il grado può variare (con t=2, $1\le k\le 3$)
3. $1 \le radice \le 2t-1$ chiavi.
4. ogni nodo interno v ha k(v)+1 figli
5. le chiavi sono ordinate e le chiavi del nodo padre sono idealmente tra i diversi figli (separano i figli). tutte le chiavi nel sottoalbero 1 Sx sono minori della prima chiave, tutte le chiavi nel sottoalbero 2 sono compresi tra prima e seconda chiave…
![[Pasted image 20230712185709.png | 350]]
	D sta tra B,C e F, G. H sta tra F, G e J, K, L...

un B albero con altezza h e n nodi ha: $h \le \log_t(\frac{n+1}{2})$

## Metodi:
- `Search:` simile ai BST, a un nodo v confrontiamo la chiave da cercare k con le chiavi nel nodo, decidendo che ramo scegliere.(il piu piccolo valore piu grande di k)
	il numero di chiamate ricorsive è $O(\log_t n)\le \log_2 n$ 
	in totale è $O(\log_2 n)$
- `Insert:` utilizziamo uno split per non violare il nodo pieno (2t-1), in cui le t-1 chiavi vengono messe in un nodo Sx, le t chiavi massime in uno Dx e la chiave in posizione t viene spinta in alto. 
	impiega $O(\log_t n)$
- `Delete:` usiamo fuse. si u il nodo che contiene l'elemento e che vogliamo cancellare e k la chiave corrispondente:
	1. se u foglia cancelliamo la chiave k
	2. se u nodo interno:
		- figlio y che precede k ha almeno t chiavi, trova il predecessore di k nel sottoalbero con radice y e cancellare il predecessore di k e sostituirlo a k (ha caso simmetrico)
		- se figlio y precede e z successivo hanno solo t-1 chiavi: fondi k con i propri figli in una sola foglia e elimina k. se la foglia è piena alla fine eseguire split

---
# Alberi 2-3-4 e Alberi rosso-neri:
### Albero 2-3-4:
è un B-albero con t = 2
- ogni nodo ha k(v) chiavi con $1 \le k(v)\le 3$, e $k(v)+1$ figli (2-4)
- `insert, cancel, search` sono eseguite come nei B-alberi

### Albero rosso-nero:
BST con proprietà di colorazione dei nodi per mantenere il bilanciamento
- ogni nodo ha colore rosso o nero 
- la radice è nera
- ogni foglia è nera e contiene NULL
- padre rosso → figli neri
- ogni cammino nodo-foglia ha lo stesso numero di nodi neri (altezza nera $h_n(v)$)

un albero rosso-nero con n nodi ha altezza $2 \log_2(n+1)$


## Trasformazione 234-rossoNero
![[Pasted image 20230713111103.png | 400]]