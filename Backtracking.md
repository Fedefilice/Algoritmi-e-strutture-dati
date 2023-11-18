## Constraint satisfaction problem(CSP):
è caratterizzato da un insieme di variabili che devono rispettare dei vincoli specifici

Esempio: problema 8 regine scacchi (96 soluzioni)
	variabili → dove mettere le regine
	vincoli → regole scacchi, le regine non devono minacciarsi l'una con l'altra

### Tecnica, generate and test:
- Generate: assegna un valore a ogni variabile
- Test: verificare che i vincoli sono soddisfatti

Problema regine:
k=8, n=64 → 4 Mld di soluzioni possibili generate
$\binom{n}{k}=\frac{n!}{k!(n-k!)}$
![[Pasted image 20231027092706.png | 150]]
### Generate and test ridotto:


## Standard backtracking:
Ad ogni assegnamento verifico i vincoli, appena sono violati termino l'assegnamento

Problema regine → 2056 tentativi

## Implementazione regine:

- creo tavola di gioco
- controllo se la regina è sotto attacco (controllo una casella alla volta)
	Inserisco regine da alto a basso per controllare solo regine sopra (vado sempre una riga sotto) → se sotto attacco cerco un'altra posizione
- se ho piazzato tutte le regine correttamente fine 

``` python
def print_board(board: list): 
	for v in board: 
		print("•" * v + "♛" + "•" * (len(board)-v-1)) 
		
def under_attack(board: list, x: int, y: int) -> bool: 
	for r in range(y): # for each row above y 
		# directions: ↖↑↗ (no queens below) 
		if board[r] in (x - (y-r), x, x + (y-r)): 
			return True 
	return False

def place_queens(board: list, y=0) -> bool: 
	if y == len(board): 
		return True # all queens already placed 
	for x in range(len(board)): 
		if not under_attack(board, x, y): 
			board[y] = x # (x, y) is safe: place a queen 
			
			# try and place queens in the following rows 
			if place_queens(board, y + 1): 
				return True 
				
			board[y] = None # no luck, backtrack 
	return False
```
