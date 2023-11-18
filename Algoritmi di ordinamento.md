Algoritmi specifici atti ad ordinare degli elementi in un insieme. Tra questi elementi deve essere definita una relazione di ordinamento.
Permutazione: modifica nell'ordine degli elementi di un insieme

- Il vantaggio di ordinare un insieme è che il tempo per la ricerca lineare è O(n) e quello per la ricerca binaria è O(log n).
- L'efficienza è misurata usando come unità di misura il numero di confronti necessari n.

## Tipi di ordinamento:
- [[A confronti]]
- [[Altri]]

## Alberi di decisione:
Gli algoritmi di ordinamento possono essere descritti con un albero di decisione, cioè un albero binario che descrive i confronti che possono essere fatti.
- ogni nodo contiene la coppia da confrontare con indici (i  ;  j)
- seguo il ramo risultante dal confronto (se i < j → si va a Sx e viceversa)
- le foglie indicano la permutazione ottenuta

comprende tutti i percorsi possibili per ordinare n elementi → al massimo $n!$ (numero di foglie → tutte le permutazioni possibili)
l'altezza dell'albero di quando si arriva alla foglia equivale al costo dell'algoritmo.

un albero binario con k foglie ha altezza almeno log2 k

## Stabilità:
#domanda 
![[domanda1.png]]