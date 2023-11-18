Generalizzando una Linked list otteniamo una struttura dati ad albero

Un albero è una struttura dati non lineare formata da nodi legati da archi direzionati, in cui ogni nodo può avere un solo arco entrante ed un qualunque numero di archi uscenti. Presenta relazioni gerarchiche.

Matematicamente è una coppia T(N, A) in cui: 
- N = insieme di nodi  
- A = insieme degli archi $A\subseteq N\times N$
	Un arco è una coppia di nodi direzionata con puntatori

- radice (r) = nodo generatore dell'albero
- nodo singolo (v) = nodo interno
- foglia = nodo senza figli

![[Tree.png | 500]]
Si utilizza la similitudine con gli alberi genealogici:
- un nodo, ad esempio r, si dice **genitore** dei nodi a cui punta, ad esempio v 
- il nodo puntato da un genitore viene chiamato **figlio**
- **fratelli** sono nodi con lo stesso genitore
- **grado** è il numero di nodi generati da un nodo padre
- **antenati/discendenti** sono i nodi raggiungibili salendo o scendendo

- **Profondità di un nodo** è il numero di archi che bisogna attraversare per raggiungerlo partendo dalla radice
- **altezza massima** alla foglia alla profondità maggiore
- Size = numero di nodi

``` Operazioni di un albero
numNodi()->int
	//restituisce il numero di nodi presenti nell'albero
grado(nodo v)->int
	//numero di figli del nodo
figli(nodo v)->[nodo, nodo, ...]
	//restituisce tutti i figli del nodo v
aggiungiNodo(nodo u)->nodo
	//inserisce un nodo v come figlio di u e lo restituisce
	//radice se albero vuoto
aggiungiSottoalbero(albero a, nodo u)
	//inserisce nell'albero il sottoalbero a in modo che radice di a diventa figlia di u
rimuoviSottoalbero(nodo v)->albero
	//cancella dall'albero il nodo v e i discendenti

```


# Diverse versioni di albero:
- [[d-ario]] → albero di grado massimo $d$, almeno un nodo ha d figli 
	Livello saturo = massimo numero possibile di figli
	pieno = tutti i livelli sono saturi (le foglie non importano)
	completo = pieno + i nodi dell'ultimo livello sono posti piu a Sx possibile

- [[Binary Tree]] → $d$-ario con $d=2$

---
#treeTrasversal
# Tree Traversals DFS:
normalmente si usa con alberi binari 
DFS: visita in profondità di un albero. si utilizza il tipo dato stack/algoritmo ricorsivo

Process of visiting each node exactly once.
we visit from L to R.
![[traversals.png| 350]]

- **Preorder traversal:** we divide the tree in L and R subtree and we want to visit any node on the same level before visiting its children. it starts from the root.
	ABDCEFGHI (note DC)
	root → all nodes of the L subtree LR → all nodes of R subtree
	
- **Postorder traversal:** visit each node after we visit its children. It starts with the most left leaf. (deleting tree)
	DBGEHIFCA
	all leaves of a node, then the node and its leaves... (L subtree → R subtree)
	
- **Inorder traversal(simmetrico):** L child, node, R child. It starts with the most left-down leaf.
	BDAGECHFI

`ALGORITMO Visita Generica(nodo r)` 
S = {r}
WHILE ($S\neq \emptyset$) DO
	estrai un nodo $u$ da S
	visita il nodo $u$
	$S=S \cup$ {figli di $u$}

$T(n)=S(n)=O(n)$

## Tree traversal BFS:
BFS: visita in ampiezza (breadth first search)
usato tipo di dato queue

starts from root. visit every node of one level, then go to next level
	ABCDEFGHI

---
# Rappresentazioni indicizzate:
## 1. **rappresentazione vettori padri**
si utilizza un array P\[n] le cui celle contengono la coppia (elemento, indice del genitore). 
i nodi sono numerati da 0 a n-1
![[Pasted image 20230710165845.png | 350]]

## 2.**rappresentazione con vettore posizionale** 
si puo utilizzare con un d-ario completo.
n va da 1 a n
ogni oggetto dell'array contiene una sola informazione: (elemento)
questo perché utilizzo gli indici dell'array.
la casella che contiene il nodo $i$ figlio di $v$ viene assegnata con $d\times v+i$ con $i \in [0, d-1]$ 
![[Pasted image 20230627214308.png | 400]]
trovo il padre con $[v/d]$ arrotondato per difetto


# Rappresentazioni collegate:
## 1. **rappresentatore puntatore ai figli:**
supponendo che ogni nodo abbia grado al piu d, 
in ogni record contengo il dato e il numero di puntatori d, messi a null quando non è presente il figlio
![[Pasted image 20230627224933.png | 300]]

## 2. **rappresentazione lista figli:**
quando il numero massimo di figli non è noto,
a ogni nodo associo una lista di puntatori ai figli (puo essere fatto tramite array o puntatori)
![[Pasted image 20230627224813.png | 300]]

## 3.**Primo figlio-fratello successivo:**
non necessita di una struttura dati addizionale come lista figli.
ogni record punta al primo figlio, il quale punta al fratello successivo
![[Pasted image 20230627225105.png | 300]]

Related: [[BST]], [[Con rotazione]], [[d-ario]]