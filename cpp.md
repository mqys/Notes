## notes on c++

### 虚函数表
<http://coolshell.cn/articles/12165.html>
对象内存的开始位置保存虚函数表，先父类后子类，若多继承，则有多个虚函数表。如果子类有重载父类函数，则表中的函数地址更新为子类函数的地址。

深入：c++内存模型：<http://coolshell.cn/articles/12176.html>

### 类型转换
```
const_cast          // 去掉const或是volatile属性
static_cast         // 基类与子类，基本数据类型之间，void
dynamic_cast        // 安全的基类与子类之间的转换，必须要有虚函数，交叉转换返回NULL
reinterpret_cast    // 不同类型的指针类型转换
```

### `volatile`
- 易变性：从内存读取变量，而不会从寄存器直接读取
- 不可优化
- 顺序性：volatile变量间的操作不会被优化改变执行顺序，volatile变量与非volatile变量之间的操作可能被交换顺序

### `sizeof` operator not function
- `struct`: 空为 1， 字节对齐：大小为最宽基本类型的整数倍
- 数组：内存字节数，若为形参则返回指针字节数

### 0 or `NULL` and `nullptr`
```
#define NULL 0
//since C++11
#define NULL nullptr
```

### c++ notes 
- int to string `to_string()`

- ***复制构造函数***必须是传引用，否则复制实参会导致自调用死循环

- ***拷贝运算符***必须先检测是否是自赋值,否则内存操作可能出错

- 函数调用时，可能发生参数的隐式类型转换

- 函数类型包括参数类型和返回类型，类的成员函数还包括类名
  
- initialization: use `=` or `{}`
    - use `{}` to avoid conversions that lose infomation, cause error(like double to int)
    - `=` may cause implicit conversion, due to c compatibility

- scope:
    - local:        declaration to block end
    - class:        class start to class end
    - namespace:    declaration to namespace end

- `constexpr`: to be evaluated at compile time
    - 常量表达式中的函数必须被定义为`constexpr`, 该函数只能有`return`语句, `constexpr`函数可以接受变量

