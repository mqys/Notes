# Content

---
分类:
- DSL(Domain-specific language): 领域专用语言, eg: shell script, UML, XML
- GPPL(General-purpose programming language): 通用编程语言, eg: c, java, python

---
# Part I 解析初步
## Chapter 2 基本解析模式
LL(1): L代表left-to-right, 第一个L代表从左到右的顺序解析输入内容, 第二个L代表下降解析时也按照从左到右的顺序遍历子节点. 1表示根据一个向前看词法单元决定解析方式.

LL(k): 能使用最多k个前向词法单元, 构建环形缓冲区.

Token: 词法单元.

使用文法DSL来构建语法解释器.

递归下降局限: 不能处理左递归, 即一开始就自引用.

## Chapter 3 高阶解析模式
使用回溯, 记忆, 语义信息进行解析

---
# Part II 分析语言
