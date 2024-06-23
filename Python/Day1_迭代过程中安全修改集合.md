# 迭代过程中安全修改集合
The problem you're addressing involves modifying a collection while iterating over it, which can lead to unexpected behavior or errors in many programming languages, including Python. The strategies you mentioned are common ways to safely modify collections during iteration.

您提到的问题涉及在迭代集合时修改它，这在包括Python在内的许多编程语言中可能会导致意外行为或错误。您提到的策略是在迭代过程中安全修改集合的常见方法。

Here's a breakdown of each strategy provided in your code:

以下是您代码中每种策略的详细说明：

1. **Iterate over a copy**: This strategy involves creating a copy of the original collection using `.copy()` method and iterating over the copy. Changes like deletions are made to the original collection based on the conditions evaluated during the iteration over the copy. This prevents modifying the collection while directly iterating over it, which can cause issues.

    **迭代一个副本**：这种策略涉及使用`.copy()`方法创建原始集合的副本，并对副本进行迭代。根据在迭代副本期间评估的条件，对原始集合进行诸如删除之类的更改。这可以防止在直接迭代过程中修改集合，这可能会导致问题。

2. **Create a new collection**: Instead of modifying the original collection, this strategy involves creating a completely new collection during the iteration. You add only the desired items to the new collection based on specific conditions. This method is very clean and leaves the original collection unchanged if needed for other purposes.

    **创建一个新集合**：这种策略不是修改原始集合，而是在迭代过程中创建一个全新的集合。根据特定条件，只将所需项目添加到新集合中。这种方法非常干净，并且如果出于其他目的需要，可以保留原始集合不变。

Here is a comparison table to further clarify these strategies:

以下是一个比较表，进一步阐明这些策略：

| Strategy | Description in English | Description in Chinese | Use Case |
|----------|------------------------|------------------------|----------|
| Iterate over a copy | Makes changes to the original collection while iterating over a copy to avoid errors. | 在迭代副本的同时对原始集合进行修改，以避免错误。 | Useful when modifications involve removing items. |
| Create a new collection | Builds a new collection based on conditions, leaving the original untouched. | 根据条件构建新集合，保留原始集合不变。 | Preferred when you need to filter items without affecting the original data. |

Each strategy has its use depending on the context and what operations are intended on the data.

每种策略的使用取决于上下文和数据上打算进行的操作。

Certainly! Here are the explanations along with the code examples for each strategy you've outlined:

当然！这里是您概述的每种策略的解释和代码示例：

1. **Iterate over a copy**:
    - **Description**: This approach involves making a copy of the collection and iterating over this copy. Changes are applied to the original collection. It is safe to modify the original collection during iteration as you are not directly iterating over it.
    - **Code Example**:

```python
# Create a sample collection
users = {'Hans': 'active', 'Éléonore': 'inactive', '景太郎': 'active'}

# Iterate over a copy
for user, status in users.copy().items():
    if status == 'inactive':
        del users[user]

print(users)  # Output will show that 'Éléonore' has been removed
```

**迭代一个副本**：
- **描述**：这种方法涉及复制集合并迭代这个副本。更改应用于原始集合。由于您没有直接迭代它，因此在迭代期间修改原始集合是安全的。
- **代码示例**：

```python
# 创建一个样本集合
users = {'Hans': 'active', 'Éléonore': 'inactive', '景太郎': 'active'}

# 迭代一个副本
for user, status in users.copy().items():
    if status == 'inactive':
        del users[user]

print(users)  # 输出将显示已删除'Éléonore'
```

2. **Create a new collection**:
    - **Description**: Instead of modifying the existing collection, this method creates a new collection and populates it based on certain conditions. This leaves the original collection unchanged.
    - **Code Example**:

```python
# Create a sample collection
users = {'Hans': 'active', 'Éléonore': 'inactive', '景太郎': 'active'}

# Create a new collection
active_users = {}
for user, status in users.items():
    if status == 'active':
        active_users[user] = status

print(active_users)  # Output will show only active users
```

**创建一个新集合**：
- **描述**：这种方法不是修改现有集合，而是创建一个新集合并根据某些条件填充它。这将保留原始集合不变。
- **代码示例**：

```python
# 创建一个样本集合
users = {'Hans': 'active', 'Éléonore': 'inactive', '景太郎': 'active'}

# 创建一个新集合
active_users = {}
for user, status in users.items():
    if status == 'active':
        active_users[user] = status

print(active_users)  # 输出将只显示活跃用户
```

These strategies are particularly useful in scenarios where you need to modify collections based on dynamic conditions, ensuring that you don't encounter runtime errors or unexpected behavior. 

这些策略在您需要根据动态条件修改集合的场景中特别有用，确保您不会遇到运行时错误或意外行为。
