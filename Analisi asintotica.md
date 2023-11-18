L'analisi asintotica è un metodo di stima matematico che misura l'efficienza di un algoritmo, cioè il tasso di crescita del costo di un algoritmo più la grandezza in input diventa grande. 
- è utile per stimare il quantitativo di risorse utilizzato per eseguire un algoritmo.
- Permette di comparare il costo di due algoritmi risolutivi per lo stesso problema 
- stimare se la soluzione proposta è al di sotto dei limiti di risorse prefissati

Molti fattori influenzano il tempo di esecuzione di un programma, come l'ambiente di programmazione (hardware),  e l'efficienza del codice
L'alternativa più affidabile è quella di usare delle misure come surrogati del tempo di esecuzione → operazioni base (non dipendono dai valori che assumono gli operandi), grandezza in input

### Elementi importanti nell'analisi asintotica:
- $n =$ dimensione dell'input
- $f(n)=$ Tempo di esecuzione o Occupazione in memoria di un algoritmo (relativamente $T(n) \space e \space S(n)$)
- $c =$ tempo richiesto per un operazione
- Essendo una stima si possono ignorare costanti e termini di ordine inferiore

un esempio di tempo richiesto (lineare) è: $T(n)=cn$

Le tre notazioni asintotiche possono essere calcolate nei casi Migliore, Peggiore, Medio. → Bisogna riportare a quale caso ci stiamo riferendo!
## Upper bound - $O(n)$:
Indica il tasso di crescita maggiore che può avere l'algoritmo.

**Definizione formale:**
$f(n)=O(g(n)) ⇔ |f(x)|\le c|g(x)|$      $\forall n\ge n_{0}$   con   $c>0, n_{0}\ge 0$

**Significato:**
Per tutte le quantità in input maggiori di $n_0$, l'algoritmo viene eseguito sempre in meno di $cg(n)$, con $c$ costante qualsiasi.
- $f(n)$ cresce definitivamente al più come $g(n)$.

![[Big-O notation.png | 200]]

**Proprietà simmetrica trasposta:**
$f(n)=O(g(n)) ⇔ g(n)=\Omega(f(n))$

## Lower bound - $\Omega(n)$:
Indica la quantità minima di risorse necessarie per l'esecuzione di un algoritmo per una quantità in input.

**definizione formale:**
$f(n)=\Omega(g(n)) ⇔ 0\le c g(x) \le f(x)$      $\forall n\ge n_{0}$   con   $c>0, n_{0}\ge 0$

**Significato:**
Definitivamente, l'algoritmo viene eseguito al minimo in $cg(n)$.
- $f(n)$ cresce almeno come $g(n)$.

![[Omega notation.png | 200]]

**Proprietà simmetrica trasposta:**
$f(n)=\Omega(g(n)) ⇔ g(n)=O(f(n))$

## Notazione asintotica $\Theta(n)$:
Usiamo questa notazione asintotica quando l'Upper e il Lower bound hanno lo stesso andamento ma sono moltiplicati per un fattore costante diverso.

**definizione formale:**
$f(n)=\Theta(g(n)) ⇔ c _{1} g(x) \le f(x) \le c _{2} g(x)$      $\forall n\ge n_{0}$   con   $c _{1}, c _{2}>0, n_{0}\ge 0$

**Significato:**
Definitivamente, l'algoritmo viene eseguito in un range tra $c_1 g(n)$ e $c_2 g(n)$.
- $f(n)$ cresce esattamente come $g(n)$

![[Theta notation.png  | 200]]

**Proprietà simmetrica:**
$\Theta(n)$ è verificata se e solo se sono vere sia $\Omega(n)$ che $O(n)$

Esempio: sia $f(n)=3n^{2}+10n$
- $f(n)=O(n^{2})$ → $\lambda = 3, n_{0}=10$
- $f(n)=\Omega(n^{2})$ → $\lambda=1, n_{0}=0$
- $f(n)=\Theta(n^{2})$ → siccome sono vere le altre notazioni asintotiche

## Comparare due funzioni:
$$\lim_{x\to\infty} \frac{f(x)}{g(x)}$$
- $\infty$: $f(n)=\Omega (g(n))$ perchè $f$ cresce più velocemente
- 0: $f(n)=O(g(n))$ perchè $g$ cresce più velocemente
- n: $f(n)=\Theta (g(n))$ perchè entrambe crescono alla stessa velocità

## Complessità campione:
Sono in ordine di Efficienza.

- $O(1)$ → costante
- $O(\log{}n)$ → logaritmica
- $O(n)$ → lineare
- $O(n\cdot \log{}n)$ → pseudolineare
- $O(n^{2})$ → quadratica
- $O(n^{k})$ → polinomiale
- $O(a^{n})$ → esponenziale

![[Complessità funzioni.png | 300]]
