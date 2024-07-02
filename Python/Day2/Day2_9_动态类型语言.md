# 动态类型语言

在我们了解动态类型语言之前，我们应该先了解什么是类型检查。类型检查是编程语言中的一个术语。
Before we understand a dynamically typed language, we should learn about what typing is. Typing refers to type-checking in programming languages.

在强类型语言中，例如 Python，表达式 "1" + 2 会导致类型错误，因为这些语言不允许“类型强制”（数据类型的隐式转换）。
In a strongly-typed language, such as Python, "1" + 2 will result in a type error since these languages don't allow for "type coercion" (implicit conversion of data types).

另一方面，在弱类型语言中，例如 Javascript，上述表达式会简单地输出结果 "12"。
On the other hand, a weakly-typed language, such as Javascript, will simply output "12" as a result.

类型检查可以在两个阶段进行：
Type-checking can be done at two stages:

静态 - 在执行前检查数据类型。
Static - Data types are checked before execution.

动态 - 在执行期间检查数据类型。
Dynamic - Data types are checked during execution.

Python 是一种解释型语言，逐行执行代码，因此类型检查是在执行过程中动态进行的。因此，Python 是一种动态类型语言。
Python is an interpreted language, executes each statement line by line, and thus type-checking is done on the fly, during execution. Hence, Python is a Dynamically Typed Language.

### Comparison Table

Here's a comparison in a markdown table format to clarify further:

```markdown
| Feature | Static Typing | Dynamic Typing |
|---------|---------------|----------------|
| **Type Checking Time** | Before execution | During execution |
| **Examples** | C++, Java | Python, JavaScript |
| **Flexibility** | Less flexible, types must be specified | More flexible, types determined at runtime |
| **Error Detection** | Early, at compile time | Late, at runtime |
```

解释语言在执行每条语句时进行类型检查，从而在执行过程中动态地进行类型检查。因此，Python 是一种动态类型语言。
