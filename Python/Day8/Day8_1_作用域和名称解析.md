# 作用域和名称解析
In Python, the concept of scopes and how names are resolved is fundamental to understanding how the language handles variables and function names. Here’s a breakdown of the key points you mentioned, explained for better clarity:

在Python中，理解作用域和名称解析的概念对于了解该语言如何处理变量和函数名称至关重要。以下是您提到的关键点的解释，以便更好地理解：

### Scope Determined by Code Structure

1. **Literal Text Determination**: The scope of variables and functions in Python is determined by where they are defined in the source code, not where they are called. This is known as lexical or static scoping. A function defined in a module has its global scope set to the namespace of that module, which means the function can access all variables that are defined at the module level.

1. **按字面文本确定**：在Python中，变量和函数的作用域是由它们在源代码中的定义位置决定的，而不是它们被调用的位置。这被称为词法或静态作用域。在模块中定义的函数其全局作用域设置为该模块的命名空间，这意味着函数可以访问在模块级别定义的所有变量。

### Dynamic Name Resolution at Runtime

2. **Dynamic Name Resolution**: While the scope is static, the actual name resolution—finding what a name refers to—is done dynamically at runtime. This means Python looks up names when the code is executed, allowing for behaviors like updating global variables or importing modules at runtime which can affect how names are resolved.

2. **运行时动态名称解析**：虽然作用域是静态的，但实际的名称解析——查找名称所指的内容——是在运行时动态完成的。这意味着Python在代码执行时查找名称，允许执行诸如更新全局变量或运行时导入模块等行为，这些可以影响名称的解析方式。

### Trend Towards Static Name Resolution

3. **Static Name Resolution Trend**: Python is moving towards more static name resolution at compile-time, which can make the language more efficient by resolving names when the code is compiled rather than at runtime. This is already true for local variables, whose scope is determined when the function is defined, not when it is called.

3. **静态名称解析趋势**：Python正在向编译时更静态的名称解析方向发展，这可以通过在代码编译时而不是运行时解析名称，使语言更加高效。对于局部变量，其作用域在函数定义时就已确定，而不是在调用时确定，这一点已经成立。

### Implications

4. **Implications of Static Resolution**: The shift towards static resolution means that programmers should be cautious about relying too heavily on dynamic features for name resolution, such as dynamically changing the meaning of global names. Static analysis tools and optimizations can work better with more predictable, static name resolution.

4. **静态解析的含义**：向静态解析的转变意味着程序员应谨慎依赖于动态功能进行名称解析，例如动态改变全局名称的含义。静态分析工具和优化可以更好地与更可预测的静态名称解析一起工作。

Understanding these concepts is essential for writing effective and efficient Python code, as it helps in designing better structures and foreseeing potential issues related to scope and name resolution.

理解这些概念对于编写有效和高效的Python代码至关重要，因为它有助于设计更好的结构并预见与作用域和名称解析相关的潜在问题。
