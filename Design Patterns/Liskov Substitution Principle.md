### What is the Liskov Substitution Principle?  
### 什么是里氏替换原则？

**English**:  
The **Liskov Substitution Principle (LSP)** is one of the five SOLID principles of object-oriented programming introduced by Barbara Liskov in 1987. It states that objects of a superclass should be replaceable with objects of a subclass without altering the correctness of the program. In other words, if a class `S` is a subclass of class `T`, then objects of type `T` should be replaceable by objects of type `S` without affecting the desired behavior of the program.

This principle encourages the design of subclasses that can be used interchangeably with their base classes, promoting better code reusability and extensibility. Violating LSP can lead to unexpected behaviors and fragile code that breaks when subclasses are used in place of base classes.

**Key Points**:  
- Subclasses should **extend** the functionality of the superclass without changing its behavior.
- Subtypes must be **substitutable** for their base types.
- Clients using the base class should not need to know if a derived class is being used instead.

**Example Scenario**:  
If we have a class `Bird` with a method `Fly()`, a subclass `Penguin` should not be created if it overrides the `Fly()` method to throw an exception, as penguins cannot fly. This violates LSP because a `Penguin` object cannot substitute a `Bird` object without altering the behavior of the program.

**中文**:  
**里氏替换原则（LSP）**是 1987 年由 Barbara Liskov 提出的面向对象编程的五个 SOLID 原则之一。该原则指出，超类的对象应该可以被子类的对象替换，而不影响程序的正确性。换句话说，如果类 `S` 是类 `T` 的子类，那么类型 `T` 的对象应该可以被类型 `S` 的对象替换，而不会影响程序的预期行为。

这一原则鼓励设计能够与其基类互换使用的子类，从而促进更好的代码重用性和扩展性。如果违反 LSP 原则，可能会导致意外行为，并导致当使用子类替换基类时程序出现问题。

**关键点**：  
- 子类应**扩展**超类的功能，而不应更改其行为。
- 子类型必须可以被**替换**为其基类型。
- 使用基类的客户端不应关心是否使用了派生类。

**示例场景**：  
如果我们有一个 `Bird` 类，其中包含 `Fly()` 方法，那么不应创建一个子类 `Penguin`，因为企鹅不能飞。如果 `Penguin` 子类覆盖了 `Fly()` 方法，并抛出异常，则违反了 LSP 原则，因为 `Penguin` 对象无法在不更改程序行为的情况下替代 `Bird` 对象。

---

### Practical Example of LSP in C#  
### C# 中的里氏替换原则实际示例

```csharp
// 基类 - 长方形
public class Rectangle
{
    public virtual int Width { get; set; }
    public virtual int Height { get; set; }

    public int GetArea()
    {
        return Width * Height;
    }
}

// 子类 - 正方形
public class Square : Rectangle
{
    // 重写 Width 属性，同时更改 Height 属性，使其保持与 Width 相等
    public override int Width
    {
        get { return base.Width; }
        set
        {
            base.Width = value;
            base.Height = value; // 正方形的高度始终与宽度相等
        }
    }

    // 重写 Height 属性，同时更改 Width 属性，使其保持与 Height 相等
    public override int Height
    {
        get { return base.Height; }
        set
        {
            base.Height = value;
            base.Width = value; // 正方形的宽度始终与高度相等
        }
    }
}

// 测试类
class Program
{
    static void Main(string[] args)
    {
        Rectangle rect = new Rectangle();
        rect.Width = 10;
        rect.Height = 5;
        Console.WriteLine($"Rectangle Area: {rect.GetArea()}"); // 输出：Rectangle Area: 50

        Rectangle square = new Square();
        square.Width = 10; // 设置宽度为10时，高度也会变为10
        square.Height = 5; // 再次设置高度为5时，宽度也会变为5
        Console.WriteLine($"Square Area: {square.GetArea()}"); // 输出：Square Area: 25
    }
}
```

**Explanation**:  
In the above example, `Square` is a subclass of `Rectangle`. However, substituting a `Square` object in place of a `Rectangle` object breaks the expected behavior of the program. When changing the width or height of a `Square`, the other dimension automatically changes to maintain the square shape, which is not true for a regular rectangle. This violates the LSP because the subclass `Square` does not preserve the behavior of its superclass `Rectangle`.

**中文解释**:  
在上面的示例中，`Square` 是 `Rectangle` 的子类。然而，用 `Square` 对象替换 `Rectangle` 对象时，会破坏程序的预期行为。当更改 `Square` 的宽度或高度时，为了保持正方形形状，另一个维度也会自动更改，这与普通矩形的行为不符。这违反了 LSP 原则，因为子类 `Square` 没有保持其超类 `Rectangle` 的行为。

---

### How to Adhere to Liskov Substitution Principle?  
### 如何遵循里氏替换原则？

To adhere to the LSP, subclasses should:
1. Not override methods in a way that alters the fundamental behavior of the superclass.
2. Avoid throwing exceptions in place of valid behavior.
3. Ensure that the subclass can be used wherever the superclass is expected, without causing unexpected results.

**中文**:  
为了遵循 LSP 原则，子类应：
1. 避免以更改超类基本行为的方式重写方法。
2. 避免在有效行为的情况下抛出异常。
3. 确保在需要使用超类的地方，可以无缝使用子类而不会导致意外结果。

**Example of Adhering to LSP (遵循 LSP 的示例)**:

To avoid violating LSP in the above example, avoid using inheritance if the subclass behavior changes the contract of the superclass. Instead, consider using a different class hierarchy or composition to model the shapes correctly.

为了避免在上述示例中违反 LSP 原则，如果子类的行为改变了超类的约定，应避免使用继承。相反，可以考虑使用不同的类层次结构或组合来正确建模形状。

```csharp
// 使用接口表示形状，而不是使用继承
public interface IShape
{
    int GetArea();
}

public class Rectangle : IShape
{
    public int Width { get; set; }
    public int Height { get; set; }

    public int GetArea()
    {
        return Width * Height;
    }
}

public class Square : IShape
{
    public int SideLength { get; set; }

    public int GetArea()
    {
        return SideLength * SideLength;
    }
}
```

By using the `IShape` interface, we define a common contract without forcing a `Square` to behave like a `Rectangle`, thus adhering to LSP.

通过使用 `IShape` 接口，我们定义了一个通用约定，而不会强迫 `Square` 的行为与 `Rectangle` 相同，从而遵循 LSP 原则。
