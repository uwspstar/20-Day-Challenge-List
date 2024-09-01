# Understanding Prefix and Suffix in Algorithms

[Back to 20天学 Algorithm](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/Algorithm/README.md)

### Introduction

In algorithm design, the concepts of prefix and suffix are fundamental techniques used to solve problems related to sequences, arrays, and strings. By leveraging prefix and suffix computations, you can often simplify complex problems, reduce time complexity, and improve the efficiency of your solution.

在算法设计中，前缀和后缀的概念是用于解决与序列、数组和字符串相关问题的基本技术。通过利用前缀和后缀计算，你通常可以简化复杂问题，减少时间复杂度，并提高解决方案的效率。

### What are Prefix and Suffix?

**Prefix:** A prefix of a sequence is a subsequence that starts from the beginning of the sequence and includes any number of leading elements up to the entire sequence.

**前缀：** 序列的前缀是从序列的开头开始并包含任意数量的前导元素的子序列，直到整个序列。

**Suffix:** A suffix of a sequence is a subsequence that starts from any position in the sequence and continues to the end of the sequence.

**后缀：** 序列的后缀是从序列中的任意位置开始并继续到序列末尾的子序列。

### Steps to Solve Problems Using Prefix and Suffix

#### 1. Understand the Problem

Clearly understand the problem statement, input, and expected output. Determine if the problem involves calculating cumulative values (e.g., sums, products) from the start or end of a sequence.

明确理解问题陈述、输入和预期输出。确定问题是否涉及从序列的开始或结束计算累积值（例如，总和、乘积）。

#### 2. Identify the Need for Prefix or Suffix

Identify whether the problem requires prefix sums/products (cumulative values from the start) or suffix sums/products (cumulative values from the end). Sometimes, a problem may require both.

确定问题是否需要前缀和/乘积（从开始的累积值）或后缀和/乘积（从末尾的累积值）。有时，一个问题可能需要两者。

#### 3. Develop the Algorithm

Outline the steps to compute the prefix or suffix values. Typically, this involves iterating through the sequence from the start (for prefix) or from the end (for suffix) and storing cumulative values in an array.

概述计算前缀或后缀值的步骤。通常，这涉及从开始（对于前缀）或从末尾（对于后缀）迭代序列，并将累积值存储在数组中。

#### 4. Handle Edge Cases

Consider edge cases such as empty arrays, single-element arrays, or cases where the entire sequence needs to be considered as a prefix or suffix.

考虑边界情况，例如空数组、单元素数组，或需要将整个序列视为前缀或后缀的情况。

### Example Problem: Product of Array Except Self

#### Problem Description

Given an array `nums` of `n` integers where `n > 1`, return an array `output` such that `output[i]` is equal to the product of all the elements of `nums` except `nums[i]`.

给定一个包含 `n` 个整数的数组 `nums`，其中 `n > 1`，返回一个数组 `output`，其中 `output[i]` 等于 `nums` 中除 `nums[i]` 之外的所有元素的乘积。

#### Steps to Solve

1. **Understand the Problem:**
   - For each element in the array, calculate the product of all other elements.
   - Ensure that the solution runs in O(n) time and does not use division.

   **理解问题：**
   - 对数组中的每个元素，计算所有其他元素的乘积。
   - 确保解决方案的运行时间为 O(n)，并且不使用除法。

2. **Identify the Need for Prefix or Suffix:**
   - We can solve this problem using prefix and suffix products.
   - The prefix product at index `i` is the product of all elements before `i`.
   - The suffix product at index `i` is the product of all elements after `i`.

   **确定前缀或后缀的需求：**
   - 我们可以使用前缀和后缀乘积来解决这个问题。
   - 索引 `i` 处的前缀乘积是索引 `i` 之前所有元素的乘积。
   - 索引 `i` 处的后缀乘积是索引 `i` 之后所有元素的乘积。

3. **Develop the Algorithm:**
   - Create an array to store the prefix products.
   - Create another array to store the suffix products.
   - For each element, multiply the corresponding prefix and suffix products to get the result.

   **开发算法：**
   - 创建一个数组来存储前缀乘积。
   - 创建另一个数组来存储后缀乘积。
   - 对于每个元素，乘以相应的前缀和后缀乘积以获得结果。

4. **Handle Edge Cases:**
   - Consider cases with minimum and maximum array sizes.
   - Handle cases where all elements are the same.

   **处理边界情况：**
   - 考虑最小和最大数组大小的情况。
   - 处理所有元素相同的情况。

#### Example Solution

```python
def product_except_self(nums):
    n = len(nums)
    if n == 0:
        return []
    
    prefix_products = [1] * n
    suffix_products = [1] * n
    
    # Calculate prefix products
    for i in range(1, n):
        prefix_products[i] = prefix_products[i - 1] * nums[i - 1]
    
    # Calculate suffix products
    for i in range(n - 2, -1, -1):
        suffix_products[i] = suffix_products[i + 1] * nums[i + 1]
    
    # Calculate the result by multiplying prefix and suffix products
    result = [prefix_products[i] * suffix_products[i] for i in range(n)]
    
    return result
```

#### Explanation

1. **Step 1: Initialize Data Structures**
   - Create `prefix_products` and `suffix_products` arrays, both initialized to `1`.
   - 步骤 1：初始化数据结构
   - 创建 `prefix_products` 和 `suffix_products` 数组，均初始化为 `1`。

2. **Step 2: Calculate Prefix and Suffix Products**
   - Calculate the prefix products by iterating from left to right.
   - Calculate the suffix products by iterating from right to left.
   - 步骤 2：计算前缀和后缀乘积
   - 通过从左到右迭代计算前缀乘积。
   - 通过从右到左迭代计算后缀乘积。

3. **Step 3: Calculate the Result**
   - Multiply the corresponding prefix and suffix products to get the final result for each element.
   - 步骤 3：计算结果
   - 乘以相应的前缀和后缀乘积以获得每个元素的最终结果。

#### Example Usage

```python
# Example Usage:
# 示例用法：
nums = [1, 2, 3, 4]
print(product_except_self(nums))  # 输出: [24, 12, 8, 6]
```

### Conclusion

The use of prefix and suffix arrays is a powerful technique in algorithm design, particularly for problems involving cumulative operations. By calculating these arrays, you can often simplify the problem, reduce complexity, and achieve more efficient solutions.

使用前缀和后缀数组是算法设计中的一种强大技术，特别适用于涉及累积操作的问题。通过计算这些数组，你通常可以简化问题，降低复杂性，并实现更高效的解决方案。

Whether you're dealing with sum, product, or other operations, understanding and applying prefix and suffix techniques will significantly enhance your problem-solving skills in competitive programming and coding interviews.

无论你是在处理求和、乘积还是其他操作，理解并应用前缀和后缀技术将显著提升你在竞争编程和编码面试中的问题解决能力。
