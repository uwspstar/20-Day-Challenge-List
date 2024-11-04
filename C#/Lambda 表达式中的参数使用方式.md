让我们通过更多的例子来进一步理解 Lambda 表达式中的参数使用方式，以及为什么我们写 `() => PrintMessage("Hello")` 而不是 `("Hello") => PrintMessage("Hello")`。

### 示例 1：没有参数的 Lambda 表达式

假设我们想要一个不需要任何外部参数的 Lambda 表达式，例如打印一个固定的消息：

```csharp
() => Console.WriteLine("Hello, world!")
```

- `()` 表示 Lambda 表达式不接收任何外部参数。
- `Console.WriteLine("Hello, world!")` 是 Lambda 表达式的主体部分，执行打印操作。

**类似于定义一个没有参数的函数：**

```csharp
void PrintHelloWorld()
{
    Console.WriteLine("Hello, world!");
}
```

### 示例 2：有一个外部参数的 Lambda 表达式

现在假设我们想要创建一个 Lambda 表达式，接收一个外部参数，并把它打印出来。这时我们需要在 Lambda 表达式中定义参数名：

```csharp
(message) => Console.WriteLine(message)
```

- `(message)` 表示 Lambda 表达式接收一个参数 `message`。
- `Console.WriteLine(message)` 使用这个参数，将其内容打印出来。

**类似于定义一个带参数的函数：**

```csharp
void PrintMessage(string message)
{
    Console.WriteLine(message);
}
```

当我们调用这个 Lambda 表达式时，可以传入不同的值：

```csharp
var myLambda = (message) => Console.WriteLine(message);
myLambda("Hello, Lambda!"); // 输出：Hello, Lambda!
myLambda("Another message"); // 输出：Another message
```

### 示例 3：Lambda 表达式内直接使用具体值

在 `() => PrintMessage("Hello")` 中，我们不需要 Lambda 表达式接收任何外部参数，因为 `"Hello"` 是一个固定的值，直接在 Lambda 表达式内部传递给 `PrintMessage`。

```csharp
() => PrintMessage("Hello")
```

**这种写法的作用是创建一个不需要参数的 Lambda 表达式**，执行时直接调用 `PrintMessage("Hello")`。

如果写成 `("Hello") => PrintMessage("Hello")` 是不合法的，因为 `"Hello"` 不能作为参数名。

### 示例 4：Lambda 表达式与方法参数的对比

让我们看一个常见的例子，假设我们要创建一个带参数的 Lambda 表达式，并传入参数给 `PrintMessage`：

```csharp
(message) => PrintMessage(message)
```

- `message` 是 Lambda 表达式的参数，它从外部传入。
- 当 Lambda 表达式执行时，它会调用 `PrintMessage(message)`，把 `message` 的值传给 `PrintMessage`。

**调用示例：**

```csharp
var myLambda = (message) => PrintMessage(message);
myLambda("Hello from Lambda"); // PrintMessage 收到 "Hello from Lambda"
```

### 小结

- `() => PrintMessage("Hello")`：没有外部参数，直接调用 `PrintMessage`，传入固定值 `"Hello"`。
- `(message) => PrintMessage(message)`：接收一个外部参数 `message`，再把 `message` 的值传递给 `PrintMessage`。

用 Lambda 表达式写法时，参数要根据需要来设置：
- 如果需要从外部接收参数，用 `(parameter)`。
- 如果不需要外部参数，用 `()` 表示不接收参数。
