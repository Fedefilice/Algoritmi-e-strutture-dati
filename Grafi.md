Un grafo è un astrazione matematica usata per rappresentare una connessione o relazione tra coppie di oggetti

G(V, E)
- V = vertici/nodi
- E = archi/spigoli (coppie di vertici), relazione tra nodi
- ogni arco connette due vertici

- n = numero nodi
- m = numero spigoli

(un albero è un grafo direzionato senza cicli)

possono essere:
- **Orientati** se hanno una direzione, relazione asimmetrica
	V = {persone che vivono in Italia}
	E = {(x, y)persone x che inviano una mail a y}
- **Non orientati** gli archi non hanno una direzione, relazione simmetrica

Relazione tra vertici:
- **Adiacenza**
	G Orientato, nodo u adiacente in v se l'arco esce da u e entra in v
	Non Orientato, nodi connessi
- **Incidenza**
	Orientato, esce da u e entra in v
	arco che connette due nodi è incidente agli stessi

Grado di un vertice: $\delta(v)$
numero di archi incidenti su v
- sommando il grado di tutti i nodi in un grafo non orientato contiamo ogni arco due volte, quindi il **grado totale del grafo è 2m**
- in un grafo orientato ci sono gradi di entrata e uscita, il grado totale è la somma dei due

**Raggiungibilità** → due nodi sono raggiungibili se esiste un cammino che li connette 
**Grafo connesso**, esiste un cammino tra ogni coppia di nodi
**Grafo fortemente connesso**, esiste un cammino tra ogni coppia di nodi (orientato)
**Sottografo**, un grafo G' è sottografo di G se ogni vertice e arco di G' appartiene anche a G
**Sottografo indotto**, 

# Metodi:
- `numVertici`
- `numArchi`
- `Grado`
- `archiIncidenti`
- `estremi`
- `opposto`
- `sonoAdiacenti`
- `aggiungiVertice`
- `aggiungiArco`
- `rimuoviVertice`
- `rimuoviArco`

# Cammini:
Il cammino da u a v di lunghezza k di un grafo G è dato dalla sequenza di vertici per cui ogni arco attraversato appartiene a G
- **cammino semplice**, non attraverso due volte lo stesso vertice
- **ciclo**, il vertice finale e iniziale coincidono

il cammino è dato dal numero di nodi attraversati meno 1

---
# Strutture dati per rappresentare grafi:
- **Lista di archi:** ogni oggetto contiene il vertice e il vertice di un arco adiacente
	S(n) = O(n + m)
	la maggior parte delle operazioni impiegano O(m)
	orientato è piu corto

- **Lista di adiacenza:** ho una lista per ogni vertice che contiene i nodi adiacenti.
	spreco di memoria, ogni arco appare in più liste O(n + m)
	molte operazioni sono più efficienti, O($\delta(v)$) nel caso peggiore
	sono già direzionali come concetto

- **Lista di incidenza:** ogni vertice mantiene una lista di indici che puntano a una lista di archi. 
	analisi spazio e costo operazione = lista di adiacenza
	sono già direzionali come concetto

- **Matrice di adiacenza:** matrice m x m in cui righe e colonne indicizzano i nodi, funziona solo per grafi non orientati
	ogni elemento è 1 se i due nodi sono connessi, 0 altrimenti
	S(n) = O(n^2)
	pro: adiacenza nodi, aggiungere o rimuovere archi
	contro: aggiunta o rimozione vertice = rialloca matrice
	matrice simmetrica

- **Matrice di incidenza:** matrice n x m in cui righe indicizzano i nodi e le colonne gli archi
	ogni elemento è 1 se il nodo appartiene a un arco → ogni colonna ha max due valori
	S(n) = O(nm)
	prestazioni peggiori
	esco con +1, entro con -1

---
# Visita di grafi:
- **Visita generica:** 
	1. parto da un nodo s
	2. costruisco un sottoalbero T di G i cui archi formano un albero radicato in s
	3. per non visitare più volte il vertice si marcano i nodi. inesplorato, aperto (visitato per prima volta), chiuso (vicini esaminati)
	
	T contiene i vertici incontrati fino a quel punto
	F = frangia, contenuto in T. contiene i vertici aperti (i restanti sono chiusi)

```
ALGORITMO visita generica(vertice s)->albero
	T<- albero formato da s
	F<- insieme vuoto di vertici
	marca il vertice s e aggiungi s a F
	WHILE (F!=0){
		estrai un vertice u da F
		visita u
		FOR EACH (arco (u, v) in G){
			IF (v non è ancora marcato){
				marca v e aggiungi v a F
				rendi u padre di v in T
			}
			ELSE{
				rendi u nuovo padre di v in T
			}
		}
	}
	return T
```

costo:
- lista di archi O(nm)
- liste di adiacenza O(m + m)
- matrice di adiacenza O(n^2)

### proprietà albero visita BFS, grafo non orientato:
- il livello di v nell'albero BFS è pari alla distanza di v dalla sorgente s
- per ogni arco (u, v), gli estremi appartengono allo stesso livello o a livelli consecutivi dell'albero BFS
- gli archi possono essere classificati in 3 gruppi rispetto all'albero prodotto: archi di BFS, archi tra vertici dello stesso livello del BFS, archi tra livelli adiacenti del BFS

### proprietà albero visita BFS, grafo orientato:
- possono esistere archi che attraversano più di un livello all'indietro
- 4 gruppi rispetto al BFS prodotto: archi di BFS, archi tra vertici dello stesso livello del BFS, archi che vanno da un livello al successivo, o al precedente

### DFS:
```
PROCEDURA visita DFS ricorsiva(vertice v, albero T)
	marca e visita il vertice u
	FOR EACH (arco (u, v)){
		aggiungi arco (u, v) a T
		visita DFS ricorsiva(v, T)
```

**proprietà grafo non orientato:**
- (u, v) è arco di DFS 
- i nodi u e v sono discendenti/antenati dell'altro

**proprietà grafo orientato:**
- (u, v) è arco di DFS 
- i nodi u e v sono discendenti/antenati dell'altro
- (u, v) è un arco trasversale a Sx (il vertice v è in un sottoalbero visitato precedentemente ad u)

## connessione in grafo non orientato:
la visita del grafo è utile a verificare se il grafo è connesso

la proprietà di raggiungibilità ha tre condizioni:
- Riflessività → ogni nodo è raggiungibile da se stesso
- Simmetria → gli archi possono essere percorsi in entrambe le direzioni
- Transitività → se esiste un cammino da u a v e da v a w, allora esiste anche da v a w

un grafo è connessa se e solo se ha una sola componente connessa

## connessione forte in grafo orientato:
due nodi sono fortemente connessi se esiste un cammino da u a v e da v a u

- Riflessività → ogni vertice è fortemente connesso a se stesso
- Simmetria → se u ↔ v allora v ↔ u
- Transitività → se esiste un cammino da u a v e da v a w, allora esiste anche da v a w. questo è possibile assumendo il fatto che i cammini possono avere vertici in comune

---
# Minimi alberi ricoprenti:
Dato un grafo non orientato e connesso G(V, E),

Un **ALBERO RICOPRENTE** di G è un sottografo T compreso in G tale che
- T è un albero contenente tutti i vertici di G

- w(e) = costo di un arco $e\in E$ 
- **MINIMO ALBERO RICOPRENTE** di G→ Albero ricoprente di costo minimo
	costo = somma dei costi degli spigoli che l'albero contiene

Possono esistere diversi minimi alberi ricoprenti
![[Pasted image 20230717161547.png | 400]]

## Taglio:
un taglio di G è una partizione dei vertici in due insiemi, X e X' = V-X

un arco e = (u, v) attraversa il taglio (X, X') se $u \in X \wedge v \in X'$

## Tecnica Golosa:
Tecnica per costruire un minimo albero ricoprente un arco alla volta includendo o escludendo archi dalla soluzione.
- Archi blu → inclusi in soluzione
	Regola blu(del taglio)
		scegli un taglio che non contiene archi blu, scegline uno di costo minimo e coloralo di blu
- Archi rossi → esclusi da soluzione
	Regola rossa(del ciclo)
		scegli un ciclo che non contiene archi rossi, scegline uno di costo massimo e coloralo di rosso

Bisogna applicare a ogni passo una delle due regole fino a colorare tutti gli archi. (Esiste sempre un minimo albero ricoprente che contiene tutti gli archi blu e nessuno rosso)

si ottengono diversi algoritmi:
#domanda 
### 1. Kruskal: $O(m \log n)$
cerca da arco con valore piu piccolo, senza connettere due nodi già connessi

foresta: grafo non orientato, aciclico in cui due vertici qualsiasi sono connessi da al più un cammino (unione disgiunta di alberi)

Mantiene una foresta di alberi disgiunti, all'inizio consiste degli n vertici del grafo 
Ordina gli archi in ordine non decrescente di costo e per ogni arco:
- se gli estremi appartengono a due alberi diversi della foresta applica la regola del taglio e aggiungi l'arco alla foresta unendo i due alberi
- se gli estremi appartengono allo stesso albero applica regola del ciclo e omettilo dalla soluzione

i vertici sono mantenuti da una struttura dati union find

### 2. Prim: $O(m+n \log n)$
Utilizziamo una lista per tenere conto dei nodi visitati
partiamo da un nodo arbitrario e lo aggiungiamo alla lista.
→ scegliamo l'arco con valore minore

guardiamo i nodi che si possono visitare dai nodi già visitati scegliendo ogni volta l'arco con valore minore che porta a un nodo non visitato

costruisce un unico albero blu

### 3. Boruvka: $O(m \log n)$

---
# Cammini minimi su grafi orientati:

**proprietà:**
- sottostruttura ottima → ogni sotto cammino di un cammino minimo è anch'esso minimo
- grafi con cicli negativi → non esiste un cammino minimo finito tra essi
- se G non contiene cicli negativi, esiste sempre un cammino minimo semplice 
- distanza tra due vertici d → costo di un cammino minimo tra i due vertici. (+inf se i vertici non sono connessi)
- disuguaglianza triangolare → $d_{xz} \le d_{xy} + d_{yz}$
- condizione di bellman → per ogni costo arco w(u, v) e ogni vertice s, $d_{su} +w(u, v)\ge d_{sv}$ → se = allora ho percorso il cammino minimo

ricostruire un cammino anche conoscendo le distanze puo richiedere fino a n volte la sua lunghezza. 
i cammini minimi da un vertice s a tutti gli altri vertici del grafo possono essere rappresentati tramite un albero T radicato in s (albero dei cammini minimi)
ogni cammino in T è un cammino minimo in G

### Tecnica del rilassamento:
utilizzata dai prossimi algoritmi, serve per effettuare stime delle distanze per poi arrivare a quelle corrette.
Parto da stima per eccesso delle distanze, le aggiorno fino a renderle esatte
$$if(D_{xv}+w(\pi_{vy})<D_{xy})\{D_{xy} ← D_{xv}+w(\pi_{vy})\}$$
se trovo un cammino meno costoso di quello iniziale, lo sostituisco

## Algoritmo di Dijkstra:
cammini minimi a sorgente singola

cammino minimo da un nodo a tutti gli altri con costi non negativi
è un algoritmo goloso

1. parto da un nodo da me scelto e vedo gli archi di costo minore che trova
2. scelgo un solo nodo dell'arco a costo minore e reitero. tenendo conto che se trovo un cammino meno costoso per un nodo già visitato faccio update

$O(m \log n)$ usando un heap
$O(m+n \log n)$ usando un heap di Fibonacci

## ALGORITMO DI BELLMAN E FORD:
cammino minimo da un nodo a tutti gli altri
con n = numero vertici, iteriamo n-1 volte l'algoritmo ogni ciclo.

1. inizializzo ogni distanza a +inf
2. fa n cicli, effettua rilassamento in ordine di tutti gli archi

esegue molti rilassamenti inutili
T(n) = O(nm)

## Ordinamento topologico:
bellman e ford senza cicli

funzione L: V → {1, .., n}: L(u)<L(v) se esiste un cammino da u a v in G

identificare un nodo senza archi entranti e assegnare L(u)=1
cancello il nodo del grafo e vedo i nodi che hanno solo archi uscenti

T(n) = O(n + m)

## Algoritmo di Floyd Warshall
cammino minimo tra tutte le coppie di vertici, con sorgente che varia

creiamo una matrice $nxn$ e inizializziamo tutti i nodi a 0 sulla diagonale

$T(n) = n^3$