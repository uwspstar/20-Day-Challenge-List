# C4 Model 学习计划（7天）

https://simonbrown.je/

**C**ontext、**C**ontainer、**C**omponent、**C**ode

---
#### C4 模型的逐步分解和可视化让不同角色的人都能在各自的理解层次上与其他团队成员进行有效沟通：

- **架构师**可以用 `Context` 图和 `Container` 图与非技术人员解释系统的大致功能和外部依赖。
- **开发者**则可以通过 `Component` 图和 `Code` 图深入理解系统的实现，具体执行开发任务。

通过使用同一个模型，团队成员可以在不同抽象层次上保持一致的理解，减少了沟通成本和误解。C4 模型特别强调**“用图进行沟通”**，这一点使其成为简化复杂系统的一种强大工具。

---

#### 第一天: 软件架构简介与重要性
- **学习内容**:
  - 软件架构的定义与目的。
  - 软件架构在开发中的重要性。
  - 架构师在开发团队中的角色和责任。
- **目标**:
  - 理解为什么软件架构对于大型系统的成功至关重要。
  - 掌握架构师如何通过设计高效、可扩展的系统来帮助团队。
- **建议资源**:
  - [学习不同的架构风格（例如微服务、单体架构）并进行比较。](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/C4%20Model/%E5%AD%A6%E4%B9%A0%E4%B8%8D%E5%90%8C%E7%9A%84%E6%9E%B6%E6%9E%84%E9%A3%8E%E6%A0%BC%E5%B9%B6%E8%BF%9B%E8%A1%8C%E6%AF%94%E8%BE%83.md)
  
#### 第二天: C4 模型概述与优势
- **学习内容**:
  - [C4 模型的核心概念（Context、Container、Component、Code）。](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/C4%20Model/C4%20%E6%A8%A1%E5%9E%8B%E7%9A%84%E6%A0%B8%E5%BF%83%E6%A6%82%E5%BF%B5.md)
  - [为什么 C4 模型能够简化复杂系统的理解。](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/C4%20Model/%E4%B8%BA%E4%BB%80%E4%B9%88%20C4%20%E6%A8%A1%E5%9E%8B%E8%83%BD%E5%A4%9F%E7%AE%80%E5%8C%96%E5%A4%8D%E6%9D%82%E7%B3%BB%E7%BB%9F%E7%9A%84%E7%90%86%E8%A7%A3.md)
  - [C4 模型与其他架构模型的比较。](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/C4%20Model/C4%20%E6%A8%A1%E5%9E%8B%E4%B8%8E%E5%85%B6%E4%BB%96%E6%9E%B6%E6%9E%84%E6%A8%A1%E5%9E%8B%E7%9A%84%E6%AF%94%E8%BE%83.md)
- **目标**:
  - 掌握 C4 模型的关键概念及其在系统设计中的优势。
  - 理解使用 C4 模型的好处，如可视化和沟通效率。
- **建议资源**:
  - 阅读 C4 模型的官方文档，探索其与传统 UML 图的对比。
  
#### 第三天: Context 图 - 系统上下文的可视化
- **学习内容**:
  - [学习如何创建 Context 图。](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/C4%20Model/%E5%AD%A6%E4%B9%A0%E5%A6%82%E4%BD%95%E5%88%9B%E5%BB%BA%20Context%20%E5%9B%BE.md)
  - [使用 Context 图表示系统与外部实体的交互。](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/C4%20Model/%E4%BD%BF%E7%94%A8%20Context%20%E5%9B%BE%E8%A1%A8%E7%A4%BA%E7%B3%BB%E7%BB%9F%E4%B8%8E%E5%A4%96%E9%83%A8%E5%AE%9E%E4%BD%93%E7%9A%84%E4%BA%A4%E4%BA%92.md)
  - [Context 图的最佳实践，如清晰的边界和角色定义。](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/C4%20Model/Context%20%E5%9B%BE%E7%9A%84%E6%9C%80%E4%BD%B3%E5%AE%9E%E8%B7%B5.md)
- **目标**:
  - 掌握如何使用 Context 图清晰展示系统的外部关系。
  - 理解在不同场景下 Context 图的应用。
- **实践**:
  - [绘制一个常见应用的 Context 图。](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/C4%20Model/%E7%BB%98%E5%88%B6%E4%B8%80%E4%B8%AA%E5%B8%B8%E8%A7%81%E5%BA%94%E7%94%A8%E7%9A%84%20Context%20%E5%9B%BE.md)
  
#### 第四天: Container 图 - 容器和关系的识别
- **学习内容**:
  - [学习如何创建 Container 图，展示系统中的容器及其交互关系。](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/C4%20Model/%E5%AD%A6%E4%B9%A0%E5%A6%82%E4%BD%95%E5%88%9B%E5%BB%BA%20Container%20%E5%9B%BE.md)
  - [理解容器与组件之间的区别，识别每个容器的职责。](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/C4%20Model/%E7%90%86%E8%A7%A3%E5%AE%B9%E5%99%A8%E4%B8%8E%E7%BB%84%E4%BB%B6%E4%B9%8B%E9%97%B4%E7%9A%84%E5%8C%BA%E5%88%AB.md)
  - [Container 图的最佳实践，强调模块化和清晰的边界。](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/C4%20Model/Container%20%E5%9B%BE%E7%9A%84%E6%9C%80%E4%BD%B3%E5%AE%9E%E8%B7%B5.md)
- **目标**:
  - 通过 Container 图准确表示系统的主要构件及其交互。
  - 理解容器在系统扩展性和维护性中的重要性。
- **实践**:
  - [绘制一个项目的 Container 图，展示各个服务及其交互。](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/C4%20Model/%E7%BB%98%E5%88%B6%E9%A1%B9%E7%9B%AE%E7%9A%84%20Container%20%E5%9B%BE.md)
  
#### 第五天: Component 图 - 容器的分解
- **学习内容**:
  - [学习如何分解容器并创建 Component 图，深入展示容器的内部组件。](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/C4%20Model/%E5%AD%A6%E4%B9%A0%E5%A6%82%E4%BD%95%E5%88%86%E8%A7%A3%E5%AE%B9%E5%99%A8%E5%B9%B6%E5%88%9B%E5%BB%BA%20Component%20%E5%9B%BE.md)
  - [理解容器分解的重要性，尤其是在系统复杂性增加时。](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/C4%20Model/%E7%90%86%E8%A7%A3%E5%AE%B9%E5%99%A8%E5%88%86%E8%A7%A3%E7%9A%84%E9%87%8D%E8%A6%81%E6%80%A7.md)
- **目标**:
  - 掌握如何使用 Component 图展示容器内部的具体实现。
  - 理解组件之间的依赖关系及其影响。
- **实践**:
  - [为一个具体的容器创建 Component 图，展示其主要组件。](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/C4%20Model/%E4%B8%BA%E4%B8%80%E4%B8%AA%E5%85%B7%E4%BD%93%E7%9A%84%E5%AE%B9%E5%99%A8%E5%88%9B%E5%BB%BA%20Component%20%E5%9B%BE.md)
  
#### 第六天: 动态图与架构决策文档
- **学习内容**:
  - [动态图：展示系统运行时的行为。](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/C4%20Model/%E5%8A%A8%E6%80%81%E5%9B%BE%EF%BC%9A%E5%B1%95%E7%A4%BA%E7%B3%BB%E7%BB%9F%E8%BF%90%E8%A1%8C%E6%97%B6%E7%9A%84%E8%A1%8C%E4%B8%BA.md)
  - [学习如何在动态图中捕获系统的动态交互。](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/C4%20Model/%E5%A6%82%E4%BD%95%E5%9C%A8%E5%8A%A8%E6%80%81%E5%9B%BE%E4%B8%AD%E6%8D%95%E8%8E%B7%E7%B3%BB%E7%BB%9F%E7%9A%84%E5%8A%A8%E6%80%81%E4%BA%A4%E4%BA%92.md)
  - [架构决策文档：如何记录关键的架构决策。](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/C4%20Model/%E5%A6%82%E4%BD%95%E8%AE%B0%E5%BD%95%E5%85%B3%E9%94%AE%E7%9A%84%E6%9E%B6%E6%9E%84%E5%86%B3%E7%AD%96.md)
  - [使用架构决策模板和最佳实践。](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/C4%20Model/%E4%BD%BF%E7%94%A8%E6%9E%B6%E6%9E%84%E5%86%B3%E7%AD%96%E6%A8%A1%E6%9D%BF%E5%92%8C%E6%9C%80%E4%BD%B3%E5%AE%9E%E8%B7%B5.md)
- **目标**:
  - 掌握如何通过动态图展示系统的运行时行为。
  - 理解记录架构决策对项目长期成功的重要性。
- **实践**:
  - [为一个交互复杂的系统绘制动态图，展示其运行时的操作。](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/C4%20Model/%E5%8A%A8%E6%80%81%E5%9B%BE%EF%BC%9A%E5%B1%95%E7%A4%BA%E4%BA%A4%E4%BA%92%E5%A4%8D%E6%9D%82%E7%B3%BB%E7%BB%9F%E7%9A%84%E8%BF%90%E8%A1%8C%E6%97%B6%E6%93%8D%E4%BD%9C.md)
  
#### 第七天: [C4 模型的集成与协作](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/C4%20Model/%E5%A6%82%E4%BD%95%E5%B0%86%20C4%20%E6%A8%A1%E5%9E%8B%E9%9B%86%E6%88%90%E5%88%B0%E5%BC%80%E5%8F%91%E6%B5%81%E7%A8%8B%E4%B8%AD.md)
- **学习内容**:
  - 如何将 C4 模型集成到开发流程中。
  - C4 模型在文档和团队协作中的作用。
  - [如何选择合适的 C4 建模工具 如 Structurizr、PlantUML。](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/C4%20Model/%E5%A6%82%E4%BD%95%E9%80%89%E6%8B%A9%E5%90%88%E9%80%82%E7%9A%84%20C4%20%E5%BB%BA%E6%A8%A1%E5%B7%A5%E5%85%B7.md)
  - [团队协作中的架构决策：如何在团队中达成共识。](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/C4%20Model/%E5%9B%A2%E9%98%9F%E5%8D%8F%E4%BD%9C%E4%B8%AD%E7%9A%84%E6%9E%B6%E6%9E%84%E5%86%B3%E7%AD%96%EF%BC%9A%E5%A6%82%E4%BD%95%E5%9C%A8%E5%9B%A2%E9%98%9F%E4%B8%AD%E8%BE%BE%E6%88%90%E5%85%B1%E8%AF%86.md)
- **目标**:
  - 掌握如何在实际项目中使用 C4 模型，提升团队协作效率。
  - 理解不同工具的优势，并选择合适的工具进行建模。
- **实践**:
  - 使用工具为一个项目绘制 C4 图，并与团队成员分享进行反馈。

#### 总结：
通过7天的学习，你将掌握如何使用 C4 模型来构建、分析和展示复杂系统的架构，并通过 Context、Container、Component 和动态图为项目提供更高效的架构文档和沟通方式。

