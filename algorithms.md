

## 说明

本文档用于记录阅读algorithms(4th)时的一些思想记录，学习材料包括书和coursa上的课程视频

### Union-find

数组存储，下标为元素编号，值为父节点。Union操作为更改当前节点的根节点的父节点为合并节点的根节点。

通过增加权重数组，记录每个独立集合的元素个数，保证树的平衡。

路径压缩：将节点直接链接到根节点，得到扁平化的树。

### ThreeSum

可以进行数据预处理，sort，使用二元组，对第三个元素进行binarySearch。缩减计算时间至N^2logN。

### Dijkstra双栈算数表达式求值算法

数值栈和符号栈。

忽略左括号，遇到右括号，弹出两个数值和一个运算符号。

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

### BinarySearchTree

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

### BalancedSearchTree

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
      = insert into 2-node(black link,no childern,bottom): 
      	- add to left: 1. add 2. set red 
          - add to right: 1. add 2. set red 3. rotation
      = insert into 3-node:
      	- larger: 1. add up right 2. turn black
          - smaller: 1. add down left 2. rotate right 3. turn black
          - between: 1. add dow right 2. left rotate 3. right rotate 4. turn black
      ```
      
    - deletion: hard (replace with BST deletion,not so good)
  
- ***B-trees***
  
  - external nodes contain client keys
  - internal nodes contain key copies to guide search
  - insertion: insert, if overload then split