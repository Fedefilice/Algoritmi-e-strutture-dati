Stack è una struttura di tipo lista in cui gli elementi possono essere inseriti o rimossi solo da un'estremità
- LIFO (Last in First out).
- Meno flessibile di una lista, ma efficiente e semplice da implementare

## Pseudocodice:
TIPO Pila:
DATI: sequenza S di n elementi
OPERAZIONI:
- `IsEmpty`() → bool
	if (n == 0) return True
	else return False
- `Push`(elemento e)
	aggiunge e come ultimo elemento di S
- `Pop`() → e
	toglie l'ultimo elemento di S e lo restituisce
- `Top`() → e
	restituisce l'ultimo elemento di S

![[Stack.png | 300]]

---
## ADT Implementation:
```c++
template <typename E> class Stack{
private:
	void operator = (const Stack&) {} //protect assignment
	Stack (const Stack&) {}  //protect copy constructor
public:
Stack(){}           //default constructor
virtual ˜Stack() {} //base destructor

//reinitialize the stack
virtual coid clear() = 0;

//push "it" element on top of stack
virtual void push(const E& it)= 0;
//remove
virtual E pop() = 0;
//return a copy of top
virtual const E& topValue() const = 0;

//return number of elements
virtual int length() const = 0;
}
```

---

## Array-based Stack implementation:
- listArray must be declared of fixed size when the stack is created
- size = size of listArray
- top = curr pos + number of element in the stack

AStack is a simplified version of the AList
Top element at n-1 pos its the most efficient setup, it causes:
- push, pop $\Theta(1)$

```c++
template <typename E> class AStack : public Stack<E>{
private:
	int maxSize;
	int top;
	E *listArray;

public;
	AStack (int size = defaultSize){
		maxsize = size;
		top = 0;
		listArray = new E[size];
	}
	˜AStack() { 
	delete []listArray; 
	}
	void clear() { top = 0; }
	//push
	void push (const E& it){
		Assert (top != maxsize, "Stack is full");
		listArray[top++] = it;
	}
	//pop
	E pop(){
		Asert(top != 0, "Stack is empty");
		return listArray[--top];
	}
	//return top element
	const E& topValue() const {
		Assert(top != 0, "Stack is empty"); 
		return listArray[top-1];
	}
	//length
	int length() const { return top; }
};
```

--- 

## Linked Stack implementation:
simplified version of linked list implementation

```c++
template <typename E> class LStack : public Stack<E>{
private:
	Link<E>* top;
	int size;
public:
	LStack(int sz = defaultSize){
	top = NULL;
	size = 0; 
	}
	˜LStack() { clear(); }
	
	void clear() {    //reinitialize
	while (top != NULL){
		Link<E>* temp = top;
		top = top->next
		delete temp;
		}
	size = 0;
	}
	void push (const E& it){
	top = new Link(it, top);
	size++;
	}
	
	E pop(){
	Assert(top != NULL, "Stack is empty");
	E it = top->element; 
	Link* ltemp = top->next; 
	delete top; top = ltemp; 
	size--; 
	return it;
	}
	
	const E& topValue() const { // Return top value 
	Assert(top != 0, "Stack is empty"); 
	return top->element; 
	}
	int length() const { return size; }
};
```

---

## Comparazione tra le due implementazioni:
- dal punto di vista dell'efficienza non ci sono vantaggi tra le due implementazioni
- dal punto di vista dello spazio utilizzato l'analisi è simile a quella delle liste
- se bisogna implementare due stacks, essi possono essere inseriti nello stesso array a patto che abbiano un rapporto di crescita inverso. 