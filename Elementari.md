1. Dictionary 
2. tabella ad accesso diretto
3. [[List]]
4. [[Stack]]
5. [[Queue]]

# 1. Dictionary:
Collezione di elementi in cui gli elementi sono associati a delle chiavi univocamente. è ordinato
- Chiavi: sono uniche (no duplicati) e hanno attributi immutabili
- Valore associato alla chiave: può essere uno o può essere una collezione di valori → int, float, list, tuple...

## Operazioni supportate:
- `Insert`: si può inserire una nuova coppia chiave-elemento. se la chiave è già esistente, il valore associato verrà sostituito con l'ultimo inserito.
- `Delete`: viene cancellata la coppia chiave-valore
- `Search`: il valore associato alla chiave viene cercato passando la chiave come argomento di ricerca

## Pseudocodice:
TIPO Dizionario:
DATI: un insieme S di coppie(chiave, valore)
OPERAZIONI:
- insert (elemento e, chiave k)
	aggiunge a S una nuova coppia (e, k)
- delete (chiave k)
	cancella da S la chiave k e l'elemento associato ad essa
- bin_search (chiave k) → e
	restituisce e associato a k se k è presente in S,  altrimenti null

![[Dictionary.png | 400]]

# 2. Tabella ad accesso diretto:
Dizionario basato sull'accesso diretto alle celle del dizionario stesso tramite indice
è ordinato

- $k=chiave$
- $v = array$
- $e = elemento = v[k]$
- $m = celle$
- $\forall \space m$ è associata una chiave intera nell'intervallo $[0, m-1]$
- $n=numero \space elementi$
- è inefficiente dal punto di vista della memoria, possono esserci delle celle vuote. Il grado di riempimento della tabella è $\alpha=\frac{n}{m}$

il  problema è che le chiavi devono essere numeri interi distinti

c'è un insieme U di chiavi possibili con il suo sottoinsieme k di chiavi utilizzate che puntano a dati (possiamo dire che la tabella ad accesso diretto è un array)