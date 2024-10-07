1. **What is the difference between `virtual` and `override` in C#?**  
   **C# 中 `virtual` 和 `override` 的区别是什么？**  
   - **Answer**:  
     - `virtual` is used in the base class to indicate that a method or property can be overridden in derived classes, providing a default implementation.  
       `virtual` 用于基类中，表示方法或属性可以在派生类中被重写，并提供默认实现。
     - `override` is used in the derived class to modify the behavior of the virtual method or property defined in the base class. It replaces the base class implementation with a new one.  
       `override` 用于派生类中，用于修改基类中定义的虚方法或属性的行为。它用新的实现替换了基类的实现。

2. **Can a derived class override a non-virtual method in the base class? Why or why not?**  
   **派生类能否重写基类中的非虚方法？为什么能或不能？**  
   - **Answer**:  
     - No, a derived class cannot override a non-virtual method in the base class. This is because only methods marked as `virtual`, `abstract`, or already overridden using the `override` keyword can be overridden in derived classes. Non-virtual methods are not designed to be changed by derived classes.  
       不能，派生类不能重写基类中的非虚方法。这是因为只有被标记为 `virtual`、`abstract` 或已用 `override` 关键字重写的方法才能在派生类中被重写。非虚方法的设计初衷就是不允许派生类进行更改。

3. **How would you call a base class method from a derived class in C#?**  
   **在 C# 中如何从派生类调用基类方法？**  
   - **Answer**:  
     - In a derived class, you can call the base class method using the `base` keyword followed by the method name, like `base.MethodName()`. This allows the derived class to access the base class implementation of the method.  
       在派生类中，可以使用 `base` 关键字加上方法名来调用基类方法，如 `base.MethodName()`。这样可以让派生类访问基类方法的实现。  
     - Example 示例:  
       ```csharp
       public override void Speak()  
       {  
           base.Speak();  // Calls the base class Speak method  
           Console.WriteLine("Dog barks.");  // Additional functionality in the derived class  
       }  
       ```
     - In this example, `base.Speak()` calls the base class method before adding new functionality in the derived class.  
       在这个示例中，`base.Speak()` 调用了基类方法，然后在派生类中添加了新功能。

4. **What is the difference between `new` and `override` keywords in C#?**  
   **C# 中 `new` 和 `override` 关键字的区别是什么？**  
   - **Answer**:  
     - The `override` keyword extends or modifies the base class method that is marked as `virtual`. The derived class provides its own implementation for that method, while still allowing polymorphic behavior.  
       `override` 关键字用于扩展或修改基类中被标记为 `virtual` 的方法。派生类为该方法提供了自己的实现，同时仍允许多态行为。
     - The `new` keyword, on the other hand, hides the base class method instead of overriding it. This means that the base class method and the derived class method are two separate methods that do not exhibit polymorphic behavior.  
       而 `new` 关键字则隐藏了基类方法，而不是重写它。这意味着基类方法和派生类方法是两个独立的方法，它们不具备多态行为。  
     - Example 示例:  
       ```csharp
       public class Animal  
       {  
           public virtual void Speak()  
           {  
               Console.WriteLine("Animal makes a sound.");  
           }  
       }

       public class Cat : Animal  
       {  
           public new void Speak()  // Hides the base class method, no polymorphism  
           {  
               Console.WriteLine("Cat meows.");  
           }  
       }
       ```
     - In this example, calling `Animal myCat = new Cat(); myCat.Speak();` will output "Animal makes a sound." because `new` keyword hides, but does not override the base class method.  
       在这个例子中，调用 `Animal myCat = new Cat(); myCat.Speak();` 会输出“Animal makes a sound.”，因为 `new` 关键字隐藏了但没有重写基类方法。

5. **When should you use `virtual` vs `abstract` in a base class?**  
   **基类中应何时使用 `virtual` 与 `abstract`？**  
   - **Answer**:  
     - Use `virtual` when you want to provide a base implementation that derived classes can optionally override. It allows derived classes to either use the base implementation or provide their own.  
       当希望提供一个基类实现，并允许派生类选择性地重写时，使用 `virtual`。这允许派生类使用基类实现或提供自己的实现。  
     - Use `abstract` when you want to enforce that derived classes must provide an implementation for the method. An abstract method has no body and must be overridden in all non-abstract derived classes.  
       当希望强制派生类必须为该方法提供实现时，使用 `abstract`。抽象方法没有方法体，必须在所有非抽象派生类中被重写。

---

This covers the commonly asked interview questions about `virtual` and `override` in C#. Let me know if you need more detailed explanations or additional questions!  
这就涵盖了有关 C# 中 `virtual` 和 `override` 的常见面试问题。请告诉我是否需要更详细的解释或其他问题！
