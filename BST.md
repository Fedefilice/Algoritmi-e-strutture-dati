A BST is a binary tree that conforms to the following condition:
- All the nodes stored in the L subtree of a node have value $\le$ node. 
- All the nodes stored in the R subtree of a node have value $\ge$ node.

ogni nodo è formato da due valori: v (elemento, chiave) , la cui chiave(v) è presa da un dominio completamente ordinato

BST nodes are printed using an in-order traversal(simmetrico), the resulting enumeration will be in sorted order from lowest to highest.

## Metodi:
- `insert`  O(h)
	cerco il nodo v che diventerà genitore del nuovo nodo,
	creo il nuovo nodo u con elemento e e chiave k e rispettando la proprietà di ricerca lo appende come figlio Dx o Sx
- `search` O(h) 
```
//pseudocodice
ALGORITMO search(chiave k) -> elemento
	v<-radice T
	while (v != NULL){
		if (k = chiave(v)) return elem(v)
		else if (k < chiave(v)) v<-figlio Sx v
		else v<-figlio Dx v
	}
	return NULL
```
- `max` ricerca il nodo con valore massimo nel sottoalbero di un nodo u - O(h)
```
ALGORITMO max(nodo u) -> nodo
v-<u
	while(figlio Dx v != NULL){
		v<-figlio Dx v
	}
	return v
```
- `pred` predecessore di u è v con Max Chiave(v)$\le$chiave(u) - O(h)
	1. u ha figlio Sx, pred(u) → max del sottoalbero Sx u
	2. u non ha figlio Sx, pred(u) → più basso antenato di u, il cui figlio Dx è antenato di u(risalgo finche non trovo svolta a Sx)
```
ALGORITMO pred(nodo u)->nodo
	if (u ha figlio Sx(u)) return max(Sx(u))
	while(parent(u) != NULL && u è figlio Sx di suo padre){
		u<-parent(u)
	}
	return parent(u)
```
- `delete` O(h)
	ci sono 3 casi:
	1. u è foglia: elimino la foglia
	2. u ha un solo figlio w: se u = radice → w = radice. sostituisco l'arco (v, u) con (v, w)
	3. u ha due figli: individuo il predecessore v (max sottoalbero Sx di u, ha max un figlio a Sx) di u. copio chiave(v) in chiave(u). cancello v ricadendo in caso 1 o 2.
h = altezza = log n
albero ha al max $2^h$ nodi

---
# BST implementazione:
(implementazione professore programmazione c++, cioè fa un po schifo)

```c++
//#include "symbol_table_item.h"

// albero binario di ricerca
template <class Item, class Key>
class BST 
  {
    private:
	  // struttura dati per rappresentare i nodi dell'albero
		struct node 
        { 
	        Item item; //dato del nodo
	        node *l, *r; //puntatori ai figli
	        //costruttore del nodo -> inizializza un nuovo albero
        node(Item x) { item = x; l = 0; r = 0; } 
        }; 
      typedef node *link;
      link head;
      Item nullItem;
	  
	  // ricerca di un elemento data una chiave in ingresso
	  // restituisce, se presente, il primo elemento trovato nell'albero con la chiave cercata
      Item searchR(link h, Key v)
        { if (h == 0) return nullItem; //elemento non trovato
          Key t = h->item.key(); //chiave elemento corrente
          if (v == t) return h->item; //se chiavi uguali trovato elemento
          if (v < t) return searchR(h->l, v); //ricerca in sottoalbero sx o dx
                else return searchR(h->r, v);
        }
		
	  // inserimento di un elemento nell'albero binario di ricerca
      void insertR(link& h, Item x)
      //se puntatore null, creo un nuovo nodo e ci assegno il puntatore (foglia)
        { if (h == 0) { h = new node(x); return; }
        //confronto chiave elemento da inserire e chiave corrente
          if (x.key() < h->item.key()) 
               insertR(h->l, x);
          else insertR(h->r, x);
        }

		//Stampa gli elementi dell'albero
      void showR(link h, ostream& os)//h = radice, os = oggetto su cui scrivo elementi
        { 
          if (h == 0) return;
		  
          h->item.show(os); //oggetto con contenuto corrente
          //visita pre-order
		  showR(h->l, os);
          showR(h->r, os);
        }

	  void rotR(link& h) //rotazione verso destra
		{ link x = h->l; h->l = x->r; x->r = h; h = x; }
	  void rotL(link& h)
	    { link x = h->r; h->r = x->l; x->l = h; h = x; }

	  // nserisce un elemento come radice dell'albero, applicando rotazione per mantenere proprietà binaria
	  void insert_rootR(link& h, Item x)
	  //se albero vuoto ne creo uno
        { if (h == 0) { h = new node(x); return; }
        //se elemento a chiave minore di nodo corrente cerco la posizione corretta di x, poi applico una rotazione per far diventare h sottoalbero dx del nuovo nodo
          if (x.key() <  h->item.key()) 
           { insert_rootR(h->l, x); rotR(h); }
          else { insert_rootR(h->r, x); rotL(h); }
         }

	  // Restituisce l'elemento con k-esima chiave minore nell'albero.
	  Item selectR(link h, int k)
	  {
		  if (h == 0) return nullItem;
		  int t = tree_size(h->l);//calcolo dim sottoalbero sx
		  if (t > k) return selectR(h->l, k);//l'elemento cercato si trova nel sottoalbero sinistro
		  if (t < k) return selectR(h->r, k-t-1);  
		  return h->item; //Se nessuna delle condizioni precedenti è soddisfatta, significa che l'elemento cercato è l'elemento corrente h
	  }

	  // partizionamento: porta in radice il k-mo elemento con chiave minore
	  void partR(link& h, int k)
		  {  int t = tree_size(h->l);
			if (t > k )
			  { partR(h->l, k); rotR(h); }
			if (t < k )
			  { partR(h->r, k-t-1); rotL(h); }
		  } 

	  // fonde due alberi binari di ricerca in cui il secondo (b) contiene elementi con chiavi maggiori delle chiavi del primo albero (a)
	  // restituisce il nodo radice dell'albero risultante dalla fusione di a e b
	  link joinLR(link a, link b)
		{ 
		  if (b == 0) return a;
		  partR(b, 0); //sposta il nodo con la chiave minima nell'albero `b` nella radice
		  b->l = a; //`a` diventa il sottoalbero sinistro dell'albero `b`.
		  return b;//restituisce il puntatore al nodo radice dell'albero `b`
		}
		
	  // elimina, se presente, il primo elemento nell'albero con chiave v
	  void removeR(link& h, Key v)
		{ if (h == 0) return;
		  Key w = h->item.key(); 
		  if (v < w) removeR(h->l, v);
		  if (w < v) removeR(h->r, v);
		  if (v == w) //elemento da rimuovere è stato trovato.
			{ link t = h; //puntatore temporaneo `t` che punta a `h`
			  h = joinLR(h->l, h->r); //`h` viene sostituito con la fusione dei suoi sottoalberi sinistro e destr
			  delete t; }
		}

	  // fonde due alberi binari di ricerca generici
	  link joinR(link a, link b)
        { 
          if (b == 0) return a;
          if (a == 0) return b;
          insert_rootR(b, a->item); //inserisco radice di a in b-> a diventa radice
          b->l = joinR(a->l, b->l); //fusione dei sottoalberi sinistri.
          b->r = joinR(a->r, b->r); 
          delete a; return b;
        }

	//: Inserisce un elemento in modo casuale nell'albero.
	  void rand_insertR(link& h, Item x)
	    { if (h == 0) { h = new node(x); return; }
	      if (rand() < RAND_MAX/(1+tree_size(h)))
	        { insert_rootR(h, x); return; }
	      if (x.key() < h->item.key()) 
			  rand_insertR(h->l, x);
	      else rand_insertR(h->r, x);
	    }
	
	   // bilanciamento di un albero binario di ricerca
	   void balanceR(link& h)
			{
				int size;
	            size=tree_size(h);
				
				if (size<2) return;
				partR(h, size/2);
				balanceR(h->l);
				balanceR(h->r);
			}

   /*
   int height(link h)
   {
	   if (h == 0) return -1;
	   int u = height(h->l), v = height(h->r);
	   if (u > v) return u + 1; else return v + 1;
   }
   */
	public:
      BST()
        { head = 0; }

      int tree_size(link tree){
        if(!tree) return 0;
        return 1+tree_size(tree->r)+tree_size(tree->l);
        }

      Item search(Key v) 
        { return searchR(head, v); } 
        
      void insert(Item x)
        { insertR(head, x); }
        
	  void show(ostream& os)
        { showR(head, os); } 
        
	  void insert_root(Item item)
        { insert_rootR(head, item); }
        
	  Item select(int k)
        { return selectR(head, k); } 
        
	  void remove(Item x)
		{ removeR(head, x.key()); }
		
	  void join(BST<Item, Key>& b)
        { head = joinR(head, b.head); }
        
	  void rand_insert(Item x)
		{ rand_insertR(head, x); }
		
	  void balance()
		{ balanceR(head);}

	  /*int tree_height()
	  {
		  return height(head);
	  }*/
  };
```


search impiega T(n)=log n