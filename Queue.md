Coda o queue è una sequenza lineare e ordinata di elementi e si comporta secondo FIFO(First in First out)

è una struttura di tipo lista con accesso limitato ai suoi elementi

si comporta come la fila per un volo aereo, i nuovi arrivati sono dietro e la persona davanti è la prossima ad entrare

## Operazione supportate:
- `Insert/Enqueue`: aggiunge un elemento alla fine della coda
- `Delete/Dequeue`: Elimina l'elemento all'inizio della coda
- `First`: Restituisce l'elemento in coda dell'array/coda
-  `IsEmpty`: Controlla che la coda sia vuota, True = vuota

## Pseudocodice:
TIPO Coda:
DATI: sequenza S di n elementi
OPERAZIONI:
- isEmpty() → bool
	if (n == 0) return True 
	else return False 
- Enqueue(elemento e)
	aggiunge e alla coda di S
- Dequeue() → e 
	toglie l'elemento in capo a S e lo restituisce
- First() → e 
	restituisce l'elemento in coda di S

![[Queue.png | 300]]

---
# Array-based Queue:

- enqueue operations takes $\Theta(1)$ because you append the element at the end
- for having dequeue operation that takes $\Theta(1)$ we must not have the first element in the first spot of the array. When you dequeue you cancel the element without moving all the others.
	This implementation raises a space problem because now the queue can easily run out of space.
	solution: We see the array as circular, so the array can continue from last to first position organically
![[Array circular queue.png| 300]]
Too understand if the queue is empty we make the array of size $n+1$ and we allow only $n$ elements to be stored (so we can distinguish empty from full queue)

```c++
template <typename E> class AQueue: public Queue<E>{
private:
	int maxSize;
	int front;    //index of front
	int rear;     //index of rear
	E *listArray;
	
public:
	AQueue (int size = defaultSize){
	maxSize = size + 1;    //for empty slot
	rear = 0; 
	front = 1;
	listArray = new E[maxsize];
	}

	AQueue() { delete [] listArray; } 
	void clear() { rear = 0; front = 1; }

	void enqueue(const E& it){
	Assert(((rear+2) % maxSize) != front, "Queue is full");
		//if rear +2 = maxsize -> full
		rear = (rear+1) % maxSize;    //circular increment
	#domanda 
		listArray[rear] = it    //insert
	}

	E dequeue() {  
		Assert(length() != 0, "Queue is empty"); 
		E it = listArray[front]; 
		front = (front+1) % maxSize; // Circular increment
		return it;
	}

	const E& frontValue() const{
		Assert (length() != 0, "Queue is empty");
		return listArray[front];
	}
//A virtual function is a member function that is declared within a base class and is re-defined (overridden) by a derived class.
	virtual int length() const {
	return ((rear + maxSize) - front + 1) % maxSize;
	}
};
```

---

# Linked Queue:

- front and rear elements are pointers to the respective elements. 
	in the initialization they point to the header node (front always → header node)

```c++
template <typename E> class LQueue: public Queue<E>{
private: 
Link<E>* front;
Link<E>* rear;
int size;

public:
LQueue(int sz = defaultSize){
	front = rear = new Link<E>;
}

˜LQueue() { clear(); delete front; } 

void clear(){
	while(front-> next != NULL){
		rear = front;
		delete rear;
	}
	rear = front;
	size = 0;
}

void enqueue(const E& it){
	rear-> next = new Link<E>(it, NULL);
	rear = rear->next;
	size++;
}

E dequeue(){
	Assert(size != 0, "Queue is empty");
	E it = front-> next-> element;    //store the element in it
	Link<E>* Itemp = front-> next;    //creates a pointer pointing to the element to dequeue
	front-> next = Itemp-> next;    //update the pointer to the next element of the list before dequeueing
	if (rear == Itemp) rear = front;    //checks if there are no more element in the list (rear == itemp) if true queue is empty
	delete Itemp;    //effectively deleting the item
	size--;
	return it;
}
}
```

---

# Comparison:
all member functions require constant time.
Space wise it's the same as the stack implementation