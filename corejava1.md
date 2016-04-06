## Content
- basics
- OO

---
### Basics
- 字符串不可以改变内容, 可以使得字符串共享
- 字符串常量是共享的
- 对经常编辑的字符串, 使用`StringBuilder`
- 输入: `Scanner in = new Scanner(System.in);`
- java不能在嵌套的两个块中声明相同的变量
- `switch`的类型可以为`char, byte, short, int`, 枚举常量, 字符创字面量(since SE 7)
- 大数值: `BigInteger`, `BigDecimal`
- java中`[]`运算符被预定义为检查数组边界
- 命令行参数, 与c++不同, java不包含程序名称

## OO
- 域初始化:
    - java中可以在类定义中, 直接将一个值赋给任何域.
    - c++中不能直接初始化类的实例域, 需要使用初始化列表
    
```
// java
class haha {
    private String name = "haha";
    // ...   
}
// c++
class haha {
 public:
    haha(): name("haha") {}
private:
    std::string name;
}
```
      
- java可以在一个构造器的第一句调用其他构造器, c++不可以
- java初始化数据的方法
    - 在构造器中设置值
    - 在声明中赋值
    - 初始化块: 使用`{}`包裹初始化语句块
- java不支持析构器, 可以为类添加`finalize`方法
- 静态导入: `import static java.lang.System.out`
- java中都是公有继承, 不支持多继承
- 如果子类的构造器没有显式调用超类的构造器, 则将自动地调用超类默认的构造器
- 函数调用过程:
    - 查看对象的声明类型和方法名
    - 查看调用方法时提供的参数类型
    - 如果是`private, static, final`则执行静态绑定
    - 动态绑定     
- 检测对象类型: `if (staff[1] instanceof Manager) ...`, 转换失败则抛出异常
- `abstract`: 抽象类可以包含具体数据和具体方法, 即使不含抽象方法也可以声明为抽象类, 不可以实例化抽象类, 可以定义指向具体对象的抽象类引用变量
- java中`protected`对本包和所有子类可见, 比c++的保护机制安全性差
- Object: 所有类的超类, 具有方法`equals(), hashCode(), toString()`
- 反射:
    - Class类:
        - `obj.getClass()`: 获取当前对象的类型实例, 即Class对象
        - `getName()`: 获取类的名字
        - `forName(String)`: 由名字获取类型对象, 若类名不存在则抛出异常
        - `newInstance()`: 创建类的实例
    - Field, Method, Constructor类: 域, 方法, 构造器
        - Method类中有`invoke`方法实现方法的调用
    - Modifier类: 修饰符  
- 接口没有实例域和实现方法, 所有的方法自动地是`public`              