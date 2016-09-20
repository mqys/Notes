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
