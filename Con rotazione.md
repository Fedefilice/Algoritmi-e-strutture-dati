# AVL
L'albero AVL nasce per risolvere un problema nella complessità di operazioni e spazio utilizzato del BST, che dipende dall'altezza dello stesso. Nel BST possono esistere casi in cui l'altezza aumenta di molto e quindi l'efficienza dell'albero viene meno.

AVL è un BST che viene bilanciato in altezza → $h = log (n)$
- bilanciamento in altezza: un albero è bilanciato in altezza se le altezze dei sottoalberi Sx e Dx di ogni nodo, differiscono al max di un'unità
	$\beta(v) \le 1$ 

Un AVL ha tre elementi:
- elemento
- chiave
- fattore di bilanciamento $\beta (v)$ → differenza tra altezze di sottoalberi Sx e Dx (più è basso, meglio è)

---
## Metodi:
### `Rotazione` O(1)
(la visita simmetrica non cambia con la rotazione, la preordine cambia)

1. Scelgo un nodo sbilanciato come perno, $v$

**Casi quando un sottoalbero solo causa sbilanciamento:**
- Sinistra-sinistra(SS): $T$ è sottoalbero Sx di figlio Sx di $v$
	eseguo una rotazione semplice verso DESTRA
- Destra-destra(DD):
- Sinistra-destra(SD): $T$ è sottoalbero Dx di figlio Sx di $v$
	rotazione SX + DX 
- Destra-sinistra(DS):

**Sbilanciamento da due sottoalberi:**
applico una rotazione che bilancia l'albero, ma non diminuisce l'altezza.

### `Insert`

1. come nei BST, creo un nuovo elemento come foglia
2. ricalcolo i fattori di bilanciamento dei nodi nel cammino radice-nuovoElemento
3. applico rotazioni necessarie a bilanciare AVL (ne basta una)

### `Delete`
1. procedura BST
2. ricalcolo i fattori di bilanciamento dei nodi nel cammino radice-padreNodoEliminato
3. ripercorro il cammino da basso a alto applicando rotazioni necessarie, O(log n) rotazioni  

### `Search`
Procedura BST

---
# Alberi Splay
Gli alberi splay o alberi auto-aggiustanti è un BST con la proprietà che gli elementi cui si è acceduto più di recente vengono portati alla radice. 
L'albero viene aggiustato dopo un operazione qualsiasi
- **Operazione Splay - O(1):** parto dal nodo $u$ e risalgo fino alla radice eseguendo una sequenza di rotazioni → porto $u$ alla radice
	$p(u) = padre \space u$
	$p^2(u) = padre \space p(u) = nonno \space u$
	1. if (p(u) = radice) ruoto su $p(u)$
	2. if ($p^2(u) != NULL$ && $u \wedge p(u)$ sono figli Dx || Sx) ruoto su $p^2$ e poi su $p(u)$
	3. if ($p^2(u) != NULL$ && $u = figlio\space Sx$ e $p(u)=figlio\space Dx$ o viceversa) ruoto su $p(u)$, poi su $p^2(u)$ portando su $u$

- `search` dopo search eseguo splay sull'elemento in cui termina la ricerca
- `insert` dopo insert eseguo splay sull'elemento aggiunto
- `delete` dopo delete eseguo splay sul genitore del nodo cancellato

il tempo di queste operazioni è O(log n)
