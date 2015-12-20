

## 说明

本文档用于记录阅读algorithms(4th)时的一些思想记录，学习材料包括书和coursa上的课程视频

## ##Part I
### Union-find

数组存储，下标为元素编号，值为父节点。Union操作为更改当前节点的根节点的父节点为合并节点的根节点。

通过增加权重数组，记录每个独立集合的元素个数，保证树的平衡。

路径压缩：将节点直接链接到根节点，得到扁平化的树。

### ThreeSum

可以进行数据预处理，sort，使用二元组，对第三个元素进行binarySearch。缩减计算时间至N^2logN。

### Dijkstra双栈算数表达式求值算法

数值栈和符号栈。

忽略左括号，遇到右括号，弹出两个数值和一个运算符号。

--------------------------------
## ---SORT---

### Elementary Sort

- **Selection Sort:** interate rest, find the smallest, put it in place
- **Insertion Sort:** swap the current and its pre till current in the right place
- **ShellSort:** 间隔的插入排序，确定距离，在间隔h的距离上进行插入排序；缩小距离直到距离为1；关键点为距离的确定，建议（3x+1）
- **Shuffling:** 构建随机数组。对于位置为i的元素，产生随机数组0-i，交换，++i
- **Convex Hull:** 凸包：找到右下点，链接其他点，顺时针排序，逐个添加，如果新加入的在前一条连线的左侧，则保持啦顺时针的位置，可以作为凸包的点，若不能保持顺时针，则删去该点

### MergeSort

分治思想，辅助数组拷贝两个排序好的数组，归并到原数组，构成一个排序好的大数组

辅助数组不要动态创建，开始时创建，和原数组大小一样，避免动态创建销毁。

自顶向下与自底向上

**stability:** same key, keep the former order

- stable sort: insertion, merge
- not stable sort: selection, shell

### QuickSort

预先shuffle可以保证效率，避免最坏情况

- 3-way quicksort: duplicate keys

### Priority queue

- **binary heap:**
  
  ``` 
  - start from 1 
  - opertion: swim(上浮) sink(下沉)
  - insert: add to tail, then swim up
  - delete: exchange top and tail, then top sink down, delete tail
  ```
  
- **heap sort:**
  
  ``` 
  1. build heap order:
  	- start from N / 2 to 1,  sink()
  2. sort:
  	- echange N with top, --N
  	- sink(top)
  	- loop
  ```
  
- event-driven simulation:
  
``` 
  - predict collision event
  - put event into priority queue
  - deal with event
  - change model and delete that event from pq
```

## ---SEARCH---

### Symbol table

key-value

- implementation:
  
  ``` 
  - unordered list
  - ordered array : binary search(two arraies: one key, one value), insert cost all larger key to move
  ```

### Binary Search Tree

could be used to implement symbol table efficiently

all insertion will be at the leaf

**deletion:** 

- no / one child: replace with child
  
- two child:
  
  ``` 
  1. find successor x -> the smallest in the right subtree
  2. delete the x in the right subtree
  3. put x to replace the deletion
  4. ( delete smallest ): smallest in the left with no left child, so replace with its right subtree
  ```

### Balanced Search Tree

- ***2-3 Search Trees***
  
  - nodes:
    
    - 2-node: 1 key, 2 children(less, larger)
    - 3-node: 2 keys, 3 children(less, middle of two keys, larger)
    
  - **Insertion**:
    
    - insert into 2-node at bottom: replace 2-node with 3-node
      
    - insert into 3-node at bottom:
      
      ``` 
      1. add into the 3-node to become temporary 4-node(3 keys) 
      2. move middle to parent
      3. split the other two keys into 2-node
      4. if parent bocome 4-node, repeat the process(may add height)
      ```
    
  - **implementation** may be too complicated, so we need a little transformation (red-black tree)
  
- ***Red-Black Trees***
  
  - left-leaning red-black tree:
    
    - red links(only left) two nodes as a 3-node
      
    - black links two common nodes
      
    - *search*: same as BST 
      
    - *representation*: bool color(the link points to it)
      
    - *left/right rotation*: right red link rotate to left...
      
    - *color flip*(split 4-node): just change colors
      
    - **insertion:** 
      
      ``` 
      insert into 2-node(black link,no childern,bottom): 
      	- add to left: 1. add 2. set red 
          - add to right: 1. add 2. set red 3. rotation
      insert into 3-node:
      	- larger: 1. add up right 2. turn black
          - smaller: 1. add down left 2. rotate right 3. turn black
          - between: 1. add dow right 2. left rotate 3. right rotate 4. turn black
      ```
      
    - deletion: hard (replace with BST deletion,not so good)
  
- ***B-trees***
  
  - external nodes contain client keys
  - internal nodes contain key copies to guide search
  - insertion: insert, if overload then split

### Geometric Application of BSTs

- 1 d range search
  - search keys in a range
- line segment intersection
  - search from left to right 
  - put the node's y into a BST
  - delete y when this y repeats
  - meet more one, range search and delete
- ***kd trees***
  - 2 d range search
  - 2 d tree
    - recursively partition plane into two halfplanes
    - h and v partition take tree level turns 
    - h node: left->below right->above
    - v node: left->left right->right
    - application: closest neighbor
  - kd tree
    - recursively partition k-dimensional space into 2 halfspaces
    - application: n-body simulation
- interval search trees
  - data structure hold a set of intervals(lo, hi)
  - left endpoint as BST key
  - store max endpoint in subtree rooted at node
  - insertion: BST insert, update max endpoint
  - search for intersection
- Rectangle intersection
  - sweep vertical line from left to right
  - review line segment intersection method

### HashTable

default implement: memory address

java: `hashCode()` all objects

collision:
  - separate chaing: 
    - use linked list
  - linear probing:
    - bigger size of array
    - check the next postion till an empty place
    
### Symbol Table Applications
- Set
- Dictionary Client
- Indexing Client
- Sparse Vector

## ##Part II
## -----GRAPH-----
### Undirected Graphs

- graph representation:
  - adjacency-matrix graph: v * v boolean array
  - adjacency-list graph: vertex-indexed array of lists
  
In pratice: use adjacency-list for graph tend to be sparse

- Depth-First search:
  - recursive func
  - marked[] to record whether visited
  - edgeTo[] to record path, store the prevertex

- Breadth-First search:
  - use queue

- Connected components:
  - dfs
  - union-find
  - cc[] to record which set this node should be 
  
- challenges:
    - is a graph bipartite:
      - means can we divide the graph into two sets
      - the v in set1 only connects to vertexes in set2
    - find a cycle 
    - ...
    
### Directed Graphs

- application: java GC
- dfs: search
- bfs: shortest path

- Topological Sort(拓扑排序)
  - DAG: directed acyclic graph (no cycle)
  - all the edges point upwards
  - dfs, stack
  - application: precourses needed to take
  
- Strongly-connected components
  - def: v->w w->v, directed ways 
  - kosaraju-sharir algorithm:
    1. compute reverse postorder in ***reverse graph*** (topological order)
    2. run dfs in graph in the order computed by step1 

### Minimun Spanning Trees

- Greedy Algorithms
  - cut property: cut the node into two sets
    - the shortest edge between two sets must be in the MST

- Kruskal's Algorithm (no cycle property, add edges)
  - sort the edges
  - add the edge to MST in ascending order if no cycle created
  - judge cycle: 
    - use Union-Find
    - if the V and W are all in the same set then there is a cycle

- Prim's Algorithm (add vertex)
  - start with vertex 0, add this vertex into the MST
  - add the shortest edge between the current MST and the rest vertex
  - until v-1 edges
  - lazy implementation:
    - 1 use PQ to store the edges connected to the vertex in the current MST
    - 2 pick (the shortest && W not in MST) edge
    - 3 add W to MST, and add edges connected to W into the PQ
    - use marked[] to judge whether this vertex in the MST
  - eager implementation
    - difference against lazy implementation:
      - the edges in the PQ
      - when add W, do not add all edges connected to W into the MST
      - if W-X, X not in MST, then add this edge
      - else, compare the edge existed in MST having X, add the shorter one
    - only keep one edge having the vertex not in the MST
    - and refresh it to keep it remianing the shortest one

### Shortest Paths
- Edge relaxation(松弛)
```java
 private void relax(DirectedEdge e)
 {
    int v = e.from(), w = e.to();
    if (distTo[w] > distTo[v] + e.weight())
    {
      distTo[w] = distTo[v] + e.weight();
      edge[w] = e;
    }
 }
```

- Dijkstra's Algorithms (nonnegative weights)(one src to all des)
  - consider vertices in increasing order of distance from s
  - add the vertex and relax all edges pointing from that vertex
  - compare Prim's:
    - Prim's: cloest to the tree
    - Dijkstra's: cloest to the source
    
- Edge-Weighted DAGs (no cycle)
  - consider vertices in **topological** order
  - relax all edges pointing from that vertex
  - longest path: negate all weights then find shortest paths
    - application: parallel job scheduling solution

- negative weights
  - Bellman-Ford algorithms(no negative cycle):
    - repeat V times: relax all E edges
    - improvement: use queue to maintain the vertices whose distTo[] changed
    - could find negative cycle 
    
### Maximum Flow

- Ford-Fulkerson Algorithm
  - find an **undirected** path from s to t
  - increase flow on forward edges(not full)
  - decresse flow on backward edges(not empty)

- Mincut problem
  - cut s and t into two sets
  - Flow-value lemma.
  - value of the maxflow = capacity of mincut
  
### Radix Sorts (String[])
- JAVA: String, StringBuilder(mutable)
  - String: char[], offset(start pos), lenght
  - subString(): change the offset and lenght, same char[]
  
- Key-Indexed Counting
  - count the frequencies
  - compute cumulates: count[]: store the start index of the char
  - move items: move to aux[], add one to the count[i]
  - copy back
  
- LSD Radix Sort(least-significant-digit-first)
  - consider char from right to left
  - use key-index counting inside
  
- MSD Radix Sort
  - from left to right
  - recurive do the sort each char
  - can sort Strings of different length

- 3-way radix quicksort
  - partition into three sets: less, equal, greater
  
- suffix array  
  - generate the suffix array, then radix sort
  - longest repeated substring (huge string)
    - use space for reducing time
    - suffix array, radix sort the array, 
      calcu the longest char between neighboring suffix array
      