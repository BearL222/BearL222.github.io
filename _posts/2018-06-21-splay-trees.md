---
layout: post
title: Splay trees
tags: data-structures, splay
category: data-structures
---
## What is Splay trees
### Definition
Splay tree is one kind of binary search trees in the circumstance that the recently accessed node will be accessed again. So, it has a basic operation: splay, which makes one node become the root.  

### Splay cases
There are 3 cases:
- x has no grandparent (zig)- x is LL or RR grandchild (zig-zig)- x is LR or RL grandchild (zig-zag)

### Operations

* After access(_i_):
	* Successful: splay at node containing i	* Unsuccessful: splay at last node on search path* After insert(_i_): 
	* splay at node containing i* After delete(_i_):	* Found: Let x be the node that was actually deleted; splay atthe node that was the parent of x	* Not found: Splay at last node on search path

### Example
<center>**Complete Splay example**</center>
![splay-tree-example](http://pair5904t.bkt.clouddn.com/2018-06-21-splay-intro/splay-tree-example.png)

## Complexity
The amortized time of insertion, access, deletion of each data structure is O(log n).

## Implementation
It is implemented with Python. [Github](https://github.com/BearL222/CS261p/tree/master/Project2)  
Note: insertion, access, deletion functions return a array sized 2, which contains the return value and a operation counter.
### Insertion
```
def insert(self, k):
    results = [None] * 2
    self.counter = 1
    new_node = SNode(k, None)
    if self.root is None:
        self.empty = False
        self.root = new_node
    else:
        # insert new node
        node = self.root
        parent = None
        lor = 0
        h1 = True
        h = 0
        while node is not None:
            h += 1
            self.counter += 1
            parent = node
            if k < node.value:
                lor = 0
                node = node.leftChild
            elif k > node.value:
                lor = 1
                node = node.rightChild
            else:
                # already exist
                h1 = False
                break
        self.height = max(self.height, h)
        if h1:
            # on the left or right side of parent
            if lor == 0:
                parent.leftChild = new_node
            else:
                parent.rightChild = new_node
            new_node.parent = parent

            # splay
            self.splay(new_node)
        else:
            self.splay(node)
    results[1] = self.counter
    return results
```
### Access
```
def search(self, k):
    results = [None] * 2
    self.counter = 1
    node = self.root
    if self.root is not None:
        last = node
        while node is not None:
            self.counter += 1
            last = node
            if k < node.value:
                node = node.leftChild
            elif k > node.value:
                node = node.rightChild
            else:
                break
        if node is not None:
            self.splay(node)
        else:
            self.splay(last)
    results[0] = True if node is not None else False
    results[1] = self.counter
    return results
```
### Deletion
```
def delete(self, k):
    results = [None] * 2
    self.counter = 1
    success = False
    if self.root is not None:
        node = self.root
        last = None
        while node is not None:
            self.counter += 1
            last = node
            if k < node.value:
                node = node.leftChild
            elif k > node.value:
                node = node.rightChild
            else:
                success = True
                break
        if success:
            # find it, then delete it
            p = node.parent
            self.true_delete(node)
            self.splay(p)
        else:
            self.splay(last)
    results[0] = success
    results[1] = self.counter
    return results
```
### Other utility functions (signatures)
```
rotate_right(self, parent) # do left rotation
rotate_left(self, parent) # do right rotation
true_delete(self, node) # just delete this node

def splay(self, node):
    self.counter += 1
    if node is None:
        return
    while node.parent is not None:
        self.counter += 1
        if node.parent.parent is None:
            # zig
            if node is node.parent.leftChild:
                self.rotate_right(node.parent)
            else:
                self.rotate_left(node.parent)
        elif node is node.parent.leftChild and node.parent is node.parent.parent.leftChild:
            # zig-zig left
            self.rotate_right(node.parent.parent)
            self.rotate_right(node.parent)
        elif node is node.parent.rightChild and node.parent is node.parent.parent.rightChild:
            # zig-zig right
            self.rotate_left(node.parent.parent)
            self.rotate_left(node.parent)
        elif node is node.parent.rightChild and node.parent is node.parent.parent.leftChild:
            # zig-zag left
            self.rotate_left(node.parent)
            self.rotate_right(node.parent)
        elif node is node.parent.leftChild and node.parent is node.parent.parent.rightChild:
            # zig-zag right
            self.rotate_right(node.parent)
            self.rotate_left(node.parent)
```
## Performance
### Testing method
In this lab, each data structure’s performance is tested on insertion, search, deletion operations. Data set sizes from 100, 200 to 5000. Elements in data set are chosen randomly. The testing program runs around 50 times to get the average result. The results are numbers of operations instead of time.  
Plots below show 3 curves with different colors. Blue one means one insertion operation, red one means one search operation and green one means one deletion operation. X axis is the number of nodes in the tree when searching, inserting or deleting. Y axis is the cost to do the operation.

### Plot
![performance-splay1](http://pair5904t.bkt.clouddn.com/2018-06-21-splay-intro/performance-splay1.png)
![performance-splay1](http://pair5904t.bkt.clouddn.com/2018-06-21-splay-intro/performance-splay2.png)

In case that deletion operation curve is not obvious in the first plot, I put the second plot here.

## Conclusion
We can see from the plots in Performance part that the performance of each operation is O(log n).  
For Splay tree, search and insertion costs are similar and they are higher than deletion cost. I think it is due to the order of sequence I use. It affects whether the node to delete is close to leaf or root. If it is close to the root, the cost is lower.
## Referrence
Notes from Prof. Michael B. Dillencourt  Wikipedia