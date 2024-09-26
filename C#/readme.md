# C# interview questions
---
As of September 2024, the current versions of C#, .NET Core, and .NET are as follows:

1. **C# Version**: C# 12 is the latest stable release. It introduces several new features, including primary constructors for classes and structs, collection expressions, `ref readonly` parameters, and more. C# 12 is compatible with .NET 8【8†source】.

2. **.NET Core Version**: .NET Core has evolved into the broader .NET ecosystem, with the current version being **.NET 8 (LTS)**. The latest release for .NET 8 is version 8.0.8, with long-term support ending in November 2026【9†source】【10†source】.

3. **.NET Version**: The latest .NET release is **.NET 9**, currently available as a **release candidate (9.0.0-rc.1)**. The official release is expected in November 2024【8†source】【9†source】.

---

- **[Question 1 - 50](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/C%23/1-50%20Interview%20Questions.md)**
- **[Question 51 - 100](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/C%23/51-100%20Interview%20Questions.md)**
- **[Question 101 - 149](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/C%23/101-149%20Interview%20Questions.md)**
- **[Question 150 - 164](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/C%23/150-164%20Interview%20Questions.md)**

----

- [How Does Garbage Collection Work in C#?](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/C%23/How%20Does%20Garbage%20Collection%20Work%20in%20C%23.md)
- [What is Entity Framework?](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/C%23/Entity%20Framework.md)
- [What is LINQ?](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/C%23/LINQ.md)
- [Task vs Thread vs Process vs Parallelism](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/C%23/Task%2C%20Thread%2C%20Process%2C%20and%20Parallelis.md)



----
1. [Explain the difference between .NET and C#?]()
2. .NET Framework vs .NET Core vs .NET 5.0
3. What is IL (Intermediate Language) Code?
4. What is the use of JIT (Just In Time compiler)?
5. Is it possible to view IL code?
6. What is the benefit of compiling into IL code?
7. Does .NET support multiple programming languages?
8. What is CLR (Common Language Runtime)?
9. [What is managed and unmanaged code?]()
10. [Explain the importance of the Garbage Collector?]()
11. Can the garbage collector claim unmanaged objects?
12. What is the importance of CTS?
13. Explain CLS (Common Language Specification)?
14. Difference between Stack vs Heap?
15. What are Value types & Reference types?
16. Explain boxing and unboxing?
17. What are the consequences of boxing and unboxing?
18. Explain casting, implicit casting, and explicit casting?
19. What can happen during explicit casting?
20. Differentiate between Array and ArrayList?
21. Whose performance is better, Array or ArrayList?
22. [What are generic collections?]()
23. [What are threads (Multithreading)?]
24. [How are threads different from TPL (Task Parallel Library)?]()
25. How do we handle exceptions in C# (try/catch)?
26. What is the need for the 'finally' block?
27. Why do we need the 'out' keyword?
28. What is the need for Delegates?
29. What are events?
30. What's the difference between an Abstract class and an Interface?
31. What is a Delegate and how to create a Delegate?
32. Where have you used Delegates?
33. What is a Multicast Delegate?
34. What is an Event?
35. How to Create an Event?
36. Delegate vs Events.
37. Why do we need OOP (Object-Oriented Programming)?
38. What are the important pillars of OOPs?
39. What is a class and object?
40. [Abstraction vs Encapsulation?]()
41. Explain Inheritance?
42. Explain the 'virtual' keyword?
43. What is overriding?
44. Explain overloading?
45. Overloading vs Overriding?
46. Explain static vs dynamic polymorphism?
47. Explain operator overloading?
48. [Why do we need Abstract classes?]
49. Are Abstract methods virtual?
50. Can we create an instance of Abstract classes?
51. Is it compulsory to implement Abstract methods?
52. Why simple base class can replace an Abstract class?
53. Explain interfaces and why do we need them?
54. [Can we write logic in an interface?]
55. Can we define methods as private in an interface?
56. If I want to change an interface, what's the best practice?
57. Explain multiple inheritance in Interface?
58. Explain Interface Segregation Principle (ISP)?
59. Can we create an instance of an interface?
60. Can we do multiple inheritance with Abstract classes?
61. [Abstract Class vs Interface?]
62. Why do we need constructors?
63. In parent-child inheritance, which constructor fires first?
64. How are initializers executed?
65. How are static constructors executed in parent-child inheritance?
66. When does the static constructor fire?
67. What is shadowing?
68. Explain method hiding?
69. Shadowing vs Overriding?
70. When do we need Shadowing?
71. Explain Sealed Classes?
72. Can we create an instance of sealed classes?
73. What are nested classes and when to use them?
74. Can a nested class access outer class variables?
75. Can we have public/protected access modifiers in nested classes?
76. Explain Partial classes?
77. In what scenarios do we use partial classes?
78. [What is SOLID?]
79. What is the full form of SOLID?
80. What is the goal of SOLID?
81. Explain SRP (Single Responsibility Principle) with an example?
82. What is the benefit of SRP?
83. Explain OCP (Open-Closed Principle) with an example?
84. What is the benefit of OCP?
85. Can you explain Liskov Substitution Principle and its violation?
86. How can we fix Liskov Substitution Principle violation?
87. Explain Dependency Injection with an example?
88. Explain IoC (Inversion of Control)?
89. [What are design patterns?]
90. What are the different types of design patterns?
91. Explain Structural, Behavioral, and Creational design patterns?
92. Explain the Singleton Pattern and its use?
93. [How did you implement the Singleton pattern?]
94. Can we use a static class instead of using a private constructor in a Singleton?
95. [Static vs Singleton pattern?]
96. How did you implement thread safety in Singleton?
97. What is double-null check in Singleton?
98. Can the Singleton pattern code be made easy with the Lazy keyword?
99. Can we get rid of double-null check code in Singleton?
100. What is composition?
101. Explain Aggregation.
102. Explain Association.
103. Differentiate between Composition vs Aggregation vs Association.
104. UML Symbols for Composition, Aggregation, and Association.
105. Explain Stack and Heap.
106. Where are Stack and Heap stored?
107. What goes on Stack and what goes on Heap?
108. How is the Stack memory address arranged?
109. How is Stack memory deallocated (LIFO or FIFO)?
110. How are primitive types and objects stored in memory?
111. Can primitive data types be stored in Heap?
112. Explain value types and reference types.
113. Explain 'ByVal' and 'ByRef'.
114. Differentiate between copy by value and copy by reference.
115. What is boxing and unboxing?
116. Is boxing/unboxing good or bad?
117. Can we avoid boxing and unboxing?
118. What effect does boxing and unboxing have on performance?
119. Are strings allocated on Stack or Heap?
120. How many Stacks and Heaps are created for an application?
121. How are Stack and Heap memory deallocated?
122. Who clears the Heap memory?
123. Where is a structure allocated: Stack or Heap?
124. Are structures copied by value or by reference?
125. Can structures get created on Heap?
126. Explain the Garbage Collector (GC).
127. How does the Garbage Collector know when to clean objects?
128. Is there a way to view Heap memory?
129. Does the Garbage Collector clean primitive types?
130. Managed vs Unmanaged code/objects/resources?
131. Can the Garbage Collector clean unmanaged code?
132. Explain Generations in the Garbage Collector.
133. [What is GC0, GC1, and GC2?]
134. Why do we need Generations in the Garbage Collector?
135. Which is the best place to clean unmanaged objects?
136. How does the Garbage Collector behave when we have a destructor?
137. What do you think about an empty destructor?
138. [Explain the Dispose Pattern.]
139. Finalize vs Destructor.
140. [What is the use of the 'using' keyword?]
141. Can you force Garbage Collection?
142. Is it a good practice to force Garbage Collection?
143. How can we detect memory issues?
144. How can we know the exact source of memory issues?
145. [What is a memory leak?]
146. [Can a .NET application have memory leaks even with the Garbage Collector?]
147. [How to detect memory leaks in .NET applications?]
148. Explain weak and strong references.
149. When will you use weak references?
150. What are design patterns?
151. What are the different types of design patterns?
152. Explain Structural, Behavioral, and Creational design patterns.
153. Explain the Singleton Pattern and its use.
154. How did you implement the Singleton pattern?
155. Can we use a static class instead of a Singleton with a private constructor?
156. Static vs Singleton pattern.
157. How did you implement thread safety in Singleton?
158. What is double-null check in Singleton?
159. Can Singleton pattern code be made easier with the Lazy keyword?
160. Can we eliminate double-null check code?
