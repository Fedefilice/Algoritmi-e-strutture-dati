Sequenza finita e ordinata di elementi
- **Ordinata** significa che ogni elemento ha una posizione specifica nella lista

Head: beginning of a list
Tail: end of a list

### Methods: 
- `Empty` → true when the list has no elements
- `Length` → number of elements stored
- `Insert` 
- `Remove` 
- Access a value(read or change)
- Create and clear the list
- Access to pervious element from the current one

# Implementation
List is a class template with one parameter: E, which is a placeholder for the element that has to be stored in the list

- A key concept is the current position. Every single action in the list is performed in the current position
	{20, 23 | 12} → vertical bar indicates that the current position is on the value 12, at its right.
	using insert with value 8 will change the list to be 
	{20, 23 | 8, 12}

---

## ADT implementation:

```C++
template <typename E> class List { // List ADT
private:
	void operator =(const List&) {} // Protect assignment
	List(const List&) {} // Protect copy constructor
public:
	List() {} // Default constructor
	virtual ˜List() {} // Base destructor
	
	// Remove all contents from the list.
	virtual void clear() = 0;
	
	// Insert an element at the current location. 
	// The client must ensure that the list’s capacity is not exceeded.
	// item: The element to be inserted
	virtual void insert(const E& item) = 0;
	
	// Append an element at the end of the list. 
	virtual void append(const E& item) = 0;
	
	// Remove and return the current element.
	virtual E remove() = 0;
	
	// Set the current position to the start of the list
	virtual void moveToStart() = 0;
	
	// Set the current position to the end of the list
	virtual void moveToEnd() = 0;
	
	// Move the current position one step left.
	virtual void prev() = 0;
	
	// Move the current position one step right.
	virtual void next() = 0;
	
	// Return: The number of elements in the list.
	virtual int length() const = 0;
	// Return: The position of the current element.
	virtual int currPos() const = 0;
	
	// Set current position.
	// pos: The position to make current.
	virtual void moveToPos(int pos) = 0;
	
	// Returns a pointer to the current element
	// you can ask only if the element exsists
	virtual const E& getValue() const = 0;
	
};

```

``` C++
//Print all elements in the list

//it can become linear serch
//bool find(List<int>&L, int toSearch){
for (L.moveToStart(); L.currPos() < L.length(); L.next()){
	element = L.getValue();
	std::cout << L.currPos() << ", " << element;
	
	//if (toSearch == element) return true;
}
```

---
## Array-based list implementation:
(**AList**)

- defaultSize → max element of the array (used if no parameter is given)

Private attributes in the AList:
- listArray → array that holds the elements
- maxSize 
- listSize
- curr → stores the current position

```C++
template <typename E> 
class: AList: public List<E>{
private:
	int maxSize; 
	int listSize;    //num of item in the list atm
	int curr;   //position of current element
	E* listArray;    //Array that holds elements of list

public: 
AList (int size = defaultSize){    //constructor
	maxSize = size
	listSize = curr = 0;
	listArray = new E[maxSize];
	}
˜AList() {delete [] listArray; }    //destructor

void clear(){    //reinitialization
	delete[] listArray;
	listSize = curr = 0;    //reset size
	listArray = new E[maxSize];
}

//insert element at current position
void insert(const E& element){
	//assert -> if expression false print statement
	Assert(listSize < maxSize, "List capacity exceeded");
	for (int i = listSize; i>curr; i--)//shift element up 
	{
		listArray[i] = listArray[i-1];  //make room
		listArray[curr] = element;
		listSize++;    
	}
}

//append at end of list
void append(const E& element){
	Assert (listSize < maxSize, "List capacity exceeded");
	listArray[listSize++] = element;
}

//remove and return curr element
E remove(){
	Assert((curr>=0) && (curr < listSize), "No element");
	E element = listArray[curr]; //copy element
	for (int i = curr; i < listSize-1; i++){
		listArray[i] = listArray[i+1];
		//shift elements after the one to cancel down
	}
	listSize--;
	return element;
}

void moveToStart() {curr = 0}  //reset position
void moveToEnd() {curr = listSize;} // move to end

//sposta indicatore indietro di una posizione
void prev() {if (curr != 0) curr--;} 
//sposta indicatore avanti
void next() {if (curr < listSize) curr++;}
//return list size
int length() const {return listSize;}
//return current pos
int currPos() const {return curr;}

//set current position to pos
void moveToPos(int pos){
	Assert ((pos >= 0) && (pos <= listSize), "Pos out of range");
	curr = pos;
}

//return current element
const E& getValue() const {
	Assert ((curr>=0)&&(curr<=listSize), "No current element");
	return listArray[curr];
}
};
```

### Analysis:
- because all elements have an index of the array, **append** operation takes  $T(n)=\Theta (1)$
- **insert** or **remove** of an element at the head of the list must shift all the elements. it takes $T(n)=\Theta (n)$
- **constructor**, **destructor**, **clear** can be more expensive #domanda 

--- 

## Linked list implementation:
un albero è una linked list con piu connessioni tra gli elementi

A node is a distinct object (cell in array)
A linked list is made up of nodes linked together → we create a list node class "Link"
![[LListi.png| 300]]
- value stored in a pointer variable is the arrow pointing to something
- / (in C++ is NULL), is used for a pointer that points nowhere
- | is used to indicate the current position (the element at right of the |)


This class can be used for stack and queue implementations #Link_class
```C++
template <typename E> class Link{
public:
	E element; //store the value of the element
	Link *next; //pointer to next node
	//its a one way list!
//constructors
	Link (const E& elemval, Link* nextval = NULL){
	element = elemval;
	next = nextval; 
	}
	 
	Link(Link* nextval = NULL){ //no initial value
	next = nextval; }
}
```
The methods are public(breaking encapsulation rules) because the Link class should be implemented as a private class of the linked list

- LList makes use of pointer (dynamic memory allocation)

```C++
// Linked list implementation 
template <typename E> class LList: public List<E>{
private:
link<E> *head;   //pointer to first element
link<E> *tail;   //pointer to last element
link<E> *curr;   //access to current element
int cnt    //size of list

void init(){    //initialization helper
	curr = tail = head = new Link<E>;
	cnt = 0;
}

void removeall(){   
	while (head != NULL){
		curr = head
		head = head->next:
		delete curr;
	}
}

public:   //constructor
LList(int size=defaultSize){
	init();
}
˜LList() { removeall(); }   //destructor
void print() const;    //print list content
void clear() { removeall(); init();}   //clear list

//insert value in current position
void insert (const E& it){
	curr->next = new Link<E> (it, curr->next);
	if (tail == curr) tail = curr->next; //creates new tail
	cnt++;
}

void append(const <E>& it){
	tail = tail->next = new Link<E>(it, NULL);
	cnt++
}

//remove and return curr element
E remove(){
	Assert (curr->next != NULL, "no element");
	E it = curr->next->element;   // Remember value
	Link* ltemp = curr->next;     // Remember link node
	if (tail == curr->next) tail = curr; // Reset tail
	curr->next = curr->next->next; // Remove from list
	delete ltemp; // Reclaim space
	cnt--;
	return it;
}
// Move curr one step left
void prev() { 
	if (curr == head) return; //no prev, return
	Link<E>* temp = head;  //creo elemento temporaneo
	//check se elem successivo a temp = curr, se si allora curr = temp
	while (temp->next!=curr) temp=temp->next; 
	curr = temp;
}

//move curr one step right
void next() { 
	if (curr != tail) curr = curr->next; 
}

// Return the position of the current element 
int currPos() const { 
Link<E>* temp = head; 
for (int i=0; curr != temp; i++){ 
	temp = temp->next;} 
return i;
}

//move curr in position "pos"
void moveToPos(int pos) { 
	Assert ((pos >= 0) && (pos <= cnt), "Position out of range"); curr = head; 
	for(int i = 0; i<pos; i++) curr = curr->next; 
}

//return curr
const E& getValue() const{
	Assert (curr->next != NULL, "no value")
	return curr->next->element
}
};
```

quando la lista è vuota non abbiamo head, tail, curr → una soluzione è quella di creare il primo nodo in modo speciale. header node diventa un nodo come ogni altro, ma con valore ignorato. in piu non è considerato elemento della lista.
![[LList.png| 400]]

### Analysis:
- insert, remove $\Theta(1)$
- move to pos $\Theta(i)$ con i = posizione

## Comparison of list implementation:
AList have a predetermined sized that cannot be enlarged $S(n) = \Omega(n)$
LList need just the space required for the object in the list $S(n) = \Theta(n)$

AList don't waste space for individual elements
LList require a pointer for every node

formula for space efficiently
P = pointer size (4 bytes)
E = size data element
D = max number of list that can be stored in array

space required for AList → DE
space required for LList → P+E

solve for n elements

$n> \frac{DE}{P+E}$

Generally LLists are better when implementing lists whose number of elements varies widely or is unknown. 
AList are generally more space efficient when the user knows in advance approximately how large the list will become