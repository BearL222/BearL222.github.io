---
layout: post
title: Treap, an alternative for binary tree
tags: data-structures, treap
category: data-structures
---
## What is Treap
### Definition
Treap is Trees + Heaps. It is one kind of binary trees.  
Each node contains:  

* key value
* child pointer  
* priority value

The priority value is assigned when the node is created and it will not change. The value is chosen randomly from [0, 1].  
Treap is organized so that the data forms:

* binary search tree with respect to key values
* heap-ordered tree with respect to priority values

Note: high priorities are represented by high values.
### Example
![treap-example](http://pair5904t.bkt.clouddn.com/2018-06-19-treap-intro/Screen%20Shot%202018-06-19%20at%2013.50.17.png)
## Complexity

* The time complexity of insertion, access, deletion of each data structure is O(log n).  
* Expected number of rotation is <= 2.

## Pseudocode
### Access
```
Same as common binary tree
```
### Insertion
```
def insert(self, k):
	v = Insert k using standard binary tree insertion
	# v is a leaf node
	v.priority = random()
	while(v is not the root and v.priority > v.parent.priority):
		if v is a leaf child:
			rotate right(v.parent)
		else:
			rotate left(v.parent)

```
### Deletion
```
def delete(self, v):
	while v is not a leaf:
		if left(v) == None:
			rotate left(v)
		elif right(v) == None or v.left.priority > v.right.priority:
			rotate right(v)
		else:
			rotate left(v)
	delete the leaf node v

```
## Implementation
It is implemented with Python. [Github](https://github.com/BearL222/CS261p/tree/master/Project2)  
Note: insertion, access, deletion functions return a array sized 2, which contains the return value and a operation counter.
### Insertion
```
def search(self, k):
    results = [None] * 2
    self.counter = 1
    if self.empty:
        results[1] = self.counter
        return results

    node = self.root
    while node is not None:
        self.counter += 1
        if k < node.value:
            node = node.leftChild
        elif k > node.value:
            node = node.rightChild
        else:
            results[0] = node
            break
    results[1] = self.counter
    return results

```
### Access
```
def insert(self, k):
    results = [None] * 2
    self.counter = 1
    new_node = TNode(k, random.random(), None)
    if self.empty:
        self.empty = False
        self.root = new_node
    else:
        node = self.root
        parent = None
        lor = 0
        h1 = True
        while node is not None:
            self.counter += 1
            if k < node.value:
                parent = node
                lor = 0
                node = node.leftChild
            elif k > node.value:
                parent = node
                lor = 1
                node = node.rightChild
            else:
                h1 = False
                break
        if h1:
            if lor == 0:
                parent.leftChild = new_node
            else:
                parent.rightChild = new_node
            new_node.parent = parent

            # do some rotation
            v = new_node
            r = 0
            while v.parent is not self.root and v.priority > v.parent.priority:
                r += 1
                # print(r)
                if v is v.parent.leftChild:
                    self.rotate_right(v.parent)
                elif v is v.parent.rightChild:
                    self.rotate_left(v.parent)
    results[1] = self.counter
    return results
```
### Deletion
```
def delete(self, k):
    results = [None] * 2
    self.counter = 1
    return_node = self.search(k)
    v = return_node[0]
    if v is not None:
        while v.leftChild is not None or v.rightChild is not None:
            if v.leftChild is None:
                self.rotate_left(v)
            elif v.rightChild is None or v.leftChild.priority > v.rightChild.priority:
                self.rotate_right(v)
            else:
                self.rotate_left(v)
        self.true_delete(v)
    results[1] = self.counter
    return results

```
### Other utility functions (signatures)
```
rotate_right(self, parent) # do left rotation
rotate_left(self, parent) # do right rotation
true_delete(self, node) # just delete this node
```
## Performance
### Testing method
In this lab, each data structure’s performance is tested on insertion, search, deletion operations. Data set sizes from 100, 200 to 5000. Elements in data set are chosen randomly. The testing program runs around 50 times to get the average result. The results are numbers of operations instead of time.  
Plots below show 3 curves with different colors. Blue one means one insertion operation, red one means one search operation and green one means one deletion operation. X axis is the number of nodes in the tree when searching, inserting or deleting. Y axis is the cost to do the operation.
### Plot
![treap-performance](http://pair5904t.bkt.clouddn.com/2018-06-19-treap-intro/treap-performance.png)
## Conclusion
We can see from the plots in Performance part that the performance of each operation is O(log n).  
For Treap, cost of search is lowest because it is just like the binary tree search. Costs of other two operations are similar because their expected number of rotations is at most 2.
## Referrence
Notes from Prof. Michael B. Dillencourt  Wikipedia