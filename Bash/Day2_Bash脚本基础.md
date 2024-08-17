# Bash脚本基础

Bash脚本是一种强大的工具，广泛用于自动化任务、管理系统和处理数据流。学习Bash脚本的基础编写可以让你在Linux和其他类Unix系统上更加高效地工作。本课程将介绍Bash脚本的基本概念、变量的定义与使用，以及简单的控制结构如`if-else`、`for`和`while`循环。

## 学习目标

1. **掌握Bash脚本的基础编写**  
   你将学习如何创建、编辑和运行Bash脚本，并理解其基本语法。

2. **了解变量与简单控制结构**  
   你将了解如何在Bash脚本中定义和使用变量，并掌握基本的控制结构，用于构建条件逻辑和循环。

## 学习内容

### 1. 脚本编写基础：如何编写和运行Bash脚本

Bash脚本是由一系列命令组成的文件，通常以`.sh`为扩展名。以下是编写和运行Bash脚本的基本步骤：

1. **创建脚本文件**  
   使用文本编辑器创建一个新文件，例如`script.sh`。

   ```bash
   nano script.sh
   ```

2. **添加shebang**  
   在脚本的第一行添加`shebang`，指定使用`/bin/bash`解释器来运行脚本。

   ```bash
   #!/bin/bash
   ```

3. **编写脚本内容**  
   在shebang之后，添加你希望执行的命令。例如：

   ```bash
   #!/bin/bash
   echo "Hello, World!"
   ```

4. **保存并关闭文件**  
   保存你的脚本并关闭编辑器。

5. **赋予执行权限**  
   使用`chmod`命令赋予脚本可执行权限。

   ```bash
   chmod +x script.sh
   ```

6. **运行脚本**  
   通过在命令行中调用脚本文件来运行它。

   ```bash
   ./script.sh
   ```

### 2. 变量：定义和使用

Bash脚本中的变量可以存储字符串、数字或命令的输出。定义变量不需要类型声明，变量名通常由字母和数字组成，区分大小写。

1. **定义变量**  
   使用`=`符号定义变量。注意，`=`两侧不能有空格。

   ```bash
   my_variable="Hello"
   ```

2. **访问变量**  
   使用`$`符号来引用变量的值。

   ```bash
   echo $my_variable
   ```

3. **读取用户输入**  
   使用`read`命令读取用户输入，并将其存储在变量中。

   ```bash
   echo "Enter your name:"
   read user_name
   echo "Hello, $user_name!"
   ```

4. **命令替换**  
   使用反引号`` ` ``或`$()`将命令的输出存储在变量中。

   ```bash
   current_date=$(date)
   echo "Today is $current_date"
   ```

### 3. 简单的控制结构：if-else, for, while

控制结构允许你根据条件执行不同的代码块或重复执行代码。

#### 1. **if-else 结构**

`if`语句用于条件判断，如果条件为真，执行相应的代码块。`else`可以用于处理条件为假的情况。

```bash
#!/bin/bash
echo "Enter a number:"
read number

if [ $number -gt 10 ]; then
    echo "The number is greater than 10."
else
    echo "The number is 10 or less."
fi
```

#### 2. **for 循环**

`for`循环用于遍历列表或范围内的元素。

```bash
#!/bin/bash
for i in {1..5}; do
    echo "Iteration $i"
done
```

#### 3. **while 循环**

`while`循环在条件为真时重复执行代码块。

```bash
#!/bin/bash
counter=1
while [ $counter -le 5 ]; do
    echo "Counter is $counter"
    ((counter++))
done
```

### 总结

通过本课程，你已经学习了如何编写和运行Bash脚本，如何定义和使用变量，以及如何利用基本的控制结构（如`if-else`、`for`和`while`循环）来构建逻辑。掌握这些基础知识后，你可以进一步探索更复杂的脚本编写，以自动化更复杂的任务。Bash脚本是一项非常有用的技能，在系统管理、数据处理和自动化工作流程中具有广泛的应用。
