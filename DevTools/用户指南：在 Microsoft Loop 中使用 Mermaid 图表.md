### 用户指南：在 Microsoft Loop 中使用 Mermaid 图表

Microsoft Loop 支持使用 Mermaid 语法，让您可以直接在协作文档中创建图表、流程图和其他视觉效果。按照本指南开始在 Loop 中使用 Mermaid。

---

#### 1. **检查 Mermaid 支持**
   - **注意**：Microsoft Loop 正在逐步推出对 Mermaid 语法的支持，不同设备上的可用性可能有所不同。如果您在一个设备上看不到 Mermaid 选项，尝试使用其他设备或检查是否有可用更新。

#### 2. **创建 Mermaid 图表**
   1. **打开 Microsoft Loop** 并进入您希望插入 Mermaid 图表的页面。
   2. **插入代码块**：
      - 输入 `/code` 以显示代码块选项。
      - 选择代码块并将语言设置为 `mermaid`。
   3. **添加 Mermaid 语法**：
      - 在代码块中编写您的 Mermaid 代码以生成所需的图表。例如：
        ```mermaid
        graph TD;
          A-->B;
          B-->C;
          C-->D;
          D-->A;
        ```
      - 以上语法将创建一个连接节点 A、B、C 和 D 的循环流程图。

#### 3. **图表示例**
   - **流程图**：展示节点和链接的基本流程：
     ```mermaid
     flowchart LR
       Start --> Process1 --> Decision{是否正确？} 
       Decision -- 是 --> End
       Decision -- 否 --> Process1
     ```
   - **甘特图**：
     ```mermaid
     gantt
       title 项目时间表
       section 开发阶段
       任务1 :a1, 2023-01-01, 30d
       任务2 :after a1, 20d
     ```
   - **时序图**：
     ```mermaid
     sequenceDiagram
       Alice->>Bob: 你好 Bob，你好吗？
       Bob-->>Alice: 我很好，谢谢！
     ```

#### 4. **测试和调整图表**
   - **渲染**：Microsoft Loop 可能会自动渲染图表。检查显示效果，确保图表符合预期。
   - **调整**：如果需要，可以修改语法来调整图表的外观或修正错误。

#### 5. **添加学习参考链接**
   - 要添加视频教程或其他参考资料的链接，直接将链接粘贴到 Loop 文档中。例如，您可以粘贴 [如何在 Microsoft Loop 中创建流程图（YouTube 视频）](https://www.youtube.com/watch?v=XZ5p_24uDvo)，让团队成员可以轻松访问。

---

通过这些步骤，您可以在 Microsoft Loop 中使用 Mermaid 创建图表，以增强文档效果、简化复杂信息并促进团队间的协作。
