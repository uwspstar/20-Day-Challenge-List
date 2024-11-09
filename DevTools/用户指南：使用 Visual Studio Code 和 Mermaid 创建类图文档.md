### 用户指南：使用 Visual Studio Code 和 Mermaid 创建类图文档

本指南将带您在 Visual Studio Code（VS Code）中创建和使用 Mermaid 语法来创建类图，并将其应用到代码文档中。这种方法非常适合可视化类结构和工作流程，提升代码文档的可读性和理解性。

---

### 1. **在 Visual Studio Code 中配置 Mermaid**

1. **安装 Visual Studio Code**：
   - 从 [Visual Studio Code](https://code.visualstudio.com/) 下载并安装 VS Code。

2. **安装 Mermaid 扩展**：
   - 打开 VS Code，进入 **扩展** 面板（通常在左侧边栏）。
   - 搜索“Markdown Preview Mermaid Support”或“Mermaid Markdown Syntax Highlighting”。
   - 安装其中一个扩展，以便在 Markdown 文件中支持 Mermaid 语法。

3. **（可选）安装 Markdown Preview Enhanced 扩展**：
   - 可以选择搜索并安装 “Markdown Preview Enhanced” 扩展。
   - 该扩展提供了更丰富的 Markdown 文件预览功能，包括对 Mermaid 图的更佳支持。

---

### 2. **在 VS Code 中创建 Mermaid 类图**

1. **创建新文件**：
   - 在 VS Code 中创建一个 `.md` 文件（例如 `ClassDiagram.md`），Markdown 文件适合文档编写，因为它支持文本和代码格式。

2. **添加 Mermaid 图形代码块**：
   - 在 Markdown 文件中，插入一个代码块，指定 `mermaid` 作为代码语言，这样会启用 Mermaid 语法高亮显示和预览。

   ```markdown
   ```mermaid
   classDiagram
   ```

3. **编写 Mermaid 类图代码**：
   - 使用 Mermaid 语法定义类、关系和方法。以下是基于 `GlobalConfigurationCache` 类的示例。

   ```markdown
   ```mermaid
   classDiagram
       class GlobalConfigurationCache {
           - ReaderWriterLockSlim _lock
           - Dictionary~int, string~ _cache
           + void Add(int key, string value)
           + string? Get(int key)
       }

       class ReaderWriterLockSlim {
           + EnterWriteLock()
           + EnterReadLock()
           + ExitWriteLock()
           + ExitReadLock()
       }

       class Dictionary~int, string~ {
           + TryGetValue(int key, string value) string?
       }

       GlobalConfigurationCache --> ReaderWriterLockSlim : uses
       GlobalConfigurationCache --> Dictionary~int, string~ : contains

       GlobalConfigurationCache : + Add(int key, string value)
       GlobalConfigurationCache : + Get(int key)

       class AddMethod {
           - bool lockAcquired
           + EnterWriteLock()
           + Add to _cache
           + ExitWriteLock()
       }

       class GetMethod {
           - bool lockAcquired
           + EnterReadLock()
           + TryGetValue from _cache
           + ExitReadLock()
       }

       GlobalConfigurationCache --> AddMethod : calls
       GlobalConfigurationCache --> GetMethod : calls
   ```
   ```

4. **预览图形**：
   - 在 Markdown 文件中右键点击，选择 **Preview Mermaid**（如果扩展支持）或 **Markdown Preview Enhanced**。
   - VS Code 会显示 Mermaid 图的预览，您可以在此进行可视化查看和调整。

---

### 3. **Mermaid 类图的基本语法**

- **定义类**：
  - 使用 `class ClassName` 定义类。
  - 在大括号 `{}` 内添加属性和方法。

  ```mermaid
  class ExampleClass {
      - int attribute
      + void method()
  }
  ```

- **定义关系**：
  - 使用 `-->` 表示类之间的关系。
  - 在箭头后添加 `: 关系名称` 来标注关系。

  ```mermaid
  ClassA --> ClassB : uses
  ```

- **访问修饰符**：
  - 使用 `+` 表示公共，`-` 表示私有，`#` 表示保护访问。
  - 可以在属性和方法后添加类型和返回类型。

---

### 4. **示例：为 `GlobalConfigurationCache` 生成文档**

以下是使用前面示例的 `GlobalConfigurationCache` 类结构的 Mermaid 文档步骤：

1. **定义主要类及其属性**：
   - 定义 `GlobalConfigurationCache`，包含私有属性 `_lock` 和 `_cache`。
   - 列出公共方法 `Add` 和 `Get`。

   ```mermaid
   class GlobalConfigurationCache {
       - ReaderWriterLockSlim _lock
       - Dictionary~int, string~ _cache
       + void Add(int key, string value)
       + string? Get(int key)
   }
   ```

2. **定义支持类**：
   - 添加 `ReaderWriterLockSlim` 类，包含进入和退出读/写锁的方法。
   - 定义 `Dictionary<int, string>` 类，包含用于缓存读取的 `TryGetValue` 方法。

   ```mermaid
   class ReaderWriterLockSlim {
       + EnterWriteLock()
       + EnterReadLock()
       + ExitWriteLock()
       + ExitReadLock()
   }

   class Dictionary~int, string~ {
       + TryGetValue(int key, string value) string?
   }
   ```

3. **添加关系**：
   - 定义 `GlobalConfigurationCache` 使用 `ReaderWriterLockSlim`，并包含 `Dictionary<int, string>`。

   ```mermaid
   GlobalConfigurationCache --> ReaderWriterLockSlim : uses
   GlobalConfigurationCache --> Dictionary~int, string~ : contains
   ```

4. **将方法作为独立类（可选）**：
   - 可以创建单独的类如 `AddMethod` 和 `GetMethod` 来进一步细化逻辑。

   ```mermaid
   class AddMethod {
       - bool lockAcquired
       + EnterWriteLock()
       + Add to _cache
       + ExitWriteLock()
   }

   class GetMethod {
       - bool lockAcquired
       + EnterReadLock()
       + TryGetValue from _cache
       + ExitReadLock()
   }

   GlobalConfigurationCache --> AddMethod : calls
   GlobalConfigurationCache --> GetMethod : calls
   ```

---

### 5. **保存和导出图形**

完成图形创建后：

- **保存 Markdown 文件**：您的 Mermaid 代码和文档保存在 `.md` 文件中。
- **导出为图片（可选）**：
   - 如果使用 **Markdown Preview Enhanced**，可以右键点击图形预览并选择 **Export to PNG/SVG**。
   - 这样可以生成图片文件，用于演示或在 VS Code 之外的文档中使用。

---

### 6. **VS Code 中使用 Mermaid 的其他提示**

- **保持图形简单**：从高层次概述开始，逐步添加细节。
- **使用注释**：可以在 Mermaid 代码中使用 `%%` 添加注释，便于协作或添加更新说明。
- **参考 Mermaid 文档**：了解 Mermaid 的高级功能可以参考 [Mermaid 官方文档](https://mermaid-js.github.io/mermaid/#/)。

---

通过本指南，您可以在 VS Code 中使用 Mermaid 来有效地记录类结构。这种方法使您能够在代码库中直接创建、可视化和优化类图，大大提高了代码文档的可读性。
