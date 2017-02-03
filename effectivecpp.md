- 使用`explicit`禁止编译器执行非预期的类型转换
- `Foo f2 = f1`使用拷贝构造函数, 不是拷贝运算符
- 用户自定义类型, 不建议使用`pass-by-value`, 建议使用`pass-by-reference-to-const`

## Chapter 1 
- 使用`const, enum, inline`代替`#define`
- `const`与指针结合, 区分是所指物还是指针本身, `*`左->所指物, `*`右->指针

```
const char* p = "hello"; // non-const pointer, const data
char* const p = "hello" // const pointer, non-const data

// 迭代器
const std::vector<int>::iterator iter; // const iter, non-const data
std::vector<int>::const_iterator iter2; // non-const iter, const data
```
`const`成员函数:
- `const`对象调用`const`版本成员函数
- `const`成员函数不可以修改成员变量, 除非成员变量声明为`mutable`
- 可以使用`const`版本成员函数实现 `non-const`版本成员函数, 先转成const型调用,再去除const属性. 反向不可.

初始化: 
- 手工初始化内置型对象, c++不保证初始化他们
- 使用初始化列表, 而不是赋值的方式
- 初始化次序: base class 先于 derived class, class成员变量以声明方式次序初始化, 而不是初始化列表中的次序
- `static` 对象: 寿命从构造直到程序结束
    - `local static`: 函数体内的`static`对象
    - `non-local static`: global对象, 定义于namespace作用域内的对象, 在class内/file作用域内声明为`static`的对象 
- 使用`local static`替代`non-local static`来解决跨编译单元之初始化次序问题

## Chapter 2 构造/析构/赋值
编译器默认为class创建: default构造函数, copy构造函数, copy assignment操作符, 析构函数
- 一旦声明一个构造函数, 则不再创建default构造函数
- 这些函数被需要时, 才会被创建出来
- c++不允许reference改指向不同对象

阻止拷贝和赋值拷贝:
- 将成员函数声明为`private`, 并且不实现他们
- 继承`noncopyable`父类
- c++11: 使用`=delete`

析构:
- 带多态性质的的base class应该声明一个`virtual`析构函数
- 如果class带有`virtual`函数, 那它应该有`virtual`析构函数
- 析构方式: 最深层派生类的析构函数最先调用, 然后是每一个基类的析构函数. (构造过程相反)

析构函数不要抛出异常, 如果客户需要对某个函数运行期间抛出的异常做出反应, 那么应该提供一个普通函数执行操作, 在析构函数可以检查该操作是否成功.

在构造和析构期不要调用`virtual`函数, 因为这类调用不下降至derived class

赋值预算符`=`:
- 返回`reference to *this`
- 处理自我赋值的情况, 注意异常安全
- 解决方法: `copy and swap` 先拷贝(创建栈上对象)再交换(交换资源, 栈上对象析构, 释放旧资源)

拷贝构造函数和拷贝赋值函数:
- 子类的拷贝构造函数和拷贝赋值函数需要显式调用基类的拷贝构造函数和拷贝赋值函数, 来确保所有成员都被复制
- 拷贝构造函数和拷贝赋值函数不相互调用

## Chapter 3 资源管理
使用对象管理资源RAII(资源在构造时获得, 在析构时释放)

小心资源管理类的copying行为:
- 禁止复制
- 对底层资源使用引用计数

APIs往往需要访问原始资源, 所以资源管理类要提供接口获得原始资源

用独立语句将`new`出的对象放入智能指针中, 否则容易产生难以察觉的资源泄露

## Chapter 4 设计与声明
尽量以`pass-by-reference-to-const`代替`pass-by-value`, 但是此规则不适用内置类型/STL的迭代器/函数对象

必须返回对象时, 别想返回引用
- 不要返回pointer或reference指向local stack对象
- 不要返回reference指向heap-allocated对象
- 不要返回pointer或reference指向local static对象

将成员变量声明为`private`: 一致性, 封装

## Chapter 5 实现
尽量延后变量定义式的出现

异常安全:
- 函数如果成功, 则完全成功; 如果失败, 则回复到调用前的状态

## Chapter 6 继承与面向对象设计
`public inheritance` 意味着`is-a`的关系

`virtual`
- `pure virtual` -> 继承接口
- `impure virtual` -> 继承接口和缺省实现
- `non-virtual` -> 继承接口及一份强制性实现

`composition`复合:
- 应用领域: `has-a`关系
- 实现领域: `is-implemented-in-terms-of`(根据某物实现)

`private inheritance` 意味着 `is-implemented-in-terms-of`
- 当`derived class`需要访问`protected base class`的成员, 或需要重新定义继承而来的`virtual`函数时, 这样设计是合理的

c++裁定凡是独立对象都必须有非零大小, 通常插入一个`char`到空对象, 同时有可能有对齐需求

## Chapter 7 模板与泛型编程

## Chapter 8 定制new和delete

