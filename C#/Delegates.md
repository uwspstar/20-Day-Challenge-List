### **What is the Need for Delegates?**  
### **为什么需要委托？**

Delegates are a core concept in C# used to pass methods as arguments to other methods. They allow flexibility in program design by enabling a function to be treated as an object, thus promoting code reuse and event-driven programming.

委托是C#中的核心概念，用于将方法作为参数传递给其他方法。它们通过允许将函数作为对象来处理，从而增强了程序设计的灵活性，促进了代码复用和事件驱动编程。

#### **1. Flexibility in Method Invocation**  
#### **方法调用的灵活性**

- **Need**: Delegates enable passing methods as parameters to other methods, allowing dynamic method invocation at runtime.
  
  **需求**：委托允许将方法作为参数传递给其他方法，从而实现运行时的动态方法调用。

- **Example**: If you need to apply different methods to a dataset, you can pass the specific method as a delegate without hardcoding which method to use.

  **示例**：如果你需要对数据集应用不同的方法，你可以将特定方法作为委托传递，而无需硬编码要使用的方法。

#### **2. Event Handling**  
#### **事件处理**

- **Need**: Delegates are crucial for event handling in C#. They allow you to define methods that respond to specific events (e.g., button clicks, data changes). Delegates help create event-driven applications.
  
  **需求**：委托在C#中的事件处理至关重要。它们允许定义响应特定事件的方法（如按钮点击、数据变化）。委托有助于创建事件驱动的应用程序。

- **Example**: You can use a delegate to specify which method should be called when a button is clicked.
  
  **示例**：你可以使用委托来指定当按钮被点击时应该调用哪个方法。

#### **3. Code Reusability**  
#### **代码复用性**

- **Need**: Delegates allow you to reuse code by passing different methods to the same delegate. This makes the code more modular and reduces duplication.
  
  **需求**：委托允许通过将不同方法传递给相同的委托来复用代码。这使代码更加模块化并减少重复。

- **Example**: A sorting algorithm could accept a delegate to define the sorting criteria, allowing different sorting methods to be applied to the same dataset.
  
  **示例**：排序算法可以接受一个委托来定义排序标准，从而对相同的数据集应用不同的排序方法。

#### **4. Callbacks**  
#### **回调**

- **Need**: Delegates allow you to implement callback methods, where a method is called after an asynchronous operation completes. This is essential for non-blocking operations like file I/O, network requests, etc.
  
  **需求**：委托允许实现回调方法，即在异步操作完成后调用某个方法。这对于非阻塞操作（如文件I/O、网络请求等）至关重要。

- **Example**: After downloading a file, you might use a delegate to specify a method that processes the downloaded data.
  
  **示例**：在下载文件后，你可以使用委托来指定处理下载数据的方法。

#### **5. Multicast Delegates**  
#### **多播委托**

- **Need**: Delegates in C# can point to multiple methods at once, enabling multicast functionality where multiple methods are invoked in sequence. This is useful in event-driven programming where multiple handlers may respond to a single event.
  
  **需求**：C#中的委托可以一次指向多个方法，从而实现多播功能，即多个方法按顺序调用。这在事件驱动编程中很有用，多个处理程序可以响应一个事件。

- **Example**: You can attach multiple event handlers to a button click, and all of them will be invoked when the event occurs.
  
  **示例**：你可以将多个事件处理程序附加到一个按钮点击事件，当事件发生时，所有处理程序都会被调用。

---
### **1. Flexibility in Method Invocation**  
### **方法调用的灵活性**

- **Need**: Delegates enable passing methods as parameters to other methods, allowing dynamic method invocation at runtime.
  
  **需求**：委托允许将方法作为参数传递给其他方法，从而实现运行时的动态方法调用。

- **Example**: If you need to apply different methods to a dataset, you can pass the specific method as a delegate without hardcoding which method to use.

  **示例**：如果你需要对数据集应用不同的方法，你可以将特定方法作为委托传递，而无需硬编码要使用的方法。

#### **Code Example (Chinese only)**:
```csharp
// 定义一个委托
public delegate int Operation(int x, int y);

// 定义两个不同的方法
public static int Add(int a, int b) => a + b;
public static int Subtract(int a, int b) => a - b;

// 使用委托传递不同的方法
public static void PerformOperation(int a, int b, Operation operation)
{
    Console.WriteLine($"Result: {operation(a, b)}");
}

public static void Main()
{
    // 动态调用不同的方法
    PerformOperation(10, 5, Add);        // 输出: Result: 15
    PerformOperation(10, 5, Subtract);   // 输出: Result: 5
}
```

---

### **2. Event Handling**  
### **事件处理**

- **Need**: Delegates are crucial for event handling in C#. They allow you to define methods that respond to specific events (e.g., button clicks, data changes). Delegates help create event-driven applications.
  
  **需求**：委托在C#中的事件处理至关重要。它们允许定义响应特定事件的方法（如按钮点击、数据变化）。委托有助于创建事件驱动的应用程序。

- **Example**: You can use a delegate to specify which method should be called when a button is clicked.

  **示例**：你可以使用委托来指定当按钮被点击时应该调用哪个方法。

#### **Code Example (Chinese only)**:
```csharp
// 定义一个委托，用于按钮点击事件
public delegate void ButtonClickHandler();

// 定义响应事件的方法
public static void OnButtonClicked()
{
    Console.WriteLine("按钮被点击！");
}

public static void Main()
{
    // 创建按钮点击事件处理程序
    ButtonClickHandler clickHandler = OnButtonClicked;

    // 模拟按钮点击事件
    Console.WriteLine("模拟按钮点击...");
    clickHandler();  // 输出: 按钮被点击！
}
```

---

### **3. Code Reusability**  
### **代码复用性**

- **Need**: Delegates allow you to reuse code by passing different methods to the same delegate. This makes the code more modular and reduces duplication.
  
  **需求**：委托允许通过将不同方法传递给相同的委托来复用代码。这使代码更加模块化并减少重复。

- **Example**: A sorting algorithm could accept a delegate to define the sorting criteria, allowing different sorting methods to be applied to the same dataset.

  **示例**：排序算法可以接受一个委托来定义排序标准，从而对相同的数据集应用不同的排序方法。

#### **Code Example (Chinese only)**:
```csharp
// 定义一个委托用于排序比较
public delegate int ComparisonDelegate(int a, int b);

// 升序排序方法
public static int AscendingOrder(int a, int b) => a.CompareTo(b);

// 降序排序方法
public static int DescendingOrder(int a, int b) => b.CompareTo(a);

// 使用委托执行排序
public static void Sort(int[] array, ComparisonDelegate comparison)
{
    Array.Sort(array, new Comparison<int>(comparison));
}

public static void Main()
{
    int[] numbers = { 5, 2, 8, 3, 1 };

    // 使用升序排序
    Sort(numbers, AscendingOrder);
    Console.WriteLine("升序排序: " + string.Join(", ", numbers));  // 输出: 1, 2, 3, 5, 8

    // 使用降序排序
    Sort(numbers, DescendingOrder);
    Console.WriteLine("降序排序: " + string.Join(", ", numbers));  // 输出: 8, 5, 3, 2, 1
}
```

---

### **4. Callbacks**  
### **回调**

- **Need**: Delegates allow you to implement callback methods, where a method is called after an asynchronous operation completes. This is essential for non-blocking operations like file I/O, network requests, etc.
  
  **需求**：委托允许实现回调方法，即在异步操作完成后调用某个方法。这对于非阻塞操作（如文件I/O、网络请求等）至关重要。

- **Example**: After downloading a file, you might use a delegate to specify a method that processes the downloaded data.

  **示例**：在下载文件后，你可以使用委托来指定处理下载数据的方法。

#### **Code Example (Chinese only)**:
```csharp
// 定义委托用于回调
public delegate void FileDownloadCallback(string filePath);

// 模拟文件下载并执行回调
public static void DownloadFile(FileDownloadCallback callback)
{
    // 模拟文件下载
    Console.WriteLine("正在下载文件...");
    System.Threading.Thread.Sleep(2000);  // 模拟延迟
    string downloadedFile = "/path/to/file.txt";

    // 文件下载完成，执行回调
    callback(downloadedFile);
}

// 文件处理方法
public static void ProcessDownloadedFile(string filePath)
{
    Console.WriteLine($"文件下载完成，处理文件：{filePath}");
}

public static void Main()
{
    // 执行文件下载并在完成后处理文件
    DownloadFile(ProcessDownloadedFile);
}
```

---

### **5. Multicast Delegates**  
### **多播委托**

- **Need**: Delegates in C# can point to multiple methods at once, enabling multicast functionality where multiple methods are invoked in sequence. This is useful in event-driven programming where multiple handlers may respond to a single event.
  
  **需求**：C#中的委托可以一次指向多个方法，从而实现多播功能，即多个方法按顺序调用。这在事件驱动编程中很有用，多个处理程序可以响应一个事件。

- **Example**: You can attach multiple event handlers to a button click, and all of them will be invoked when the event occurs.

  **示例**：你可以将多个事件处理程序附加到一个按钮点击事件，当事件发生时，所有处理程序都会被调用。

#### **Code Example (Chinese only)**:
```csharp
// 定义委托用于多播
public delegate void MulticastDelegate();

// 方法1
public static void Handler1()
{
    Console.WriteLine("处理程序1执行");
}

// 方法2
public static void Handler2()
{
    Console.WriteLine("处理程序2执行");
}

public static void Main()
{
    // 创建多播委托
    MulticastDelegate multicast = Handler1;
    multicast += Handler2;

    // 执行多播委托，两个处理程序都会被调用
    multicast();  // 输出: 处理程序1执行，处理程序2执行
}
```

In this code, the `MulticastDelegate` is assigned to both `Handler1` and `Handler2`. When invoked, both methods are executed in sequence.

在此代码中，`MulticastDelegate`同时指向`Handler1`和`Handler2`。当调用时，两个方法按顺序执行。

---

### **Comparison with Other Techniques**  
### **与其他技术的比较**

| **Aspect**                    | **Delegates (委托)**                                    | **Direct Method Calls (直接方法调用)**            |
|-------------------------------|--------------------------------------------------------|-------------------------------------------------|
| **Flexibility**                | High, can change methods dynamically (灵活性高，可动态更改方法) | Low, method is hardcoded (灵活性低，方法是硬编码的) |
| **Event Handling**             | Essential for event-driven programming (事件驱动编程必需) | Cannot directly handle events (无法直接处理事件)    |
| **Reusability**                | High, promotes modular code (高，促进模块化代码)         | Less reusable (较少复用性)                       |
| **Asynchronous Callbacks**     | Supported with ease (支持异步回调)                      | Not supported without additional techniques (需要其他技术支持) |
| **Multicast Capability**       | Supports multiple method calls (支持多次方法调用)         | Single method call (单次方法调用)                 |

### **Code Example (Chinese only)**:
```csharp
// 定义一个委托
public delegate void PrintDelegate(string message);

// 方法1
public static void PrintToConsole(string message)
{
    Console.WriteLine("Console: " + message);
}

// 方法2
public static void PrintToFile(string message)
{
    System.IO.File.WriteAllText("output.txt", message);
}

// 使用委托
public static void Main()
{
    // 将PrintToConsole方法作为委托
    PrintDelegate print = PrintToConsole;
    print("Hello, World!");  // 输出到控制台
    
    // 将PrintToFile方法作为委托
    print = PrintToFile;
    print("Hello, File!");  // 输出到文件
}
```

In this example, the delegate `PrintDelegate` can point to different methods (`PrintToConsole` or `PrintToFile`), allowing dynamic behavior.

在这个示例中，委托`PrintDelegate`可以指向不同的方法（`PrintToConsole`或`PrintToFile`），从而实现动态行为。

---

### **Explanation of:**
```csharp
public delegate void Notify();  // 委托
public event Notify OnNotify;   // 事件
```

### **1. Delegate Definition (`public delegate void Notify();`)**  
### **委托定义 (`public delegate void Notify();`)**

A **delegate** is a type that defines the signature of methods that can be assigned to it. The delegate `Notify` here is defined as a method that takes no parameters and returns `void`.

**委托**是一种定义可以分配给它的方法签名的类型。这里的委托`Notify`定义为一个不带参数且返回`void`的方法。

#### **Explanation:**
- **Delegate Name**: `Notify`  
  **委托名称**：`Notify`
  
- **Signature**: It can point to any method that takes no arguments and returns `void`.  
  **签名**：它可以指向任何不带参数且返回`void`的方法。

#### **Example (Chinese only)**:
```csharp
// 定义符合委托签名的方法
public static void ShowMessage()
{
    Console.WriteLine("通知已触发！");
}

public static void Main()
{
    // 创建委托实例并指向方法
    Notify notifyDelegate = ShowMessage;
    notifyDelegate();  // 输出: 通知已触发！
}
```

In this example, the `Notify` delegate is pointing to the `ShowMessage` method, which matches the delegate’s signature (no parameters, returns `void`). When the delegate is invoked, it calls `ShowMessage`.

在这个示例中，`Notify`委托指向与委托签名相匹配的`ShowMessage`方法（无参数，返回`void`）。当调用委托时，它会执行`ShowMessage`。

---

### **2. Event Definition (`public event Notify OnNotify;`)**  
### **事件定义 (`public event Notify OnNotify;`)**

An **event** is a specialized delegate that is used to handle notifications or signals, typically in event-driven programming. The `OnNotify` event is defined using the `Notify` delegate, meaning it can store methods that match the `Notify` delegate’s signature.

**事件**是一种专用的委托，通常用于事件驱动编程中的通知或信号处理。`OnNotify`事件使用`Notify`委托定义，这意味着它可以存储与`Notify`委托签名匹配的方法。

#### **Explanation:**
- **Event Name**: `OnNotify`  
  **事件名称**：`OnNotify`
  
- **Delegate Association**: The event is associated with the `Notify` delegate, so it can store and invoke any method that matches the `Notify` signature.  
  **委托关联**：该事件与`Notify`委托相关联，因此它可以存储并调用任何与`Notify`签名匹配的方法。

- **Multicast Behavior**: Events are multicast delegates, meaning multiple methods can subscribe to the event, and all methods will be invoked when the event is raised.  
  **多播行为**：事件是多播委托，意味着多个方法可以订阅该事件，当事件被触发时，所有订阅的方法都会被调用。

#### **Example (Chinese only)**:
```csharp
// 定义委托和事件
public delegate void Notify();  
public event Notify OnNotify;  

// 定义两个方法，用于处理事件
public static void NotifyHandler1()
{
    Console.WriteLine("处理程序1已收到通知。");
}

public static void NotifyHandler2()
{
    Console.WriteLine("处理程序2已收到通知。");
}

public static void Main()
{
    // 创建事件实例并订阅处理程序
    Program program = new Program();
    program.OnNotify += NotifyHandler1;
    program.OnNotify += NotifyHandler2;

    // 触发事件
    if (program.OnNotify != null)
        program.OnNotify();  // 输出: 处理程序1已收到通知。
                             //      处理程序2已收到通知。
}
```

In this example:
1. The `OnNotify` event is defined using the `Notify` delegate.
2. Two methods (`NotifyHandler1` and `NotifyHandler2`) are subscribed to the event using `+=`.
3. When the event is triggered (i.e., `program.OnNotify()`), both methods are invoked in sequence.

在此示例中：
1. `OnNotify`事件使用`Notify`委托定义。
2. 两个方法（`NotifyHandler1`和`NotifyHandler2`）通过`+=`订阅事件。
3. 当事件触发时（即调用`program.OnNotify()`），两个方法将按顺序执行。

---

### **Summary**
1. **Delegate (`Notify`)**: A type-safe pointer to a method that matches the specified signature (in this case, no parameters and returns `void`).  
   **委托 (`Notify`)**：一种类型安全的指向与指定签名匹配的方法的指针（本例中无参数且返回`void`）。
   
2. **Event (`OnNotify`)**: An event based on the `Notify` delegate, allowing multiple methods to subscribe and be executed when the event is triggered.  
   **事件 (`OnNotify`)**：基于`Notify`委托的事件，允许多个方法订阅并在事件触发时执行。

Events are typically used in event-driven programming to notify observers about changes or actions, while delegates serve as the mechanism to dynamically invoke methods.

事件通常用于事件驱动编程，以通知观察者关于变化或操作，而委托则作为动态调用方法的机制。

---
### Understanding the `+=` Operator in Events

In the code:
```csharp
Program program = new Program();
program.OnNotify += NotifyHandler1;
program.OnNotify += NotifyHandler2;
```

The `+=` operator is used to **subscribe methods** to an event. When you use `+=` with an event, you're adding methods (event handlers) that should be executed when the event is triggered. Multiple methods can be attached to the same event, and they will all be invoked when the event is raised.

在代码中：
```csharp
Program program = new Program();
program.OnNotify += NotifyHandler1;
program.OnNotify += NotifyHandler2;
```
`+=`操作符用于**订阅方法**到一个事件。当你使用`+=`与事件结合时，你是在向事件添加方法（事件处理程序），这些方法会在事件触发时被执行。多个方法可以附加到同一个事件，并且当事件触发时，它们都会被调用。

### Detailed Explanation:

1. **`+=` Operator for Event Subscription**  
   The `+=` operator adds a method to the **invocation list** of the event. An event maintains a list of methods (also called event handlers) that need to be executed when the event is raised. When you use `+=`, you're adding a method to this list.

   **`+=`操作符用于事件订阅**  
   `+=`操作符将一个方法添加到事件的**调用列表**中。事件维护一个方法列表（也称为事件处理程序），当事件触发时需要执行这些方法。使用`+=`时，你是在向这个列表中添加一个方法。

2. **Multicast Delegates**  
   An event in C# is based on a **multicast delegate**, meaning it can point to more than one method. The `+=` operator allows multiple methods to be attached to the same event, and all methods will be executed in the order they were added when the event is raised.

   **多播委托**  
   C#中的事件基于**多播委托**，这意味着它可以指向多个方法。`+=`操作符允许多个方法附加到同一个事件，当事件触发时，这些方法将按照它们被添加的顺序依次执行。

3. **Order of Execution**  
   The methods are executed in the order they were added. In your case, `NotifyHandler1` is added first, followed by `NotifyHandler2`. When `OnNotify` is triggered, both methods will be called in sequence:
   - `NotifyHandler1` will be called first.
   - `NotifyHandler2` will be called next.

   **执行顺序**  
   方法按照它们被添加的顺序执行。在你的代码中，首先添加的是`NotifyHandler1`，接着是`NotifyHandler2`。当`OnNotify`事件触发时，这两个方法将按顺序调用：
   - 首先调用`NotifyHandler1`。
   - 接着调用`NotifyHandler2`。

4. **Triggering the Event**  
   When the event `OnNotify` is raised (e.g., `program.OnNotify();`), both `NotifyHandler1` and `NotifyHandler2` will be executed.

   **触发事件**  
   当`OnNotify`事件被触发时（例如，`program.OnNotify();`），`NotifyHandler1`和`NotifyHandler2`都会被执行。

### Code Walkthrough:
```csharp
public delegate void Notify();  // 定义委托
public event Notify OnNotify;   // 定义事件

// 事件处理程序1
public static void NotifyHandler1()
{
    Console.WriteLine("处理程序1已收到通知。");
}

// 事件处理程序2
public static void NotifyHandler2()
{
    Console.WriteLine("处理程序2已收到通知。");
}

public static void Main()
{
    Program program = new Program();
    
    // 使用 += 订阅两个方法到事件中
    program.OnNotify += NotifyHandler1;
    program.OnNotify += NotifyHandler2;

    // 触发事件，两个处理程序都会执行
    if (program.OnNotify != null)
        program.OnNotify();
}
```

### Breakdown:
- `program.OnNotify += NotifyHandler1;`: This adds `NotifyHandler1` to the event, meaning this method will be executed when the event is triggered.
  
  **`program.OnNotify += NotifyHandler1;`**：这将`NotifyHandler1`方法添加到事件中，意味着当事件触发时该方法将被执行。

- `program.OnNotify += NotifyHandler2;`: This adds `NotifyHandler2` to the event. Now, both `NotifyHandler1` and `NotifyHandler2` will be executed when the event is triggered.
  
  **`program.OnNotify += NotifyHandler2;`**：这将`NotifyHandler2`方法添加到事件中。现在，当事件触发时，`NotifyHandler1`和`NotifyHandler2`都会执行。

### Order of Execution (Chinese only):
1. `NotifyHandler1` will output: `处理程序1已收到通知。`
2. `NotifyHandler2` will output: `处理程序2已收到通知。`

When the event `OnNotify` is triggered, both handlers will be invoked in the order they were added. The output will be:
```
处理程序1已收到通知。
处理程序2已收到通知。
```

当`OnNotify`事件触发时，两个处理程序将按照它们被添加的顺序调用。输出结果为：
```
处理程序1已收到通知。
处理程序2已收到通知。
```

---

### Summary
1. The `+=` operator is used to **subscribe** methods to an event.
2. Multiple methods can be added to the same event, making it a **multicast** delegate.
3. When the event is triggered, all subscribed methods are called in the order they were added.

### 总结
1. `+=`操作符用于**订阅**方法到事件。
2. 可以将多个方法添加到同一个事件中，使其成为**多播**委托。
3. 当事件被触发时，所有订阅的方法将按添加顺序依次执行。

---

### 解释 "事件的调用列表"  
### **"+=操作符将一个方法添加到事件的调用列表中"**

在C#中，**事件的调用列表**（**Invocation List**）是一个包含所有已订阅事件处理程序的方法列表。当事件被触发时，调用列表中的所有方法都会按照它们被添加的顺序依次执行。

### **1. 什么是调用列表？**

调用列表是事件存储其订阅的所有方法的内部机制。每次使用`+=`操作符将一个方法附加到事件时，该方法会被添加到事件的调用列表中。当事件触发时，调用列表中的所有方法都会依次被调用。

- **调用列表**：是一个存储所有已订阅方法的列表。
  
  **Invocation List**: A list that stores all the methods subscribed to the event.

- **方法的顺序**：方法按照它们被添加的顺序存储在调用列表中。触发事件时，这些方法会按照添加的顺序依次执行。

  **Method Order**: Methods are stored in the order they are added to the list. When the event is triggered, they are executed in sequence.

---

### **2. += 操作符如何影响调用列表？**

每当你使用`+=`操作符将方法添加到事件时，实际上你是在将这个方法加入到事件的调用列表中。这个操作并不会替换已有的方法，而是将新方法追加到列表末尾。调用列表可以包含多个方法，当事件触发时，列表中的所有方法都会按顺序被调用。

#### **+= 操作步骤**:
1. **首次使用`+=`**：当你第一次使用`+=`操作符将方法添加到事件时，调用列表会创建并包含该方法。
2. **再次使用`+=`**：如果你使用`+=`操作符再次添加其他方法，新的方法会被追加到调用列表的末尾，而不会覆盖前面的方法。

#### **示例**:
```csharp
public delegate void Notify();  // 定义委托
public event Notify OnNotify;   // 定义事件

// 方法1
public static void NotifyHandler1()
{
    Console.WriteLine("处理程序1执行");
}

// 方法2
public static void NotifyHandler2()
{
    Console.WriteLine("处理程序2执行");
}

public static void Main()
{
    Program program = new Program();
    
    // 使用 += 将方法1添加到事件的调用列表中
    program.OnNotify += NotifyHandler1;

    // 使用 += 将方法2添加到事件的调用列表中
    program.OnNotify += NotifyHandler2;

    // 触发事件，调用列表中的所有方法都会被依次调用
    if (program.OnNotify != null)
        program.OnNotify();  // 输出: 处理程序1执行
                             //      处理程序2执行
}
```

### **解释**:
1. **第一次添加**：`program.OnNotify += NotifyHandler1;` 将`NotifyHandler1`方法添加到`OnNotify`事件的调用列表中。
2. **第二次添加**：`program.OnNotify += NotifyHandler2;` 将`NotifyHandler2`方法添加到`OnNotify`事件的调用列表中。
3. **触发事件**：当`program.OnNotify()`事件被触发时，调用列表中的两个方法会按顺序依次被调用，输出结果为：
   ```
   处理程序1执行
   处理程序2执行
   ```

---

### **3. 调用列表的特点**

- **顺序执行**：调用列表中的方法会按照它们被添加的顺序依次执行。例如，如果你先使用`+=`添加了方法A，再使用`+=`添加了方法B，那么当事件触发时，方法A会先执行，方法B会随后执行。

  **Sequential Execution**: The methods in the invocation list are executed in the order they were added. If method A is added first, followed by method B, method A will execute first when the event is triggered.

- **多播委托**：事件的调用列表实际上是基于**多播委托**（multicast delegate）的。在C#中，事件是多播委托的一个应用，允许一个委托指向多个方法。

  **Multicast Delegate**: The invocation list is built on the concept of a multicast delegate. In C#, an event is essentially a multicast delegate, allowing one delegate to point to multiple methods.

- **删除方法**：可以使用`-=`操作符将方法从调用列表中移除。如果在调用列表中有多个相同的方法实例，只有第一个会被移除。

  **Removing Methods**: You can remove a method from the invocation list using the `-=` operator. If the same method is subscribed multiple times, only the first instance will be removed.

#### **移除方法示例**:
```csharp
// 使用 -= 将方法1从事件的调用列表中移除
program.OnNotify -= NotifyHandler1;
```

---

### **总结**
1. **调用列表**是事件存储所有订阅方法的内部机制，当事件被触发时，调用列表中的方法会按顺序被调用。
2. **`+=`操作符**用于将方法添加到调用列表中，而不会替换已存在的方法。可以添加多个方法，并按顺序执行。
3. **`-=`操作符**可以从调用列表中移除方法，事件处理更加灵活。

**Key Points**:
- The **invocation list** is where the event stores all the subscribed methods.
- The `+=` operator adds methods to the invocation list without replacing previous ones.
- The `-=` operator removes methods from the invocation list.
