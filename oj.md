---
## 算法题
解题思路:
- 举例法: 具体化问题, 举具体的例子, 分析其中的规律
- 模式匹配法: 与现有问题进行类比
- 简化推广法: 修改约束条件, 先解决简化版本
- 简单构造法: 从最基本的情况开始, 递推发现规律
- 数据结构头脑风暴: 尝试数据结构的列表

考虑要素:
- 多用数据结构
- 适当重用代码
- 模块化
- 灵活, 健壮
- 错误检查

注意事项:
- 边界条件、特殊输入（NULL，空字符串），错误处理
- 程序逻辑的起点, 方向 (图形化)
- 操作链表, **函数的返回值为空时**传入的链表头结点应该使用指向头结点指针的指针(即为头指针的地址`LinkNode** head`) \[或是使用头指针的引用`LinkNode*& head`],否则在头结点为空的时候,因为传值参数,不能插入成功. 若函数返回值为指针类型, 则直接使用头指针

## C++ 中动态开辟二维数组 (做题常用)
```
// way 1 - new 与 delete
    //动态开辟空间  
    int **p = new int*[m]; //开辟行  
    for(int i = 0; i < m; i++)  
        p[i] = new int[n]; //开辟列
     //释放开辟的资源  
    for(i = 0; i < m; i++)  
        delete[] p[i];  
    delete[] p
// way 2 - vector
    vector<vector<int> > p(m,vector<int>(n));            
```

## C++ 中输出固定长度有填充位数字
```
printf("%04d", num);

#include<iomanip>
cout << setw(4) << setfill('0') << num << endl;
```

## C++ 中输出精确到某位的浮点数
```
double d = 11.111;
printf("%.1f", d); // 精确到一位小数
```

--- 
# Notes on leetcode (from leetcode/README.md)
* think before writing the code!!!
  
* 1.find the common way 2.find the break point 3.rebuild the code
  
* 循环遍历耗时太长，可用空间换时间，使用hash来进行直接寻找，不需要循环访问。(Two_Sum)
  
* 对null或者0的情况可以预处理排除，再对有内容的情况进行分类分析
  
* **最长回文串**：Manacher算法本质是中心扩展，分析了中心扩展时可以简化的计算部分（先字符串预处理，消除奇偶性）
  
* 单链，两点因子，一般不需要双重循环来遍历所有情况，试着分析问题特征，跳过不必要的计算
  
* **单链表常用技巧：**两个指针，增加头节点便于统一操作
  
* **按层遍历树：**
  
  ``` 
  1. add NULL to the queue, and iterate to the NULL, level up, add another NULL, be careful with the end case
  2. recursive with depth paremeter 
  3. record the num of node in the queue, then iterate num times as a round/level
  ```

* 联系图形，考虑问题

* 图形题目，分别考虑x,y， 分解，而不是当作整体考虑

* bit manipulation: usage of XOR, consider one bit, then the whole number
  - common trick: double XOR means nothing 
	- [single number](./singleNumber.cc)
	- [single numberII](./singleNumberII.cc)
	- [single numberIII](./singleNumberIII.cc)

* 分析结果的构成要素，逐个找到各个要素的求解方法

* Binary Tree Traversal, use O(1) space, no stack(morris traversal):
```
change the right child of predecessor to cur and change it back when get to it second time
rules:
  1. if the cur->left is NULL, cur = cur->right;
  2. if cur->left != NULL, find the predecessor(rightest of left subtree) 
    1) if predecessor->right == NULL, pre->right = cur, cur = cur->left
    2) if pre->right == cur, pre->right = NULL, cur = cur->right
  3. goto 1.
```             

* linked list cycle: 
	- two pointers: fast one and slow one, if the fast catches the slow then there is cycle

* use tables to record situations when a lot of cases need to be solved
    - [Integer To Roman](./integerToRoman.cc)

* divide and conquer:
    - divide the case into two parts: whether containing the mid 
    -  [Maximum Subarray](./maximumSubarray.cc)

# Notes on lintcode (from lintcode/README.md)
* KMP算法：关键是减少匹配时回退的移动位数，回退移动位数根据已经匹配的字符串的特征进行计算，其特征属性为前后缀的最长公有元素; next数组计算，考虑递推动态规划(dynamic programming)，k与k-1的关系 [site](http://www.cnblogs.com/c-cloud/p/3224788.html)
* ***动态规划：***考虑递归与状态表,通过保存先前状态来减少后续计算，关键是状态转移公式，注意迭代时计算顺序，保证先前状态已经计算完成
* 不定区间先固定一方，考虑确定区间内问题
* ***增长区间遍历：***设定区间范围的时候，设置终止指针，不是开始指针，将问题范围限定在已知范围内    
