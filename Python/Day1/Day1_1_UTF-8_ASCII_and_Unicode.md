# UTF-8, ASCII, and Unicode
默认情况下，Python 源码文件的编码是 UTF-8。这种编码支持世界上大多数语言的字符，可以用于字符串字面值、变量、函数名及注释 —— 尽管标准库只用常规的 ASCII 字符作为变量名或函数名，可移植代码都应遵守此约定。

**要正确显示这些字符，编辑器必须能识别 UTF-8 编码，而且必须使用支持文件中所有字符的字体.**

Understanding the differences between UTF-8, ASCII, and Unicode is essential for handling text in various computing environments. Here's a detailed comparison presented in a markdown table to clarify these concepts:

| Feature                | ASCII                         | Unicode                          | UTF-8                                         |
|------------------------|-------------------------------|----------------------------------|-----------------------------------------------|
| **Definition**         | A character encoding standard based on English characters. | A comprehensive character encoding standard that includes every character from all the languages of the world. | An encoding format used to encode Unicode characters, capable of representing any character in any language. |
| **Character Set**      | Limited to 128 characters (0-127), primarily English letters, digits, and control characters. | Over 143,000 characters covering 154 modern and historic scripts, as well as multiple symbol sets. | Can represent all characters in the Unicode standard. |
| **Byte Usage**         | Single byte per character (7 bits actually used). | Varies; UTF-16 uses 2 or 4 bytes per character, UTF-32 uses 4 bytes per character. | Variable; 1-4 bytes per character, optimized for characters that are more common in text. |
| **Compatibility**      | Widely compatible with older systems. | Universal character set that includes ASCII as a subset. | Fully compatible with ASCII for the first 128 characters; additional bytes used for characters outside this range. |
| **Use Case**           | Predominantly used in older systems, simple text files where only English letters and common symbols are sufficient. | Needed for applications requiring a broad variety of characters from different languages and symbols. | Preferred in web and multi-language environments due to its efficiency and compatibility. |
| **Efficiency**         | Most efficient for texts containing only characters from the basic ASCII set. | Less efficient than UTF-8 for texts primarily in English due to fixed width of characters in some encodings (e.g., UTF-32). | Highly efficient for texts that mix ASCII characters with other global scripts. |

**ASCII** is basic and limited but highly efficient for English-only texts. **Unicode** is comprehensive, covering all characters needed for global languages but can be more storage-intensive depending on the encoding form (UTF-16, UTF-32). **UTF-8** strikes a balance, efficiently encoding ASCII while also capable of handling any Unicode character, making it ideal for the internet and global applications.

理解 UTF-8、ASCII 和 Unicode 之间的差异对于处理各种计算环境中的文本至关重要。这里提供了一个详细的比较表格，以阐明这些概念：

| 特点                    | ASCII                               | Unicode                                            | UTF-8                                           |
|------------------------|-------------------------------------|----------------------------------------------------|-------------------------------------------------|
| **定义**               | 基于英文字符的字符编码标准。                | 包括世界上所有语言的每个字符的综合字符编码标准。                       | 用于编码 Unicode 字符的编码格式，能够表示任何语言的任何字符。         |
| **字符集**             | 限于128个字符（0-127），主要是英文字母、数字和控制字符。  | 超过143,000个字符，涵盖154种现代和历史脚本以及多种符号集。            | 能表示 Unicode 标准中的所有字符。                           |
| **字节使用**           | 每个字符使用单个字节（实际使用7位）。          | 变化；UTF-16 使用 2 或 4 字节每个字符，UTF-32 使用 4 字节每个字符。 | 变量；每个字符 1-4 字节，针对文本中更常见的字符进行优化。             |
| **兼容性**             | 与旧系统广泛兼容。                        | 包括 ASCII 作为子集的通用字符集。                            | 对于前128个字符完全兼容 ASCII；对范围之外的字符使用额外的字节。      |
| **使用场景**           | 主要用于只需要英文字母和常见符号的旧系统和简单文本文件。  | 需要广泛的不同语言字符和符号的应用程序。                             | 由于其效率和兼容性，被优先用于 Web 和多语言环境。                   |
| **效率**               | 对于只包含基本 ASCII 集的文本最为高效。          | 由于某些编码（例如 UTF-32）的字符固定宽度，对于主要是英文的文本来说效率较低。 | 对于混合使用 ASCII 字符和其他全球脚本的文本非常高效。                 |

**ASCII** 是基础而有限的，但对于仅英文文本非常高效。**Unicode** 是全面的，涵盖了全球语言所需的所有字符，但根据编码形式（UTF-16、UTF-32）可能需要更多存储空间。**UTF-8** 取得了平衡，有效编码 ASCII 的同时也能处理任何 Unicode 字符，使其成为互联网和全球应用的理想选择。


### Unicode vs UTF-8

Here is a comparison of Unicode and UTF-8 explained in a simple way, presented in a markdown table with code examples:


| Concept  | English Explanation | Chinese Explanation | Code Example |
|----------|----------------------|---------------------|--------------|
| **Unicode** | Unicode is a standard for representing all the characters from all the writing systems in the world. | Unicode 是一种用于表示世界上所有书写系统中的所有字符的标准。 | `char = 'A'; code_point = ord(char); print(code_point)  # Output: 65` |
|          | It assigns a unique number (code point) to every character. | 它为每个字符分配一个唯一的号码（码点）。 | `char = '€'; code_point = ord(char); print(code_point)  # Output: 8364` |
|          | For example, the code point for 'A' is U+0041. | 例如，字母 'A' 的码点是 U+0041。 | `char = 'A'; code_point = ord(char); print(hex(code_point))  # Output: 0x41` |
| **UTF-8** | UTF-8 is a way to encode Unicode characters into bytes. | UTF-8 是一种将 Unicode 字符编码成字节的方法。 | `char = 'A'; utf8_bytes = char.encode('utf-8'); print(utf8_bytes)  # Output: b'A'` |
|          | It uses one to four bytes for each character, depending on the character. | 根据字符的不同，它使用一到四个字节来表示每个字符。 | `char = '€'; utf8_bytes = char.encode('utf-8'); print(utf8_bytes)  # Output: b'\xe2\x82\xac'` |
|          | For example, the character 'A' is encoded as one byte (0x41), while '€' is encoded as three bytes (0xE2 0x82 0xAC). | 例如，字符 'A' 编码为一个字节 (0x41)，而字符 '€' 编码为三个字节 (0xE2 0x82 0xAC)。 | `char = '€'; utf8_bytes = char.encode('utf-8'); print(list(utf8_bytes))  # Output: [226, 130, 172]` |



