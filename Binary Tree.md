Albero con in cui ogni nodo ha al massimo due figli
![[Albero binario pieno.png | 300]]

Tree structures permit efficient search and insert at the same time(impossible w/list structures)

In this case there are 2 important types of trees:
**a.** Full binary tree: tree in which every node can be internal with two non-empty children or a leaf.
**b.** Complete binary tree: fill the levels from left to to right. 
	at $d$ height, all level are full, one exception possibly being the last $d-1$ level
![[full and complete bst.png]]

## Full binary tree theorem:
we might require a different amount of space for internal nodes and for leaf nodes. But in a generic tree there is not a fixed percentage of leaf nodes in comparison to internal nodes.
The upper bound (O), occurs only in the full binary tree. 

"*The number of leaves in a non-empty full binary tree is one more than the number of internal nodes.*"

**Proof by induction:**
We reduce from an instance of size $n$ to an instance of size $n − 1$ that meets the induction hypothesis.

- Base case: 
	n = 0, a non-empty tree with zero internal nodes has one leaf node.
	n = 1, a full binary tree with one internal node has two leaf nodes
- Induction Hypothesis: 
	We assume that any full binary tree T, containing $n-1$ internal nodes has $n$ leaves
- Induction Step:
	Given a $T$ tree with $n$ leaves:
	select an internal node $I$ with 2 leaf node children.
	remove the leaf node children obtaining $T'$,
	it has $n-1$ internal nodes and leaves
	restoring $T$, we obtain $(n-1)+$2 leaves,
	thus $T$ has $n+1$ leaf nodes and n internal nodes

### Extension theorem for empty subtrees:
"*The number of empty subtrees in a non-empty binary tree is one more than the number of nodes in the tree.*"

related: [[Tree]]

## Binary Tree Node ADT:

There are different activities related to nodes rather than trees, so they shall be implemented as separate classes

```c++
template <typename E> class BinNode {
public:
	virtual ˜BinNode() {}

	//return node's value
	virtual E& element() = 0;
	//set node's value
	virtual void setElement(const E&) = 0:

	// Return the L child 
	virtual BinNode* left() const = 0; 
	// Set the L child 
	virtual void setLeft(BinNode*) = 0;

	// Return the R child 
	virtual BinNode* right() const = 0; 
	// Set the R child 
	virtual void setRight(BinNode*) = 0;

	// Return true if the node is a leaf, false otherwise 
	virtual bool isLeaf() = 0;
};
```

--- 
## Binary Tree node simple implementation:
##### ---pointer---

- By definition a binary tree node has two children, but one or both can be empty.
- A node contain a value.
- A common implementation have pointers to the children

An important decision in the design of a pointer-based node implementation is whether the same class definition will be used for nodes and leaves. 
if Yes → simpler implementation but may lead to inefficient use of space

```c++
//simple binary tree node implementation
template <typename Key, typename E>
class BSTNode : public BinNode<E>{
private:
	key k;    // node's key
	E it;     // node value
	BSTNode* lc;     // pointer to L child
	BSTNode* rc;

public:
	//constructor without initial value
	BSTNode () {lc = rc = NULL}
	//constructor w/ initial values
	BSTNode(Key K, E e, BSTNode* l = NULL, BSTNode* r = NULL){
		k = K;
		it = e;
		lc = l;
		rc = r;
	}

	˜BSTNode() {}

	E& element() { return it; }    //return value
	void setElement (const E& e) { it = e }    //set 
	
	Key& key() { return k; }
	void setKey(const Key& K) { k = K; }

	// set and return R e L children
	inline BSTNode* left() const { return lc; } 
	void setLeft(BinNode* b) { lc = (BSTNode*)b; } 
	
	inline BSTNode* right() const { return rc; } 
	void setRight(BinNode* b) { rc = (BSTNode*)b; }

	bool isLeaf() {return (lc == NULL) && (rc == NULL);}
};
```

---

we use inheritance. 
VarBinNode → abstract node base class
LeafNode, IntlNode → children class

```c++
class VarBinNode { 
public: 
	virtual ˜VarBinNode() {} 
	virtual bool isLeaf() = 0; 
};

class LeafNode : public VarBinNode {
private: 
Operand var;    //operand = tipo dato

public: 
LeafNode(const Operand& val) { //constructor
	var = val; 
}
bool isLeaf() { return true; }
Operand value() { return var; }   
void traverse() { cout << "Leaf: " << value() << endl; }
};

class IntlNode : public VarBinNode { 
private: 
	VarBinNode* lc; 
	VarBinNode* rc; 
	Operator opx; 

public:
IntlNode(const Operator& op, VarBinNode* l, VarBinNode* r) { 
	opx = op; lc = l; rc = r;  // Constructor
	}

	bool isLeaf() { return false; }
	VarBinNode* left() { return lc; } 
	VarBinNode* right() { return rc; } 
	Operator value() { return opx; } 

	void traverse() { // Traversal behavior for internal nodes 
	cout << "Internal: " << value() << endl; 
	if (left() != NULL) left()->traverse(); 
	if (right() != NULL) right()->traverse(); 
	} 
};

// Do a preorder traversal 
void traverse(VarBinNode *root) { 
if (root != NULL) root->traverse(); 
}
```

---
#treeTrasversal

In code is written as a recursive function

```c++
//preorder traversal
template <typename E>
void preorder(BinNode<E>* root){    //root = input node, each node can be viewed as a root of a subtree
	if (root == NULL) return; //empty subtree, do nothing
	visit(root);    //perform action
	preorder(root-> left());
	preorder(root-> right());
}    //it can make a recursive call on an empty children, but other version are less effective.
```

---
# Binary Tree Aleotti:

è formata da diversi metodi:

PRIVATE
1. `Insert`: inserisce un nuovo elemento nell'albero binario nella posizione appropriata in base al valore dell'elemento (più grande della radice nel sottoalbero DX e viceversa).
    
2. `traverse`: visita in postordine e stampa gli elementi.
    
3. `traverse_preorder_NR`: visita in preordine.
    
4. `traverse_levelorder_NR`: visita level order: attraversa da Sx a Dx tutti i nodi per livelli. (non c'è visita in order)
    
5. `count_elements`: 
6. `tree_height`: 
    
7. `max`: trova il valore massimo nell'albero.

PUBLIC
1. `AddItem`: usa insert. nel public.
    
9. `traverse`: visita, si puo decidere nel file.h quale fare.
    
10. `count`: Questo metodo restituisce il numero di elementi presenti nell'albero binario.
    
11. `height`: Questo metodo restituisce l'altezza dell'albero binario.
    
12. `createTournament`: trova il massimo elemento

