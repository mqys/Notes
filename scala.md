# Content
- [Functional Programming Principles in Scala](# Functional Programming Principles in Scala)

## Functional Programming Principles in Scala
### Week 1: Functions and Evaluation
- Elements of Programming:
  - substitusion model: reduce an expression to a value
  - call-by-value VS call-by-name
- if CBV terminates, CBN terminates too. opposite direction wrong!
- In Scala:  default: CBV, use `=>` to CBN. `def constOne(x: Int, y: => Int) = 1`
- `def` -> CBN, `val` -> CBV
- recursive function requires explicit return type
- CBN ==>> syntactic suger
```
def foo(bar: => Int): Int = bar + bar
foo(1 + 1)
// call-by-name
def foo(bar: => Int): Int = (1 + 1) + (1 + 1)
// implementation: use function to implement call-by-name
def foo(bar: () => Int): Int = bar() + bar()
```

### Week 2: High Order Functions
- currying: 多个参数, 函数和一个参数结合后产生新的函数, 将新的函数应用于后面的参数
```
def two(f: Int => Int)(x: Int, y: Int) = f(x + y)
// (Int => Int) => ((Int, Int) => Int)

class Rational(x: Int, y: Int) {
    require(y != 0, "y can not be zero")
    
    override def toString = { "haha"}
}

assert(x > 0)
```

- operator
```
r.add(b)  ==>>  r add b
// 二元
def < (that: Type) = { ... }
r.<(that) ==>> r < b
// 一元, 冒号前必须用空格
def unary_- : Rational = new Rational(-numer, denom)
r < -b
```

- homework: func set
  - 没有数据实体的抽象数据结构
  - 用规则的组合来实现
  - `type Set = Int => Boolean`

### Week 3: Data and Abstraction
- 强制使用`override`标记
