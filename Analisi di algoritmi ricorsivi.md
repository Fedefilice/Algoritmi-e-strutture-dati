è l'[[Analisi asintotica]] con metodi specifici per gli algoritmi ricorsivi

La quantità di risorse utilizzate da algoritmi ricorsivi può essere espressa tramite le relazioni di ricorrenza.
Analisi delle relazioni di ricorrenza → tempo speso per la procedura + tempo speso per le chiamate

## Relazione di ricorrenza:
Equazione matematica che descrive l'efficienza di un algoritmo ricorsivo. 
è una sequenza dove ogni termine è utilizzato per trovare il successivo.
$$T(n) =
    \begin{cases}
      c+T(\frac{n-1}{2}) \hspace{1 cm}se \hspace{0,2 cm}n > 1\\
      1 \hspace{3,1cm} se \hspace{0,2 cm} n=1
    \end{cases}  $$
con $c = costante$

Esistono diversi metodi risolutivi:

## Metodo della sostituzione:
- ipotizzo la forma asintotica della soluzione
- uso l'induzione per trovare le costanti e dimostrare la soluzione

Esempio
$$T(n) =
    \begin{cases}
      c+T(n-1) \hspace{1 cm}se \hspace{0,2 cm}n > 1\\
      1 \hspace{3,1cm} se \hspace{0,2 cm} n=1
    \end{cases}  $$
Ipotizzo che $T(n) = O(n) → T(n) < kn \space\forall n, k>1$
$T(n-1) +c\le k(n-1)+c$
#domanda
## Metodo dell'iterazione:
Sviluppo l'equazione di ricorrenza per intuire un pattern risolutivo.
applico la relazione di ricorrenza intuita e la pongo =1 (caso base), per ottenere il valore di i. 
sostituisco nel pattern risolutivo per ottenere la funzione da convertire poi con la relazione asintotica

Si converte la relazione di ricorrenza in una sommatoria fino a che la condizione iniziale è raggiunta

https://www.youtube.com/watch?v=ZUE8Qi4sRBo

https://www.youtube.com/watch?v=767BnLPc7Vo

https://www.codingninjas.com/codestudio/library/iteration-method

$$T(n)=c+T(\frac{n}{2})=c+(c+T(\frac{n-1}{2}))=2c+T(\frac{}{})$$
$$T(n-1)=c+T(\frac{n-1}{2}) $$
