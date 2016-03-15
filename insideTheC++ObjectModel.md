## 本书主要内容:
- C++的内存模型
- 编译器对语句的转换

## Chapter 1 对象
class:
- data member: static / nonstatic
- member function: static / nonstatic / virtual

虚继承:
- base class 在子类对象中永远只会存在一个实例
- `base class table`

class object size:
- nonstatic member data
- alignment padding (边界对齐, 32位机常为4字节/32位)
- `virtual`代价

切割(slicing)与多态:
```
    // slice
    vicc cc;
    vi v = cc; // default copy constructor, two objects
    v.fly();
    
    //virtual
    vicc ccc;
    vi *vv = &ccc;
    vv->fly();
```

ADT风格 ==>> object-based(OB) 

## Chapter 2 构造函数
Default Constructor:
- 带有对象成员: 编译器插入代码, 调用各个对象成员的constructors
- 带有`Base class`: 调用base 的 constructor
- 带有`virtual function`: 插入代码, 初始化vptr
- 带有`virtual base class`: 插入代码, 初始化虚基类指针
- 注: 
    - 被合成出来的constructor只能满足编译器的需要
    - 只用`base class subobject`和`member class objects`会被初始化, 所以其他`nonstatic data member`(整数, 整数数组, 整数指针等)都不会被初始化
    
Copy Constructor:
- `Default Memberwise Initialization`: 将每个内建的或派生的data member依次拷贝, 对于其中的类对象, 以递归的方式施行`memberwise initialization`
- `Bitwise Copy`: 位逐次拷贝. 在以下4中情形, 不会`bitwise copy`:
    - class 内有 member object 而后者声明有copy constructor
    - class 继承 base class 而后者存在copy constructor
    - class 声明了 virtual functions
    - class 派生自继承串链, 其中有一个或多个 virtual base classes    

程序转化:
- 函数返回局部对象: 改成传入额外参数, 构造该参数
- NRV(named return value)优化:
    - 未优化情况下调用返回对象函数: 创建对象, 传入引用到函数, 修改该对象, 返回, 调用拷贝构造函数使用修改好的对象来构造命名的接受返回值的对象
    - NRV优化: 创建接受的对象, 传入引用到函数, 修改对象, 返回 (少一步拷贝构造的过程)

成员初始化列表:
- 必须使用的情形:
    - 初始化 reference member
    - 初始化 const member
    - 调用 base class 的 constructor, 而它拥有一组参数的时候
    - 调用 member class 的 constructor, 而它拥有一组参数的时候
- list 中的顺序是由 class 中的声明顺序决定的, 不是在 list 中的排列顺序     

## Chapter 3 Data
在C++继承模型中, 一个 derived class object 所表现出来的东西, 是其自己的member加上其 base class member的总和.

对成员取址, 传回的值总是多1, 并不是实际内存的地址, 用于区分没有任何指向的data member指针和一个指向第一个data member的指针.

虚继承在子类中至少会占用一个word(指针大小)的长度(在虚表中存放virtual base class的offset), 而普通继承则没有此限制

## Chapter 4 Function
member function:
- static: 特性 -->> 没有this指针 
    - 不能直接存取clas中的nonstatic members
    - 不能被声明为 const / volatile / virutal
    - 不需要经由 class object才能被调用
- nonstatic:
    - 被内化为nonmember形式
        - 1. 改写signature, 额外参数this指针
        - 2. 对成员的存取, 改为由this指针的存取
        - 3. 将member function重新改写成一个外部函数, mangling, member被加上class名
- virtual: 执行期类型推断法
    - 多态: 以一个public base class的指针, 寻址出一个derived class object
    - pure_virtual_called(): 纯虚函数在虚表中被该函数的地址替代
    - 多种继承: 对第二个base class及之后base class需要在执行期间调整this指针
    
inline:
- 分析函数定义, 判断是否可变为inline
- 扩展函数, 参数求值 / 临时对象管理

## Chapter 5 构造 / 析构 / 拷贝
C与C++的一个差异: BSS data segment在C++中相对地不那么重要. C++的所有全局对象都以"初始化过的数据"来对待

constructor顺序:
- member initialization list, 声明顺序
- member not in list but have default constructor
- virtual table
- base class constructor
- virtual base class constructor

destructor顺序与constructor相反

## Chapter 6 执行期
local static class object 的 constructor / destructor 保证只施行一次

## Chapter 7 站在对象模型的尖端
- Template
    - 实例化策略:
        - 编译期策略: 程序代码在program text file中备妥可用
        - 连接期策略: meta-compilation工具引导编译器的实例化行为
- Exception
- RTTI(Runtime Type Indentification)
    - 通常是虚表第一个slot, 静态设定     