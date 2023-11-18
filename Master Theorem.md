Si basa sulla tecnica del *Divide et impera*.

Serve per risolvere le relazioni di ricorrenza del tipo: 
$$T(n)=aT(\frac{n}{b})+f(n)$$
con:
- $n$ = dimensione dell'input
- $a\ge1$, $b>1$ costanti → a = numero di nodi figli di ogni nodo 
- $f(n)$ asintoticamente positiva

La complessità della relazione ricorsiva è data da queste formule
1. se $f(n) = O(n^{\log_b (a-ϵ)})$,    allora    $T(n) = \Theta(n^{\log_b a})$  con $ϵ>0$
2. se $f(n) = \Theta(n^{\log_b a})$ ,    allora    $T(n) = \Theta(n^{\log_b a}  \log n)$
3. se $f(n) = \Omega(n^{\log_b (a+ϵ)})$,    allora    $T(n) = \Theta(f(n))$ per $ϵ>0$, $a\cdot f(\frac{n}{b})\le c\cdot f(n)$ per $c<1$ e $n$ sufficientemente grande.
   
## Risoluzione esercizi:

```
T(n) = n + 2T(n/2)

1. Trovo i valori importanti:
f(n) = n
a = 2
b = 2

2. Calcolo log_a (b):
log_2 (2) = 1

3. utilizzo le formule e trovo quale delle 3 è verificata:
(solo una è verificata)

n = O(n^1-e) , con e > 0-> non verificata

n = Theta(n^1) -> n = theta(n) -> verificata!
quindi:
T(n) = Theta(n log(n))
```

---

- Divido il problema di dimensione $n$ in $a$ sotto problemi di dimensione $\frac{n}{b}$ 
- Risolvo i sotto problemi ricorsivamente
- Ricombino le soluzioni
Con $f(n)$ → tempo necessario per ricombinare le soluzioni
$$T(n) =
    \begin{cases}
      aT(\frac{n}{b})+f(n) \hspace{1 cm}se \hspace{0,2 cm}n > 1\\
      1 \hspace{3,1cm} se \hspace{0,2 cm} n=1
    \end{cases} $$

related: [[Analisi asintotica]]