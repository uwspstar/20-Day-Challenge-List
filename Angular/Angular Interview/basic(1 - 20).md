### List of Questions Based on the Provided Content

1. **What is Angular?**
2. **What is Single Page Application?**
3. **What is Angular CLI?**
4. **How to set up Angular CLI?**
5. **How to create the first Angular App?**
6. **What is the Angular File Structure (Part I)?**
7. **What is the Angular File Structure (Part II)?**
8. **What is the Angular File Structure (Part III)?**
9. **What is Angular Component?**
10. **How does Angular load components inside the browser?**
11. **What are Templates & Styles component properties?**
12. **What is a better approach for Templates & Styles?**
13. **How to generate Angular Components using Angular CLI?**
14. **What is NgOnInit() Lifecycle Hook?**
15. **What is Data Binding?**
16. **How to share data between components?**
17. **What is Parent-Child relationship in Angular?**
18. **What is @Input Decorator?**
19. **What is @ViewChild Decorator?**
20. **What is @Output & Event Emitter?**
21. **What is String Interpolation?**
22. **What is Property Binding?**
23. **What is Class Binding?**
24. **What is Style Binding?**
25. **What is Event Binding?**
26. **What is Event Filtering?**
27. **What is Template Variable?**
28. **What is Two-Way Data Binding?**
29. **What is the difference between One-Way and Two-Way Data Binding?**
30. **What is Angular Directive?**
31. **What is NgFor Directive?**
32. **How to Fetch Object Array using NgFor?**
33. **What is Angular Change Detection?**
34. **How to use Array Index in Angular?**
35. **What is NgIf Directive?**
36. **What is NgTemplate Directive?**
37. **What is NgSwitchCase Directive?**
38. **What is NgStyle Directive?**
39. **What is NgClass Directive?**
40. **What is the difference between Structural Directive and Attribute Directives?**
41. **What are Angular Pipes & types of Pipes?**
42. **What is Uppercase Lowercase Pipes?**
43. **What is Number Pipes?**
44. **What is Currency Pipes?**
45. **What is Date Pipes?**
46. **What is JSON Pipe?**
47. **What is Percent Pipe?**
48. **What is Slice Pipe?**
49. **What is Custom Pipe?**
50. **How to create a Custom Pipe using Angular CLI?**
51. **How to create Custom Pipes with Arguments?**
52. **What is Angular Service?**
53. **How to create Angular Service manually?**
54. **What is Dependency Injection (DI)?**
55. **What are DI Providers and `@Injectable` Decorator?**
56. **How to generate Angular Service using Angular CLI?**
57. **How to use Angular Service?**
58. **What is Angular Interface?**
59. **What are Angular Form Types?**
60. **How to create Bootstrap Forms?**
61. **What is NgForm Directive?**
62. **What is the difference between NgForm and FormGroup Class?**
63. **What is NgModel and FormControl Class?**
64. **What is Form Validation?**
65. **How to style Invalid Inputs?**
66. **What are the types of Form Validation?**
67. **How to validate Email Input Field?**
68. **How to validate Text Area?**
69. **How to fix Validation Errors?**
70. **How to style all invalid input fields for Validation Errors?**
71. **What is Form Submission?**
72. **How to disable Submit Button?**
73. **What is Reactive Form Setup?**
74. **How to create Reactive Form Controls Programmatically?**
75. **What are Reactive Form Basic Validations?**
76. **How to add multiple validations in Reactive Forms?**
77. **How to submit Reactive Forms and get form values?**
78. **What are Nested Form Groups?**
79. **What is Reactive Form Array?**
80. **What is Reactive Form Builder?**
81. **How to add custom validations in Reactive Forms?**
82. **What is Angular Router Outlet?**
83. **What is Angular Router Link?**
84. **What is Angular Base URL?**
85. **What is Angular Base Router?**
86. **What is the difference between Router and Href?**
87. **What is Angular RouterLinkActive?**
88. **What are Router Parameter Variables?**
89. **How to get Router Parameters?**
90. **What is an Observable?**
91. **What is Observable Subscribe?**
92. **What is Observable Next?**
93. **What is the difference between RXJS Observable and Functions?**
94. **What is the difference between Synchronous and Asynchronous Programming?**
95. **What is Observable Subscribe & Unsubscribe?**
96. **What are multiple Router Parameters?**
97. **What are Query Parameters?**
98. **What is a separate module for Angular Routing?**
99. **How to navigate programmatically in Angular?**
100. **What are Wild Card Routers?**

---


### [1. What is Angular?]() 
**English Explanation:**  
Angular is a platform and framework for building single-page client applications using HTML and TypeScript. It is maintained by Google and provides a way to build large-scale, efficient, and maintainable web applications. Angular uses a component-based architecture and is known for its dependency injection and powerful templating capabilities.  

**中文解释:**  
Angular 是一个用于使用 HTML 和 TypeScript 构建单页客户端应用程序的平台和框架。它由 Google 维护，为构建大规模、高效和可维护的 Web 应用程序提供了方法。Angular 使用基于组件的架构，并以其依赖注入和强大的模板功能而闻名。  

**Code Example:**  

```typescript
// Example of an Angular component
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `<h1>Welcome to Angular!</h1>`,
  styles: [`h1 { color: blue; }`]
})
export class AppComponent {
  title = 'Hello Angular';
}
```

**Explanation:**  
1. **Component:** This code defines an Angular component using the `@Component` decorator.  
2. **Selector:** `app-root` is used to define the HTML tag that Angular uses to insert the component.  
3. **Template:** Defines the HTML structure of the component.  
4. **Styles:** CSS styles that apply only to this component.  

**中文解释:**  
1. **组件:** 这段代码使用 `@Component` 装饰器定义了一个 Angular 组件。  
2. **选择器 (Selector):** `app-root` 用于定义 Angular 插入组件时使用的 HTML 标签。  
3. **模板 (Template):** 定义了组件的 HTML 结构。  
4. **样式 (Styles):** 仅适用于该组件的 CSS 样式。  

**Tip:**  
- When creating a new Angular component, always ensure you define a unique selector and include meaningful HTML content.  
- **中文提示:** 创建新的 Angular 组件时，务必定义一个唯一的选择器，并包含有意义的 HTML 内容。  

**Warning:**  
- Avoid creating multiple components with the same selector as this can cause unexpected behavior and rendering issues.  
- **中文警告:** 避免创建具有相同选择器的多个组件，因为这可能会导致意外行为和渲染问题。  

**5 Interview Questions & Answers:**

1. **Q:** What are the key benefits of using Angular over other frameworks?  
   **A:** The key benefits include a strong component-based architecture, built-in support for dependency injection, a powerful CLI, and support for two-way data binding.  
   
   **中文问答:**  
   **问:** 使用 Angular 相较于其他框架的主要优势是什么？  
   **答:** 主要优势包括强大的基于组件的架构、内置依赖注入支持、强大的 CLI 工具以及支持双向数据绑定。

2. **Q:** How does Angular support dependency injection?  
   **A:** Angular uses a hierarchical dependency injection system, where services are defined and injected into components or other services via constructors, ensuring loose coupling and ease of testing.  
   
   **中文问答:**  
   **问:** Angular 如何支持依赖注入？  
   **答:** Angular 使用分层依赖注入系统，服务可以通过构造函数定义并注入到组件或其他服务中，从而确保松散耦合和便于测试。

3. **Q:** What are the main components of Angular’s architecture?  
   **A:** Angular's architecture consists of modules, components, templates, metadata, data binding, services, and dependency injection. Each component works together to create a cohesive application.  
   
   **中文问答:**  
   **问:** Angular 架构的主要组成部分是什么？  
   **答:** Angular 的架构由模块、组件、模板、元数据、数据绑定、服务和依赖注入组成。每个组件协同工作以创建一个完整的应用程序。

4. **Q:** Can you explain the concept of two-way data binding in Angular?  
   **A:** Two-way data binding in Angular allows synchronization between the view and the model, meaning changes in the UI update the model and changes in the model update the UI automatically using `[(ngModel)]`.  
   
   **中文问答:**  
   **问:** 能解释一下 Angular 中的双向数据绑定的概念吗？  
   **答:** Angular 中的双向数据绑定允许视图和模型之间的同步，即 UI 中的更改会自动更新模型，而模型中的更改也会自动更新 UI。这可以通过 `[(ngModel)]` 实现。

5. **Q:** How does Angular handle error management and logging?  
   **A:** Angular provides a global `ErrorHandler` class that can be extended to customize error handling. It also supports logging via Angular services or external libraries like `ngx-logger`.  

   **中文问答:**  
   **问:** Angular 如何处理错误管理和日志记录？  
   **答:** Angular 提供了一个全局的 `ErrorHandler` 类，可以通过扩展它来自定义错误处理。它还支持通过 Angular 服务或类似 `ngx-logger` 的外部库进行日志记录。

---

### [2. What is Single Page Application (SPA)?]()
**English:**  
A Single Page Application (SPA) is a web application that loads a single HTML page and dynamically updates the content as the user interacts with the app. SPAs use AJAX and JavaScript frameworks such as Angular to retrieve data and update the view without reloading the page, resulting in faster and more fluid user experiences.

**中文:**  
单页应用程序（SPA）是一种加载单个 HTML 页面并在用户与应用程序交互时动态更新内容的 Web 应用程序。SPA 使用 AJAX 和诸如 Angular 之类的 JavaScript 框架来检索数据并更新视图，而无需重新加载页面，从而提供更快、更流畅的用户体验。

**Code Example:**

```typescript
// Example of routing in a Single Page Application using Angular
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';
import { HomeComponent } from './home/home.component';
import { AboutComponent } from './about/about.component';

const routes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'about', component: AboutComponent }
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule {}
```

**Explanation:**
1. **Routes:** Define paths and corresponding components to dynamically load based on the URL.
2. **RouterModule:** Manages navigation between different views without reloading the page.
3. **RouterModule.forRoot:** Configures the root level routing for the application.

**中文解释:**
1. **路径定义 (Routes):** 定义路径和对应的组件，根据 URL 动态加载内容。
2. **路由模块 (RouterModule):** 管理视图之间的导航，而无需重新加载页面。
3. **RouterModule.forRoot:** 配置应用程序的根级路由。

**Tip:**
- Use Angular routing for navigation between different views to avoid full-page reloads and enhance the SPA experience.
- **中文提示:** 使用 Angular 路由在不同视图之间导航，以避免页面完全重新加载，并增强单页应用程序的体验。

**Warning:**
- Ensure all paths in your routing module are correctly defined and avoid circular navigation as it may lead to navigation errors.
- **中文警告:** 确保路由模块中的所有路径均已正确定义，避免循环导航，否则可能导致导航错误。

**5 Interview Questions & Answers:**

1. **Q:** What are the main benefits of using a Single Page Application?  
   **A:** SPAs offer faster performance due to reduced server requests, provide smoother navigation, and allow for a more interactive user experience.  
   
   **中文问答:**  
   **问:** 使用单页应用程序的主要好处是什么？  
   **答:** SPA 由于减少了服务器请求，因此提供了更快的性能，带来了更流畅的导航，并提供了更具互动性的用户体验。

2. **Q:** How does Angular handle routing in an SPA?  
   **A:** Angular uses the `RouterModule` and `Routes` array to define navigation between components. It dynamically loads components based on the URL, allowing for seamless transitions without full-page reloads.  
   
   **中文问答:**  
   **问:** Angular 如何在单页应用程序中处理路由？  
   **答:** Angular 使用 `RouterModule` 和 `Routes` 数组定义组件之间的导航。它根据 URL 动态加载组件，实现无页面刷新过渡。

3. **Q:** What are some challenges when developing an SPA?  
   **A:** Challenges include managing client-side state, ensuring good SEO support, and handling authentication and authorization properly in a single-page context.  
   
   **中文问答:**  
   **问:** 开发单页应用程序时存在哪些挑战？  
   **答:** 挑战包括管理客户端状态、确保良好的 SEO 支持，以及在单页上下文中正确处理身份验证和授权。

4. **Q:** How can SPAs improve SEO performance?  
   **A:** SPAs can use server-side rendering (SSR) with Angular Universal to pre-render content on the server before sending it to the client, improving SEO and initial load performance.  
   
   **中文问答:**  
   **问:** 单页应用程序如何提高 SEO 性能？  
   **答:** SPA 可以使用 Angular Universal 进行服务端渲染（SSR），在将内容发送到客户端之前在服务器上预渲染内容，从而提高 SEO 和初始加载性能。

5. **Q:** What is lazy loading in Angular, and how does it benefit an SPA?  
   **A:** Lazy loading in Angular allows for loading specific modules only when they are needed, reducing the initial load time and improving performance in SPAs.  
   
   **中文问答:**  
   **问:** Angular 中的懒加载是什么？它如何提升单页应用程序的性能？  
   **答:** Angular 中的懒加载允许仅在需要时加载特定模块，从而减少初始加载时间并提升单页应用程序的性能。

---

### 3. What is Angular CLI?
**English:**  
Angular CLI (Command Line Interface) is a command-line tool that helps automate common tasks when building Angular applications, such as creating components, services, and modules. It also simplifies the process of building, testing, and deploying applications.

**中文:**  
Angular CLI（命令行工具）是一个用于在构建 Angular 应用程序时自动化常见任务的命令行工具，例如创建组件、服务和模块。它还简化了应用程序的构建、测试和部署过程。

**Code Example:**

```bash
# Create a new Angular project
ng new my-app

# Generate a new component
ng generate component my-component

# Serve the application
ng serve
```

**Explanation:**
1. **`ng new my-app`:** Creates a new Angular project with the name `my-app`.
2. **`ng generate component my-component`:** Generates a new component named `my-component`.
3. **`ng serve`:** Serves the application on a local development server.

**中文解释:**
1. **`ng new my-app`:** 创建一个名为 `my-app` 的新 Angular 项目。
2. **`ng generate component my-component`:** 生成一个名为 `my-component` 的新组件。
3. **`ng serve`:** 在本地开发服务器上启动应用程序。

**Tip:**
- Use the Angular CLI to quickly scaffold new projects and generate new components or services to maintain consistency.
- **中文提示:** 使用 Angular CLI 快速创建新项目和生成新组件或服务，以保持一致性。

**Warning:**
- Always check the Angular CLI version compatibility with your project to avoid conflicts.
- **中文警告:** 始终检查 Angular CLI 版本与项目的兼容性，以避免冲突。

**5 Interview Questions & Answers:**

1. **Q:** What are the benefits of using Angular CLI for development?  
   **A:** Angular CLI automates common development tasks, maintains consistent coding practices, and provides a unified build, serve, and test mechanism.  

   **中文问答:**  
   **问:** 使用 Angular CLI 进行开发有哪些好处？  
   **答:** Angular CLI 自动化了常见的开发任务，保持了一致的编码实践，并提供了统一的构建、启动和测试机制。

2. **Q:** How do you update an existing Angular project to the latest CLI version?  
   **A:** Use the command `ng update @angular/cli @angular/core` to update the Angular CLI and Core packages.  

   **中文问答:**  
   **问:** 如何将现有的 Angular 项目更新到最新的 CLI 版本？  
   **答:** 使用命令 `ng update @angular/cli @angular/core` 来更新 Angular CLI 和核心包。

3. **Q:** How can you create a service using Angular CLI?  
   **A:** Run the command `ng generate service service-name` to create a new service in the specified module.  

   **中文问答:**  
   **问:** 如何使用 Angular CLI 创建服务？  
   **答:** 运行命令 `ng generate service service-name` 在指定模块中创建新服务。

4. **Q:** How does Angular CLI handle building applications for production?  
   **A:** The `ng build --prod` command optimizes the build for production by minifying files, removing unnecessary code, and improving performance.  

   **中文问答:**  
   **问:** Angular CLI 如何为生产环境构建应用程序？  
   **答:** `ng build --prod` 命令通过压缩文件、移除不必要的代码和提升性能来优化生产环境的构建。

5. **Q:** What are some useful Angular CLI commands for development?  
   **A:** Some useful commands are `ng serve` (to serve the app), `ng test` (to run tests), `ng build` (to build the app), and `ng generate` (to generate new files).  

   **中文问答:**  
   **问:** 开发中常用的 Angular CLI 命令有哪些？  
   **答:** 常用的命令有 `ng serve`（启动应用程序）、`ng test`（运行测试）、`ng build`（构建应用程序）和 `ng generate`（生成新文件）。

---

### [4. What is Angular Component?]()  
**English:**  
An Angular component is the basic building block of an Angular application. It controls a portion of the view and defines the structure, behavior, and presentation logic using HTML, CSS, and TypeScript. A component is defined using the `@Component` decorator and consists of three main parts: the template, styles, and the component class itself.

**中文:**  
Angular 组件是 Angular 应用程序的基本构建块。它控制视图的一部分，并使用 HTML、CSS 和 TypeScript 定义结构、行为和展示逻辑。组件通过 `@Component` 装饰器定义，主要由三个部分组成：模板（template）、样式（styles）和组件类（component class）。

**Code Example:**

```typescript
// Simple Angular Component
import { Component } from '@angular/core';

@Component({
  selector: 'app-header',
  template: `<h1>{{ title }}</h1>`,
  styles: ['h1 { font-weight: bold; }']
})
export class HeaderComponent {
  title = 'Welcome to Angular Components';
}
```

**Explanation:**
1. **Selector:** `app-header` defines the HTML tag used in the template to render this component.
2. **Template:** Displays the value of the `title` variable.
3. **Styles:** Defines CSS specific to this component.
4. **Component Class:** Holds the logic and data for the component.

**中文解释:**
1. **选择器 (Selector):** `app-header` 定义了在模板中用于渲染该组件的 HTML 标签。
2. **模板 (Template):** 显示 `title` 变量的值。
3. **样式 (Styles):** 定义仅适用于该组件的 CSS。
4. **组件类 (Component Class):** 保存组件的逻辑和数据。

**Tip:**
- Always use meaningful selectors that represent the component's functionality, such as `app-header` for a header component.
- **中文提示:** 始终使用有意义的选择器来表示组件的功能，如用于头部组件的 `app-header`。

**Warning:**
- Avoid using the same selector name in multiple components as this will cause conflicts in rendering and functionality.
- **中文警告:** 避免在多个组件中使用相同的选择器名称，因为这会导致渲染和功能冲突。

**5 Interview Questions & Answers:**

1. **Q:** What are the main parts of an Angular component?  
   **A:** An Angular component consists of a selector, template, styles, and a component class that contains the logic and data binding.

   **中文问答:**  
   **问:** Angular 组件的主要部分是什么？  
   **答:** Angular 组件由选择器、模板、样式和包含逻辑及数据绑定的组件类组成。

2. **Q:** How do you create a component in Angular using the CLI?  
   **A:** Use the command `ng generate component component-name` or `ng g c component-name` to create a new component.  

   **中文问答:**  
   **问:** 如何使用 Angular CLI 创建组件？  
   **答:** 使用命令 `ng generate component component-name` 或 `ng g c component-name` 来创建新组件。

3. **Q:** How does Angular identify a component to be rendered?  
   **A:** Angular identifies a component to be rendered using its selector, which matches the custom HTML tag defined in the component.  

   **中文问答:**  
   **问:** Angular 如何识别需要渲染的组件？  
   **答:** Angular 使用组件的选择器来识别需要渲染的组件，该选择器与组件中定义的自定义 HTML 标签相匹配。

4. **Q:** How can you pass data to a component in Angular?  
   **A:** Data can be passed to a component using input properties defined with the `@Input` decorator.  

   **中文问答:**  
   **问:** 如何在 Angular 中向组件传递数据？  
   **答:** 可以使用 `@Input` 装饰器定义的输入属性向组件传递数据。

5. **Q:** What is the lifecycle of an Angular component?  
   **A:** The Angular component lifecycle includes hooks such as `ngOnInit`, `ngOnChanges`, `ngDoCheck`, `ngAfterViewInit`, `ngAfterContentInit`, and `ngOnDestroy`.  

   **中文问答:**  
   **问:** Angular 组件的生命周期是什么？  
   **答:** Angular 组件的生命周期包括 `ngOnInit`、`ngOnChanges`、`ngDoCheck`、`ngAfterViewInit`、`ngAfterContentInit` 和 `ngOnDestroy` 等钩子函数。

---

### 5. How does Angular load components inside the browser?
**English:**  
Angular loads components inside the browser using the Angular compiler and the DOM (Document Object Model). When the application is started (using `ng serve`), Angular compiles all the components and templates into a JavaScript format, which is then rendered into the DOM based on the defined component selector. Angular uses the `main.ts` file as the entry point and `AppModule` as the root module.

**中文:**  
Angular 使用 Angular 编译器和 DOM（文档对象模型）在浏览器中加载组件。启动应用程序时（使用 `ng serve`），Angular 会将所有组件和模板编译为 JavaScript 格式，并基于定义的组件选择器将其渲染到 DOM 中。Angular 使用 `main.ts` 文件作为入口点，并将 `AppModule` 作为根模块。

**Code Example:**

```typescript
// main.ts file - Angular entry point
import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';
import { AppModule } from './app/app.module';

platformBrowserDynamic().bootstrapModule(AppModule)
  .catch(err => console.error(err));
```

**Explanation:**
1. **`platformBrowserDynamic()`:** Initializes the Angular app in the browser.
2. **`bootstrapModule(AppModule)`:** Bootstraps the `AppModule` as the root module.

**中文解释:**
1. **`platformBrowserDynamic()`:** 在浏览器中初始化 Angular 应用程序。
2. **`bootstrapModule(AppModule)`:** 引导 `AppModule` 作为根模块。

**Tip:**
- Use the `ng serve` command to serve your Angular application in the development environment.
- **中文提示:** 使用 `ng serve` 命令在开发环境中启动 Angular 应用程序。

**Warning:**
- Ensure that the root module is correctly configured in `main.ts` to avoid bootstrap errors.
- **中文警告:** 确保在 `main.ts` 中正确配置了根模块，以避免引导错误。

**5 Interview Questions & Answers:**

1. **Q:** How does Angular bootstrap an application?  
   **A:** Angular bootstraps an application by first compiling the `AppModule` and rendering its components based on the selectors defined in the templates.  

   **中文问答:**  
   **问:** Angular 如何引导应用程序？  
   **答:** Angular 首先编译 `AppModule`，并根据模板中定义的选择器渲染其组件来引导应用程序。

2. **Q:** What is the purpose of the `main.ts` file in an Angular application?  
   **A:** The `main.ts` file is the entry point of the application and is responsible for bootstrapping the root module.  

   **中文问答:**  
   **问:** `main.ts` 文件在 Angular 应用程序中的作用是什么？  
   **答:** `main.ts` 文件是应用程序的入口点，负责引导根模块。

3. **Q:** How does Angular handle change detection?  
   **A:** Angular uses a change detection mechanism to check for changes in the state of components and update the DOM accordingly.  

   **中文问答:**  
   **问:** Angular 如何处理变更检测？  
   **答:** Angular 使用变更检测机制来检查组件状态的变化，并相应地更新 DOM。

4. **Q:** What is the role of the `AppModule` in an Angular application?  
   **A:** The `AppModule` is the root module that initializes the application and imports other feature modules.  

   **中文问答:**  
   **问:** `AppModule` 在 Angular 应用程序中的作用是什么？  
   **答:** `AppModule` 是根模块，用于初始化应用程序并导入其他功能模块。

5. **Q:** What are some common errors during component bootstrapping, and how can they be resolved?  
   **A:** Common errors include missing module imports, incorrect component selectors, and undefined dependencies. These can be resolved by checking module declarations and imports.  

   **中文问答:**  
   **问:** 组件引导过程中常见的错误有哪些？如何解决？  
   **答:** 常见错误包括模块导入缺失、组件选择器错误以及未定义的依赖关系。可以通过检查模块声明和导入来解决这些问题。

---
### 6. What are Templates & Styles Component Properties?
**English:**  
Templates and Styles are two important properties of an Angular component. The **template** property defines the HTML structure of the component, while the **styles** property defines the CSS rules that apply specifically to that component. The template property can be defined using either the `templateUrl` (for external HTML files) or `template` (for inline HTML content). Similarly, the styles property can be defined using `styleUrls` (for external CSS files) or `styles` (for inline CSS rules).

**中文:**  
模板（Templates）和样式（Styles）是 Angular 组件的两个重要属性。**模板** 属性定义了组件的 HTML 结构，而 **样式** 属性定义了仅适用于该组件的 CSS 规则。模板属性可以通过 `templateUrl`（外部 HTML 文件）或 `template`（内联 HTML 内容）来定义。同样，样式属性可以通过 `styleUrls`（外部 CSS 文件）或 `styles`（内联 CSS 规则）来定义。

**Code Example:**

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-card',
  templateUrl: './card.component.html',
  styleUrls: ['./card.component.css']
})
export class CardComponent {
  // Component logic here
}
```

**Explanation:**
1. **templateUrl:** Points to an external HTML file (`card.component.html`) that defines the component's structure.
2. **styleUrls:** Points to an external CSS file (`card.component.css`) that defines the component's styles.

**中文解释:**
1. **templateUrl:** 指向外部 HTML 文件（`card.component.html`），定义组件的结构。
2. **styleUrls:** 指向外部 CSS 文件（`card.component.css`），定义组件的样式。

**Tip:**
- Use `templateUrl` and `styleUrls` for larger components to keep the code clean and maintainable.
- **中文提示:** 对于较大的组件，使用 `templateUrl` 和 `styleUrls` 以保持代码清晰和易于维护。

**Warning:**
- Avoid using too much logic in templates as it can make the HTML cluttered and hard to maintain.
- **中文警告:** 避免在模板中使用过多逻辑，因为这会导致 HTML 混乱且难以维护。

**5 Interview Questions & Answers:**

1. **Q:** What are the different ways to define a template in Angular?  
   **A:** Templates can be defined using either `templateUrl` (external HTML file) or `template` (inline HTML content).

   **中文问答:**  
   **问:** 在 Angular 中定义模板的不同方式是什么？  
   **答:** 模板可以通过 `templateUrl`（外部 HTML 文件）或 `template`（内联 HTML 内容）来定义。

2. **Q:** What is the difference between `styleUrls` and `styles` in Angular?  
   **A:** `styleUrls` is used to link to an external CSS file, while `styles` is used to define inline CSS rules.

   **中文问答:**  
   **问:** Angular 中 `styleUrls` 和 `styles` 的区别是什么？  
   **答:** `styleUrls` 用于链接到外部 CSS 文件，而 `styles` 用于定义内联 CSS 规则。

3. **Q:** How can you use multiple CSS files in an Angular component?  
   **A:** You can specify multiple CSS files in the `styleUrls` array like this: `styleUrls: ['./styles1.css', './styles2.css']`.

   **中文问答:**  
   **问:** 如何在 Angular 组件中使用多个 CSS 文件？  
   **答:** 可以在 `styleUrls` 数组中指定多个 CSS 文件，例如：`styleUrls: ['./styles1.css', './styles2.css']`。

4. **Q:** What is the purpose of the `encapsulation` property in Angular components?  
   **A:** The `encapsulation` property controls how styles are applied to the component. It can be `Emulated` (default), `None`, or `ShadowDom`.

   **中文问答:**  
   **问:** Angular 组件中 `encapsulation` 属性的作用是什么？  
   **答:** `encapsulation` 属性控制样式如何应用于组件。它可以是 `Emulated`（默认）、`None` 或 `ShadowDom`。

5. **Q:** How does Angular handle style isolation for components?  
   **A:** Angular uses view encapsulation to isolate styles within components, ensuring that styles do not leak outside of their components.

   **中文问答:**  
   **问:** Angular 如何处理组件样式隔离？  
   **答:** Angular 使用视图封装（view encapsulation）在组件内隔离样式，确保样式不会泄漏到组件外部。

---

### 7. What is NgOnInit Lifecycle Hook?  
**English:**  
`NgOnInit` is one of the most commonly used lifecycle hooks in Angular. It is called once after the component is instantiated and the input properties are set. This hook is ideal for initializing the component's data or performing actions such as fetching data from a server.

**中文:**  
`NgOnInit` 是 Angular 中最常用的生命周期钩子之一。它在组件实例化并设置输入属性后被调用一次。该钩子非常适合用于初始化组件数据或执行从服务器获取数据等操作。

**Code Example:**

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-data',
  template: `<h2>{{ data }}</h2>`
})
export class DataComponent implements OnInit {
  data: string;

  constructor() {
    this.data = 'Loading...';
  }

  ngOnInit(): void {
    // Simulating fetching data
    setTimeout(() => {
      this.data = 'Data Loaded!';
    }, 2000);
  }
}
```

**Explanation:**
1. **ngOnInit:** Initializes the `data` property after the component is created.
2. **setTimeout:** Simulates data fetching and updates the `data` property after 2 seconds.

**中文解释:**
1. **ngOnInit:** 在组件创建后初始化 `data` 属性。
2. **setTimeout:** 模拟数据获取，并在 2 秒后更新 `data` 属性。

**Tip:**
- Use `ngOnInit` for data initialization tasks that should happen once during component creation.
- **中文提示:** 使用 `ngOnInit` 进行组件创建期间需要执行一次的数据初始化任务。

**Warning:**
- Avoid putting heavy logic in `ngOnInit` as it can slow down the initial rendering of the component.
- **中文警告:** 避免在 `ngOnInit` 中放置复杂逻辑，因为这会减慢组件的初始渲染速度。

**5 Interview Questions & Answers:**

1. **Q:** What is the purpose of `ngOnInit` in Angular?  
   **A:** `ngOnInit` is used to perform initialization tasks that should occur once after the component's properties are set.

   **中文问答:**  
   **问:** `ngOnInit` 在 Angular 中的作用是什么？  
   **答:** `ngOnInit` 用于执行在组件属性设置后需要执行一次的初始化任务。

2. **Q:** What is the difference between a constructor and `ngOnInit`?  
   **A:** The constructor is called when the component is instantiated, while `ngOnInit` is called after the component's input properties are set.

   **中文问答:**  
   **问:** 构造函数和 `ngOnInit` 有什么区别？  
   **答:** 构造函数在组件实例化时调用，而 `ngOnInit` 在组件的输入属性设置后调用。

3. **Q:** How would you implement `ngOnInit` to fetch data from a server?  
   **A:** Implement `ngOnInit` with a service call to fetch data and update the component's properties once the data is available.

   **中文问答:**  
   **问:** 如何在 `ngOnInit` 中实现从服务器获取数据？  
   **答:** 使用服务调用在 `ngOnInit` 中获取数据，并在数据可用时更新组件的属性。

4. **Q:** What is the order of lifecycle hooks in Angular?  
   **A:** The order is `ngOnChanges` → `ngOnInit` → `ngDoCheck` → `ngAfterContentInit` → `ngAfterContentChecked` → `ngAfterViewInit` → `ngAfterViewChecked` → `ngOnDestroy`.

   **中文问答:**  
   **问:** Angular 中生命周期钩子的调用顺序是什么？  
   **答:** 调用顺序是 `ngOnChanges` → `ngOnInit` → `ngDoCheck` → `ngAfterContentInit` → `ngAfterContentChecked` → `ngAfterViewInit` → `ngAfterViewChecked` → `ngOnDestroy`。

5. **Q:** Can you explain a scenario where `ngOnInit` would be preferable over the constructor?  
   **A:** `ngOnInit` is preferable for data initialization tasks because, at the time of its execution, input properties are already set, making it more suitable for using them.

   **中文问答:**  
   **问:** 在什么场景下 `ngOnInit` 比构造函数更合适？  
   **答:** `ngOn

Init` 更适合用于数据初始化任务，因为在其执行时输入属性已经设置完毕，更便于使用这些属性。

---
### 8. What is Data Binding?
**English:**  
Data Binding is a core feature in Angular that synchronizes the data between the model (business logic) and the view (HTML template). There are four types of data binding in Angular: **Interpolation**, **Property Binding**, **Event Binding**, and **Two-way Binding**. These types help efficiently handle user inputs, state changes, and UI updates, making Angular applications interactive and dynamic.

**中文:**  
数据绑定是 Angular 的核心功能之一，它在模型（业务逻辑）和视图（HTML 模板）之间同步数据。Angular 中有四种数据绑定类型：**插值（Interpolation）**、**属性绑定（Property Binding）**、**事件绑定（Event Binding）** 和 **双向绑定（Two-way Binding）**。这些类型帮助有效处理用户输入、状态变化和 UI 更新，使 Angular 应用程序更加交互和动态化。

**Code Example:**

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-data-binding',
  template: `
    <!-- Interpolation Binding -->
    <h1>{{ title }}</h1>

    <!-- Property Binding -->
    <input [value]="title" />

    <!-- Event Binding -->
    <button (click)="changeTitle()">Change Title</button>

    <!-- Two-way Data Binding -->
    <input [(ngModel)]="title" />
  `
})
export class DataBindingComponent {
  title = 'Data Binding Example';

  changeTitle() {
    this.title = 'Title Changed!';
  }
}
```

**Explanation:**
1. **Interpolation Binding:** `{{ title }}` is used to display the value of the `title` variable in the template.
2. **Property Binding:** `[value]="title"` binds the `title` variable to the `value` attribute of the `<input>` element.
3. **Event Binding:** `(click)="changeTitle()"` binds the button's click event to the `changeTitle` method, which changes the `title` value.
4. **Two-way Data Binding:** `[(ngModel)]="title"` binds the `title` variable to the `<input>` element and vice versa.

**中文解释:**
1. **插值绑定 (Interpolation Binding):** `{{ title }}` 用于在模板中显示 `title` 变量的值。
2. **属性绑定 (Property Binding):** `[value]="title"` 将 `title` 变量绑定到 `<input>` 元素的 `value` 属性。
3. **事件绑定 (Event Binding):** `(click)="changeTitle()"` 将按钮的点击事件绑定到 `changeTitle` 方法，该方法改变 `title` 的值。
4. **双向数据绑定 (Two-way Data Binding):** `[(ngModel)]="title"` 将 `title` 变量与 `<input>` 元素双向绑定，使它们之间可以相互更新。

**Tip:**
- Use two-way data binding (`[(ngModel)]`) for form inputs to capture and update data easily.
- **中文提示:** 对于表单输入使用双向数据绑定（`[(ngModel)]`），可以轻松捕获和更新数据。

**Warning:**
- Avoid overusing two-way binding in complex forms as it can lead to performance issues and difficult debugging.
- **中文警告:** 在复杂表单中避免过度使用双向绑定，因为这可能导致性能问题并难以调试。

**5 Interview Questions & Answers:**

1. **Q:** What are the different types of data binding in Angular?  
   **A:** The four types are Interpolation, Property Binding, Event Binding, and Two-way Data Binding.

   **中文问答:**  
   **问:** Angular 中的数据绑定类型有哪些？  
   **答:** 四种类型分别是：插值绑定、属性绑定、事件绑定和双向数据绑定。

2. **Q:** What is the difference between Property Binding and Interpolation?  
   **A:** Interpolation can only handle string values, while Property Binding can handle any data type and bind it to the DOM property.

   **中文问答:**  
   **问:** 属性绑定和插值绑定有什么区别？  
   **答:** 插值绑定只能处理字符串值，而属性绑定可以处理任何数据类型并将其绑定到 DOM 属性。

3. **Q:** How does Angular achieve two-way data binding?  
   **A:** Angular achieves two-way binding using `[(ngModel)]`, which combines property binding and event binding together.

   **中文问答:**  
   **问:** Angular 如何实现双向数据绑定？  
   **答:** Angular 通过 `[(ngModel)]` 实现双向绑定，该语法将属性绑定和事件绑定结合在一起。

4. **Q:** What is the main use case for Event Binding in Angular?  
   **A:** Event Binding is used to handle user interactions, such as button clicks, input changes, and form submissions.

   **中文问答:**  
   **问:** 在 Angular 中，事件绑定的主要用途是什么？  
   **答:** 事件绑定用于处理用户交互，例如按钮点击、输入更改和表单提交。

5. **Q:** What are the potential drawbacks of using too much two-way binding?  
   **A:** Overusing two-way binding can lead to performance issues, increased complexity, and harder-to-maintain code.

   **中文问答:**  
   **问:** 过度使用双向绑定的潜在缺点是什么？  
   **答:** 过度使用双向绑定可能导致性能问题、增加复杂性，并使代码难以维护。

---

### 9. How to Share Data Between Components?
**English:**  
In Angular, data can be shared between components using three main techniques: **Input/Output decorators**, **Shared Services**, and **State Management**. The `@Input` and `@Output` decorators are used for passing data between parent and child components, shared services can provide data across unrelated components, and state management solutions like NgRx can manage the application's state globally.

**中文:**  
在 Angular 中，可以使用三种主要技术在组件之间共享数据：**Input/Output 装饰器**、**共享服务** 和 **状态管理**。`@Input` 和 `@Output` 装饰器用于在父组件和子组件之间传递数据，共享服务可以在不相关的组件之间提供数据，而类似 NgRx 的状态管理解决方案可以全局管理应用程序的状态。

**Code Example:**

```typescript
// Parent Component: app-parent.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-parent',
  template: `
    <app-child [childMessage]="parentMessage" (messageEvent)="receiveMessage($event)"></app-child>
    <h2>Message from Child: {{ message }}</h2>
  `
})
export class ParentComponent {
  parentMessage = 'Message from Parent';
  message: string;

  receiveMessage($event: string) {
    this.message = $event;
  }
}

// Child Component: app-child.component.ts
import { Component, Input, Output, EventEmitter } from '@angular/core';

@Component({
  selector: 'app-child',
  template: `
    <h2>{{ childMessage }}</h2>
    <button (click)="sendMessage()">Send Message to Parent</button>
  `
})
export class ChildComponent {
  @Input() childMessage: string;
  @Output() messageEvent = new EventEmitter<string>();

  sendMessage() {
    this.messageEvent.emit('Message from Child');
  }
}
```

**Explanation:**
1. **Parent to Child Communication:** The `childMessage` is passed from the parent component to the child component using the `@Input` decorator.
2. **Child to Parent Communication:** The `messageEvent` is emitted from the child component and caught by the parent component using the `@Output` decorator and `EventEmitter`.

**中文解释:**
1. **父组件到子组件通信:** `childMessage` 通过 `@Input` 装饰器从父组件传递到子组件。
2. **子组件到父组件通信:** `messageEvent` 通过 `@Output` 装饰器和 `EventEmitter` 从子组件发射，并被父组件捕获。

**Tip:**
- Use shared services for complex data sharing between unrelated components to avoid unnecessary complexity in component interactions.
- **中文提示:** 对于不相关组件之间的复杂数据共享，使用共享服务以避免组件交互中的不必要复杂性。

**Warning:**
- Avoid using `@Input` and `@Output` for deeply nested components as it can lead to tightly coupled components and difficult debugging.
- **中文警告:** 避免在深层嵌套组件中使用 `@Input` 和 `@Output`，因为这可能导致组件之间的高度耦合和难以调试。

**5 Interview Questions & Answers:**

1. **Q:** How do you pass data from a parent component to a child component in Angular?  
   **A:** Use the `@Input` decorator in the child component to receive data from the parent component.

   **中文问答:**  
   **问:** 如何在 Angular 中从父组件向子组件传递数据？  
   **答:** 在子组件中使用 `@Input` 装饰器接收来自父组件的数据。

2. **Q:** How do you send data from a child component to a parent component?  
   **A:** Use the `@Output` decorator and an `EventEmitter` in the child component to emit data to the parent component.

   **中文问答:**  
   **问:** 如何从子组件

向父组件发送数据？  
   **答:** 在子组件中使用 `@Output` 装饰器和 `EventEmitter` 向父组件发射数据。

3. **Q:** When would you use a shared service for component communication?  
   **A:** Use shared services when data needs to be shared across multiple unrelated components or when state management is required.

   **中文问答:**  
   **问:** 在何种情况下应使用共享服务进行组件通信？  
   **答:** 当需要在多个不相关的组件之间共享数据或需要状态管理时，应使用共享服务。

4. **Q:** What are some limitations of using `@Input` and `@Output` for communication?  
   **A:** `@Input` and `@Output` are best suited for parent-child communication, but they become cumbersome for deep component hierarchies and unrelated components.

   **中文问答:**  
   **问:** 使用 `@Input` 和 `@Output` 进行通信的局限性是什么？  
   **答:** `@Input` 和 `@Output` 最适合用于父子组件之间的通信，但对于深层组件结构和不相关组件来说，会变得非常繁琐。

5. **Q:** What is the purpose of using state management tools like NgRx in Angular?  
   **A:** State management tools like NgRx provide a centralized store for application state, making it easier to manage and track state changes across components.

   **中文问答:**  
   **问:** 在 Angular 中使用类似 NgRx 的状态管理工具的目的是什么？  
   **答:** 状态管理工具（如 NgRx）提供了应用程序状态的集中存储，使得管理和跟踪组件之间的状态变化更加容易。

---

### 10. What is Parent-Child Relationship in Angular?
**English:**  
In Angular, a parent-child relationship is established when one component is nested inside another. The parent component can pass data to the child component using the `@Input` decorator, and the child component can communicate back to the parent using the `@Output` decorator and `EventEmitter`. This relationship is commonly used for creating modular and reusable components in Angular applications.

**中文:**  
在 Angular 中，当一个组件嵌套在另一个组件内部时，就形成了父子组件关系。父组件可以使用 `@Input` 装饰器向子组件传递数据，而子组件可以通过 `@Output` 装饰器和 `EventEmitter` 向父组件发送数据。这种关系通常用于在 Angular 应用程序中创建模块化和可重用的组件。

**Code Example:**

```typescript
// Parent Component: parent.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-parent',
  template: `
    <h2>Parent Component</h2>
    <app-child [childData]="parentData" (childEvent)="handleChildEvent($event)"></app-child>
    <p>Message from Child: {{ childMessage }}</p>
  `
})
export class ParentComponent {
  parentData = 'Data from Parent';
  childMessage = '';

  handleChildEvent(event: string) {
    this.childMessage = event;
  }
}

// Child Component: child.component.ts
import { Component, Input, Output, EventEmitter } from '@angular/core';

@Component({
  selector: 'app-child',
  template: `
    <h3>Child Component</h3>
    <p>Received from Parent: {{ childData }}</p>
    <button (click)="sendEvent()">Send Data to Parent</button>
  `
})
export class ChildComponent {
  @Input() childData: string;
  @Output() childEvent = new EventEmitter<string>();

  sendEvent() {
    this.childEvent.emit('Data from Child');
  }
}
```

**Explanation:**
1. **Parent to Child Communication:** The `childData` is passed from the parent component to the child component using the `@Input` decorator.
2. **Child to Parent Communication:** The `childEvent` is emitted from the child component and handled in the parent component using the `@Output` decorator and `EventEmitter`.

**中文解释:**
1. **父组件到子组件通信:** `childData` 通过 `@Input` 装饰器从父组件传递到子组件。
2. **子组件到父组件通信:** `childEvent` 通过 `@Output` 装饰器和 `EventEmitter` 从子组件发射，并在父组件中处理。

**Tip:**
- Use `@Input` and `@Output` decorators to establish clear data flow and communication patterns between parent and child components.
- **中文提示:** 使用 `@Input` 和 `@Output` 装饰器在父子组件之间建立清晰的数据流和通信模式。

**Warning:**
- Avoid passing complex objects directly between components as it can cause unexpected behavior and difficult-to-debug errors.
- **中文警告:** 避免在组件之间直接传递复杂对象，这可能会导致意外行为和难以调试的错误。

**5 Interview Questions & Answers:**

1. **Q:** How can a child component communicate with a parent component in Angular?  
   **A:** A child component can communicate with a parent component using the `@Output` decorator and an `EventEmitter` to emit events.

   **中文问答:**  
   **问:** Angular 中子组件如何与父组件进行通信？  
   **答:** 子组件可以使用 `@Output` 装饰器和 `EventEmitter` 向父组件发射事件进行通信。

2. **Q:** What is the use of the `@Input` decorator in Angular?  
   **A:** The `@Input` decorator is used to bind a property in the child component to a value passed from the parent component.

   **中文问答:**  
   **问:** Angular 中 `@Input` 装饰器的作用是什么？  
   **答:** `@Input` 装饰器用于将子组件中的属性绑定到父组件传递的值。

3. **Q:** Can a child component communicate directly with a grandparent component?  
   **A:** No, child components cannot communicate directly with grandparent components. Communication can be done using a shared service or by passing data through parent components.

   **中文问答:**  
   **问:** 子组件能否直接与祖父组件通信？  
   **答:** 不能，子组件不能直接与祖父组件通信。可以使用共享服务或通过父组件传递数据来实现通信。

4. **Q:** What are the best practices for parent-child communication in Angular?  
   **A:** Use `@Input` for passing data from parent to child, and `@Output` for passing data from child to parent. Avoid using global variables or shared services for direct parent-child communication.

   **中文问答:**  
   **问:** Angular 中父子组件通信的最佳实践是什么？  
   **答:** 使用 `@Input` 从父组件向子组件传递数据，并使用 `@Output` 从子组件向父组件传递数据。避免使用全局变量或共享服务进行直接的父子组件通信。

5. **Q:** How would you troubleshoot a situation where data passed from parent to child is not appearing?  
   **A:** Check if the property is correctly decorated with `@Input` in the child component, and verify that the binding syntax in the parent component is correct.

   **中文问答:**  
   **问:** 如何排查从父组件传递到子组件的数据未显示的问题？  
   **答:** 检查子组件中的属性是否正确使用 `@Input` 装饰，并验证父组件中的绑定语法是否正确。

---

### 11. What is `@Input` Decorator?
**English:**  
The `@Input` decorator in Angular allows a parent component to pass data into a child component. It is used to bind a value from the parent component to a property in the child component, making it accessible within the child’s template and logic. `@Input` is typically used when a child component needs to display or manipulate data from its parent component.

**中文:**  
Angular 中的 `@Input` 装饰器允许父组件向子组件传递数据。它用于将父组件中的值绑定到子组件中的属性，使该属性在子组件的模板和逻辑中可访问。`@Input` 通常在子组件需要显示或处理来自父组件的数据时使用。

**Code Example:**

```typescript
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-child',
  template: `
    <h3>Child Component</h3>
    <p>{{ receivedData }}</p>
  `
})
export class ChildComponent {
  @Input() receivedData: string;
}

// Parent Component
@Component({
  selector: 'app-parent',
  template: `
    <h2>Parent Component</h2>
    <app-child [receivedData]="parentData"></app-child>
  `
})
export class ParentComponent {
  parentData = 'Hello from Parent!';
}
```

**Explanation:**
1. **`@Input` Decorator:** Defines `receivedData` in the child component, which receives a value from the `parentData` property in the parent component.
2. **Property Binding:** The `receivedData` property in the child is bound to the `parentData` property in the parent using `[receivedData]="parentData"`.

**中文解释:**
1. **`@Input` 装饰器:** 在子组件中定义 `receivedData` 属性，该属性接收来自父组件 `parentData` 属性的值。
2. **属性绑定:** 子组件中的 `receivedData` 属性通过 `[receivedData]="parentData"` 绑定到父组件的 `parentData` 属性。

**Tip:**
- Always use `@Input` to pass data from parent to child to establish a unidirectional data flow, which is easier to debug and maintain.
- **中文提示:** 始终使用 `@Input` 从父组件向子组件传递数据，以建立单向数据流，这样更易于调试和维护。

**Warning:**
- Avoid modifying the `@Input` property value directly in the child component, as it may lead to unexpected behavior and side effects.
- **中文警告:** 避免在子组件中直接修改 `@Input` 属性值，因为这可能导致意外行为和副作用。

**5 Interview Questions & Answers:**

1. **Q:** What is the purpose of using `@Input` in Angular?  
   **A:** `@Input` is used to pass data from a parent component to a child component.

   **中文问答:**  
   **问:** 在 Angular 中使用 `@Input` 的目的是什么？  
   **答:** `@Input` 用于从父组件向子组件传递数据。

2. **Q:** Can you use `@Input` to pass data from a child component to a parent component?  
   **A:** No, `@Input` is used only for passing data from parent to child. Use `@Output` for passing data from child to parent.

   **中文问答:**  
   **问:** `@Input` 能否用于从子组件向父组件传递数据？  
   **答:** 不能，`@Input

` 只能用于从父组件向子组件传递数据。要从子组件向父组件传递数据，应使用 `@Output`。

3. **Q:** How do you handle property changes in a child component when using `@Input`?  
   **A:** Use the `ngOnChanges` lifecycle hook to handle property changes in a child component.

   **中文问答:**  
   **问:** 使用 `@Input` 时如何在子组件中处理属性变化？  
   **答:** 可以使用 `ngOnChanges` 生命周期钩子在子组件中处理属性变化。

4. **Q:** Can you pass objects as `@Input` values?  
   **A:** Yes, you can pass objects as `@Input` values, but it is recommended to use immutable objects or perform deep copies to prevent unwanted side effects.

   **中文问答:**  
   **问:** 能否将对象作为 `@Input` 值传递？  
   **答:** 可以将对象作为 `@Input` 值传递，但建议使用不可变对象或执行深拷贝以防止意外副作用。

5. **Q:** How would you debug a situation where the `@Input` value is not being displayed correctly?  
   **A:** Check if the parent is passing the value correctly, ensure the child component has the `@Input` decorator, and verify that the binding syntax is correct.

   **中文问答:**  
   **问:** 如何调试 `@Input` 值未正确显示的情况？  
   **答:** 检查父组件是否正确传递了值，确保子组件具有 `@Input` 装饰器，并验证绑定语法是否正确。

---
### 12. What is `@ViewChild` Decorator?
**English:**  
The `@ViewChild` decorator in Angular allows you to access a child component, directive, or DOM element within the parent component. It provides a way to interact directly with the child component’s properties and methods. `@ViewChild` is particularly useful for scenarios where you need to access or manipulate child components programmatically after the view has been initialized.

**中文:**  
Angular 中的 `@ViewChild` 装饰器允许父组件访问子组件、指令或 DOM 元素。它提供了一种方式，可以在视图初始化后直接与子组件的属性和方法交互。`@ViewChild` 在需要以编程方式访问或操作子组件的场景中特别有用。

**Code Example:**

```typescript
import { Component, ViewChild } from '@angular/core';
import { ChildComponent } from './child.component';

@Component({
  selector: 'app-parent',
  template: `
    <h2>Parent Component</h2>
    <app-child></app-child>
    <button (click)="changeChildProperty()">Change Child Property</button>
  `
})
export class ParentComponent {
  @ViewChild(ChildComponent) childComponent!: ChildComponent;

  changeChildProperty() {
    this.childComponent.childMessage = 'Message changed by Parent!';
  }
}

// Child Component
@Component({
  selector: 'app-child',
  template: `<p>{{ childMessage }}</p>`
})
export class ChildComponent {
  childMessage = 'Initial Child Message';
}
```

**Explanation:**
1. **`@ViewChild(ChildComponent)`:** The `@ViewChild` decorator is used to access the `ChildComponent` instance in the parent component.
2. **`changeChildProperty()` Method:** This method in the parent component updates the `childMessage` property of the child component when the button is clicked.

**中文解释:**
1. **`@ViewChild(ChildComponent)`:** `@ViewChild` 装饰器用于在父组件中访问 `ChildComponent` 实例。
2. **`changeChildProperty()` 方法:** 父组件中的该方法在按钮点击时更新子组件的 `childMessage` 属性。

**Tip:**
- Use `@ViewChild` when you need to call a method or access a property in a child component from the parent component.
- **中文提示:** 当需要在父组件中调用子组件的方法或访问子组件的属性时，可以使用 `@ViewChild`。

**Warning:**
- Always check that the `@ViewChild` property is defined after the view has been initialized (e.g., in `ngAfterViewInit`) to avoid undefined errors.
- **中文警告:** 始终检查 `@ViewChild` 属性在视图初始化（如 `ngAfterViewInit`）后是否已定义，以避免未定义错误。

**5 Interview Questions & Answers:**

1. **Q:** What is the purpose of using `@ViewChild` in Angular?  
   **A:** The `@ViewChild` decorator is used to access a child component, directive, or DOM element in the parent component.

   **中文问答:**  
   **问:** 在 Angular 中使用 `@ViewChild` 的目的是什么？  
   **答:** `@ViewChild` 装饰器用于在父组件中访问子组件、指令或 DOM 元素。

2. **Q:** How can you use `@ViewChild` to call a method in a child component?  
   **A:** Use `@ViewChild` to get a reference to the child component instance, then call the method using that reference, e.g., `this.childComponent.someMethod()`.

   **中文问答:**  
   **问:** 如何使用 `@ViewChild` 调用子组件中的方法？  
   **答:** 使用 `@ViewChild` 获取子组件实例的引用，然后使用该引用调用方法，例如 `this.childComponent.someMethod()`。

3. **Q:** What is the difference between `@ViewChild` and `@Input`?  
   **A:** `@Input` is used for passing data from parent to child, while `@ViewChild` is used for accessing child components and their properties or methods in the parent.

   **中文问答:**  
   **问:** `@ViewChild` 和 `@Input` 有什么区别？  
   **答:** `@Input` 用于从父组件向子组件传递数据，而 `@ViewChild` 用于在父组件中访问子组件及其属性或方法。

4. **Q:** In which lifecycle hook is `@ViewChild` typically accessed?  
   **A:** `@ViewChild` is typically accessed in the `ngAfterViewInit` lifecycle hook because the child views are initialized only after this hook is called.

   **中文问答:**  
   **问:** 通常在哪个生命周期钩子中访问 `@ViewChild`？  
   **答:** 通常在 `ngAfterViewInit` 生命周期钩子中访问 `@ViewChild`，因为只有在该钩子调用后子视图才会被初始化。

5. **Q:** How would you troubleshoot a situation where `@ViewChild` is returning `undefined`?  
   **A:** Ensure that the child component exists in the DOM and that the `@ViewChild` property is being accessed after the view is initialized (e.g., in `ngAfterViewInit`).

   **中文问答:**  
   **问:** 如何排查 `@ViewChild` 返回 `undefined` 的情况？  
   **答:** 确保子组件存在于 DOM 中，并且 `@ViewChild` 属性是在视图初始化后（如 `ngAfterViewInit`）访问的。

---

### 13. What is `@Output` and `EventEmitter`?
**English:**  
The `@Output` decorator in Angular, used in conjunction with `EventEmitter`, allows a child component to send data or events back to the parent component. This is commonly used when a child component needs to notify its parent about a change or an action (e.g., button click, form submission). `@Output` and `EventEmitter` establish a communication channel from child to parent.

**中文:**  
Angular 中的 `@Output` 装饰器与 `EventEmitter` 搭配使用，允许子组件将数据或事件发送回父组件。当子组件需要通知父组件某个更改或动作时（例如按钮点击、表单提交），通常会使用 `@Output` 和 `EventEmitter`。`@Output` 和 `EventEmitter` 建立了从子组件到父组件的通信通道。

**Code Example:**

```typescript
import { Component, EventEmitter, Output } from '@angular/core';

@Component({
  selector: 'app-child',
  template: `<button (click)="sendMessage()">Send Message to Parent</button>`
})
export class ChildComponent {
  @Output() messageEvent = new EventEmitter<string>();

  sendMessage() {
    this.messageEvent.emit('Hello from Child!');
  }
}

// Parent Component
@Component({
  selector: 'app-parent',
  template: `
    <h2>Parent Component</h2>
    <app-child (messageEvent)="receiveMessage($event)"></app-child>
    <p>Message from Child: {{ message }}</p>
  `
})
export class ParentComponent {
  message: string;

  receiveMessage($event: string) {
    this.message = $event;
  }
}
```

**Explanation:**
1. **`@Output` and `EventEmitter`:** The child component defines an output property using `@Output` and an instance of `EventEmitter<string>`.
2. **`sendMessage()` Method:** When the button is clicked, the `sendMessage` method emits an event to notify the parent component.
3. **Parent Component’s `receiveMessage()` Method:** The parent component listens to the `messageEvent` and handles it using the `receiveMessage` method.

**中文解释:**
1. **`@Output` 和 `EventEmitter`:** 子组件使用 `@Output` 和 `EventEmitter<string>` 实例定义一个输出属性。
2. **`sendMessage()` 方法:** 当按钮被点击时，`sendMessage` 方法发射一个事件来通知父组件。
3. **父组件的 `receiveMessage()` 方法:** 父组件监听 `messageEvent` 并使用 `receiveMessage` 方法处理它。

**Tip:**
- Use `@Output` and `EventEmitter` for scenarios where a child component needs to inform the parent about an event or state change.
- **中文提示:** 在子组件需要通知父组件某个事件或状态更改的场景中使用 `@Output` 和 `EventEmitter`。

**Warning:**
- Avoid overusing `EventEmitter` for unrelated components, as it can lead to tightly coupled components. Consider using a shared service instead.
- **中文警告:** 避免在不相关组件中过度使用 `EventEmitter`，因为这会导致组件高度耦合。建议使用共享服务替代。

**5 Interview Questions & Answers:**

1. **Q:** What is the purpose of `@Output` in Angular?  
   **A:** The `@Output` decorator is used to create a custom event and pass data from a child component to a parent component using `EventEmitter`.

   **中文问答:**  
   **问:** Angular 中 `@Output` 的作用是什么？  
   **答:** `@Output` 装饰器用于创建自定义事件，并使用 `EventEmitter` 将数据从子组件传递到父组件。



2. **Q:** How does `EventEmitter` work in Angular?  
   **A:** `EventEmitter` creates a custom event that the parent component can subscribe to. It is used with the `@Output` decorator to emit values.

   **中文问答:**  
   **问:** `EventEmitter` 在 Angular 中是如何工作的？  
   **答:** `EventEmitter` 创建一个父组件可以订阅的自定义事件。它与 `@Output` 装饰器一起使用来发射值。

3. **Q:** How would you pass a complex object from a child component to a parent component?  
   **A:** Use `@Output` with `EventEmitter` to emit the complex object, e.g., `this.messageEvent.emit({ name: 'John', age: 30 })`.

   **中文问答:**  
   **问:** 如何将复杂对象从子组件传递到父组件？  
   **答:** 使用 `@Output` 和 `EventEmitter` 发射复杂对象，例如 `this.messageEvent.emit({ name: 'John', age: 30 })`。

4. **Q:** Can `@Output` be used to pass data from parent to child component?  
   **A:** No, `@Output` is used to pass data from child to parent. Use `@Input` for parent-to-child communication.

   **中文问答:**  
   **问:** `@Output` 能否用于将数据从父组件传递到子组件？  
   **答:** 不能，`@Output` 用于将数据从子组件传递到父组件。使用 `@Input` 进行父组件到子组件的通信。

5. **Q:** How can you handle an event emitted by a child component in the parent component?  
   **A:** Bind the emitted event to a parent component method using the `(eventName)="parentMethod($event)"` syntax.

   **中文问答:**  
   **问:** 如何在父组件中处理子组件发射的事件？  
   **答:** 使用 `(eventName)="parentMethod($event)"` 语法将发射的事件绑定到父组件的方法。

---

### 14. What is String Interpolation?
**English:**  
String Interpolation in Angular is a form of data binding used to display dynamic data from the component's class in the HTML template. It is represented using double curly braces (`{{ }}`). String interpolation evaluates the expressions inside the curly braces and converts them into a string that is displayed in the template. It is mainly used to bind properties, method results, or variables from the component class to the view.

**中文:**  
Angular 中的字符串插值是一种数据绑定形式，用于在 HTML 模板中显示来自组件类的动态数据。它使用双大括号 (`{{ }}`) 表示。字符串插值会计算大括号内的表达式，并将其转换为字符串显示在模板中。它主要用于将组件类中的属性、方法结果或变量绑定到视图中。

**Code Example:**

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-interpolation',
  template: `
    <h2>Welcome, {{ userName }}!</h2>
    <p>The current year is {{ currentYear }}</p>
    <p>Sum of 10 and 20 is {{ addNumbers(10, 20) }}</p>
  `
})
export class InterpolationComponent {
  userName = 'Angular Developer';
  currentYear = new Date().getFullYear();

  addNumbers(a: number, b: number): number {
    return a + b;
  }
}
```

**Explanation:**
1. **`{{ userName }}`:** Displays the value of the `userName` property from the component class.
2. **`{{ currentYear }}`:** Displays the current year using the `currentYear` property.
3. **`{{ addNumbers(10, 20) }}`:** Calls the `addNumbers` method and displays the result of adding 10 and 20.

**中文解释:**
1. **`{{ userName }}`:** 显示组件类中 `userName` 属性的值。
2. **`{{ currentYear }}`:** 使用 `currentYear` 属性显示当前年份。
3. **`{{ addNumbers(10, 20) }}`:** 调用 `addNumbers` 方法，并显示 10 和 20 相加的结果。

**Tip:**
- Use string interpolation for simple property bindings, and for displaying method results or expressions in the template.
- **中文提示:** 使用字符串插值进行简单属性绑定，以及在模板中显示方法结果或表达式。

**Warning:**
- Avoid using complex logic inside interpolation expressions as it can lead to performance issues.
- **中文警告:** 避免在插值表达式中使用复杂逻辑，因为这可能导致性能问题。

**5 Interview Questions & Answers:**

1. **Q:** What is string interpolation in Angular?  
   **A:** String interpolation is a form of data binding in Angular that binds component class properties, methods, or variables to the view using double curly braces (`{{ }}`).

   **中文问答:**  
   **问:** Angular 中的字符串插值是什么？  
   **答:** 字符串插值是 Angular 中的一种数据绑定形式，使用双大括号 (`{{ }}`) 将组件类的属性、方法或变量绑定到视图中。

2. **Q:** Can string interpolation be used to call methods in Angular?  
   **A:** Yes, string interpolation can call methods in the component class, but it is recommended to use it for simple expressions only.

   **中文问答:**  
   **问:** 字符串插值能否用于调用 Angular 中的方法？  
   **答:** 可以，字符串插值可以调用组件类中的方法，但建议仅用于简单表达式。

3. **Q:** How do you perform property binding using string interpolation?  
   **A:** You can perform property binding using `{{ propertyName }}`, where `propertyName` is a variable or a property from the component class.

   **中文问答:**  
   **问:** 如何使用字符串插值进行属性绑定？  
   **答:** 可以使用 `{{ propertyName }}` 进行属性绑定，其中 `propertyName` 是组件类中的变量或属性。

4. **Q:** What are the limitations of string interpolation?  
   **A:** String interpolation can only bind to properties and expressions that result in a string. It cannot be used for complex data manipulation or multi-line expressions.

   **中文问答:**  
   **问:** 字符串插值的局限性是什么？  
   **答:** 字符串插值只能绑定到结果为字符串的属性和表达式。它不能用于复杂的数据操作或多行表达式。

5. **Q:** Can you bind HTML content using string interpolation?  
   **A:** No, string interpolation only binds text content. To bind HTML content, use property binding with `[innerHTML]`.

   **中文问答:**  
   **问:** 能否使用字符串插值绑定 HTML 内容？  
   **答:** 不能，字符串插值只能绑定文本内容。要绑定 HTML 内容，可以使用 `[innerHTML]` 属性绑定。

---

### 15. What is Property Binding?
**English:**  
Property Binding in Angular is a technique that allows you to bind the values of component properties to the attributes or properties of HTML elements in the template. It is represented using square brackets (`[property]="expression"`). Property binding helps dynamically set element properties, such as disabling a button, changing the source of an image, or setting a CSS class.

**中文:**  
Angular 中的属性绑定是一种技术，允许将组件属性的值绑定到模板中 HTML 元素的属性上。它使用方括号 (`[property]="expression"`) 表示。属性绑定可以动态地设置元素的属性，例如禁用按钮、更改图片源或设置 CSS 类。

**Code Example:**

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-property-binding',
  template: `
    <button [disabled]="isButtonDisabled">Click Me</button>
    <img [src]="imageUrl" alt="Angular Logo" />
    <p [innerHTML]="htmlContent"></p>
  `
})
export class PropertyBindingComponent {
  isButtonDisabled = true;
  imageUrl = 'https://angular.io/assets/images/logos/angular/angular.png';
  htmlContent = '<span style="color: red">This is HTML content bound using property binding.</span>';
}
```

**Explanation:**
1. **`[disabled]="isButtonDisabled"`:** Binds the `disabled` attribute of the button to the `isButtonDisabled` property.
2. **`[src]="imageUrl"`:** Sets the image source dynamically using the `imageUrl` property.
3. **`[innerHTML]="htmlContent"`:** Binds the `innerHTML` property of the `<p>` tag to display dynamic HTML content.

**中文解释:**
1. **`[disabled]="isButtonDisabled"`:** 将按钮的 `disabled` 属性绑定到 `isButtonDisabled` 属性。
2. **`[src]="imageUrl"`:** 使用 `imageUrl` 属性动态设置图片源。
3. **`[innerHTML]="htmlContent"`:** 将 `<p>` 标签的 `innerHTML` 属性绑定到动态 HTML 内容。

**Tip:**
- Use property binding for dynamically setting attributes and properties of elements that are dependent on the component’s data.
- **中文提示:** 对于依赖组件数据的元素属性和属性设置，使用属性绑定。

**Warning:**
- Ensure that the property names used in property binding are valid properties of the target HTML element.
- **中文警告:** 确保在属性绑定中使用的属性名称是目标 HTML 元素的有效属性。

**5 Interview Questions & Answers:**

1. **Q:** What is property binding in Angular?  
   **A:** Property binding is a data binding technique used to bind component properties to the attributes or properties of HTML elements.

   **中文问答:**  
   **问:** Angular 中的属性绑定是什么？  
   **答:** 属性绑定是一种数据绑定技术，用于将组件属性绑定到 HTML 元素的属性上。

2. **Q:** How is property binding different from attribute binding?  
   **A:** Property binding binds to the DOM properties of an element, whereas attribute binding only changes the initial state of the attributes.

   **中文问答:**  
   **问:** 属性绑定与属性（attribute）绑定有何不同？  
   **答:** 属性绑定绑定到元素的 DOM 属性，而属性（attribute）绑定仅更改属性的初始状态。

3. **Q:** How would you disable a button conditionally using property binding?  
   **A:** Use `[disabled]="isButtonDisabled"`, where `isButtonDisabled` is a boolean property in the component class.

   **中文问答:**  
   **问:** 如何使用属性绑定有条件地禁用按钮？  
   **答:** 使用 `[disabled]="isButtonDisabled"`，其中 `isButtonDisabled` 是组件类中的布尔属性。

4. **Q:** Can property binding be used to bind methods to element properties?  
   **A:** No, property binding should only be used for binding values or expressions that result in a value. Use event binding to handle methods.

   **中文问答:**  
   **问:** 属性绑定能否用于将方法绑定到元素属性？  
   **答:** 不能，属性绑定仅用于绑定值或表达式的结果。使用事件绑定来处理方法。

5. **Q:** What are some common use cases for property binding?  
   **A:** Common use cases include dynamically disabling elements, changing image sources

, setting CSS classes, and binding HTML content.

   **中文问答:**  
   **问:** 属性绑定的常见用例有哪些？  
   **答:** 常见用例包括动态禁用元素、更改图片源、设置 CSS 类和绑定 HTML 内容。

---

### 16. What is Class Binding?
**English:**  
Class Binding in Angular is a type of property binding used to dynamically add or remove CSS classes from an HTML element. It uses the `[class]` syntax or `[class.class-name]` syntax. With class binding, you can conditionally apply CSS classes to an element based on the values of component properties. This technique is particularly useful for styling elements dynamically or applying multiple classes at once.

**中文:**  
Angular 中的类绑定是一种属性绑定形式，用于动态地向 HTML 元素添加或移除 CSS 类。它使用 `[class]` 语法或 `[class.class-name]` 语法。通过类绑定，可以根据组件属性的值有条件地将 CSS 类应用到元素。这种技术在动态样式元素或一次性应用多个类时非常有用。

**Code Example:**

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-class-binding',
  template: `
    <div [class.active]="isActive">Active Class</div>
    <div [class]="currentClass">Current Class</div>
    <button (click)="toggleActive()">Toggle Active Class</button>
  `,
  styles: [
    `.active { color: green; }`,
    `.highlight { font-weight: bold; }`
  ]
})
export class ClassBindingComponent {
  isActive = true;
  currentClass = 'highlight';

  toggleActive() {
    this.isActive = !this.isActive;
  }
}
```

**Explanation:**
1. **`[class.active]="isActive"`:** Adds or removes the `active` class based on the `isActive` property.
2. **`[class]="currentClass"`:** Dynamically applies the value of the `currentClass` property as the class name.
3. **`toggleActive()` Method:** Toggles the `isActive` property value between `true` and `false`, which in turn toggles the `active` class on the first `<div>`.

**中文解释:**
1. **`[class.active]="isActive"`:** 根据 `isActive` 属性的值添加或移除 `active` 类。
2. **`[class]="currentClass"`:** 动态地将 `currentClass` 属性的值作为类名应用。
3. **`toggleActive()` 方法:** 在 `true` 和 `false` 之间切换 `isActive` 属性值，从而在第一个 `<div>` 上切换 `active` 类。

**Tip:**
- Use class binding to dynamically style elements based on state changes in the component, such as applying active classes on button clicks or conditionally highlighting elements.
- **中文提示:** 使用类绑定根据组件中的状态变化动态设置元素样式，例如在按钮点击时应用 active 类或有条件地高亮显示元素。

**Warning:**
- Avoid using too many class bindings on a single element as it can lead to cluttered templates and reduce readability.
- **中文警告:** 避免在单个元素上使用过多的类绑定，这会导致模板混乱并降低可读性。

**5 Interview Questions & Answers:**

1. **Q:** What is class binding in Angular?  
   **A:** Class binding is a property binding technique used to add or remove CSS classes dynamically on an HTML element based on component property values.

   **中文问答:**  
   **问:** Angular 中的类绑定是什么？  
   **答:** 类绑定是一种属性绑定技术，根据组件属性的值动态地向 HTML 元素添加或移除 CSS 类。

2. **Q:** How do you conditionally apply a CSS class using class binding?  
   **A:** Use `[class.class-name]="expression"`, where `class-name` is the CSS class, and `expression` is a boolean property in the component class.

   **中文问答:**  
   **问:** 如何使用类绑定有条件地应用 CSS 类？  
   **答:** 使用 `[class.class-name]="expression"`，其中 `class-name` 是 CSS 类，`expression` 是组件类中的布尔属性。

3. **Q:** Can you apply multiple CSS classes dynamically using class binding?  
   **A:** Yes, use `[class]="expression"`, where `expression` is a string of class names separated by spaces or an object mapping class names to boolean values.

   **中文问答:**  
   **问:** 能否使用类绑定动态地应用多个 CSS 类？  
   **答:** 可以，使用 `[class]="expression"`，其中 `expression` 是以空格分隔的类名字符串，或者是将类名映射为布尔值的对象。

4. **Q:** How do you toggle a CSS class dynamically using class binding?  
   **A:** Use a boolean property in the component class and bind it using `[class.class-name]="property"`. Change the property value to toggle the class.

   **中文问答:**  
   **问:** 如何使用类绑定动态地切换 CSS 类？  
   **答:** 在组件类中使用布尔属性，并使用 `[class.class-name]="property"` 进行绑定。更改属性值来切换类。

5. **Q:** What is the difference between `[ngClass]` and class binding?  
   **A:** `[ngClass]` provides more flexibility and allows applying multiple classes conditionally, while class binding (`[class]`) is mainly for single class binding.

   **中文问答:**  
   **问:** `[ngClass]` 和类绑定的区别是什么？  
   **答:** `[ngClass]` 提供了更多的灵活性，可以有条件地应用多个类，而类绑定 (`[class]`) 主要用于单个类的绑定。

---

### 17. What is Style Binding?
**English:**  
Style Binding in Angular is a technique that allows you to dynamically set the styles of an HTML element using the `[style]` or `[style.style-property]` syntax. It binds a component property to a CSS style property, allowing the style to change based on the component’s state or data. This is particularly useful for dynamically changing visual aspects like background color, width, height, or margins.

**中文:**  
Angular 中的样式绑定是一种技术，它使用 `[style]` 或 `[style.style-property]` 语法动态设置 HTML 元素的样式。它将组件属性绑定到 CSS 样式属性，使样式可以根据组件的状态或数据而变化。这在动态更改背景颜色、宽度、高度或边距等视觉属性时特别有用。

**Code Example:**

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-style-binding',
  template: `
    <p [style.color]="textColor">This text has dynamic color!</p>
    <p [style.fontSize.px]="fontSize">This text has dynamic font size!</p>
    <button (click)="increaseFontSize()">Increase Font Size</button>
  `
})
export class StyleBindingComponent {
  textColor = 'blue';
  fontSize = 16;

  increaseFontSize() {
    this.fontSize += 2;
  }
}
```

**Explanation:**
1. **`[style.color]="textColor"`:** Sets the `color` style property of the paragraph based on the `textColor` property.
2. **`[style.fontSize.px]="fontSize"`:** Sets the `fontSize` in pixels (`px`) based on the `fontSize` property.
3. **`increaseFontSize()` Method:** Increases the `fontSize` property by 2 units whenever the button is clicked, dynamically changing the text size.

**中文解释:**
1. **`[style.color]="textColor"`:** 根据 `textColor` 属性设置段落的 `color` 样式属性。
2. **`[style.fontSize.px]="fontSize"`:** 根据 `fontSize` 属性以像素（`px`）为单位设置 `fontSize` 样式属性。
3. **`increaseFontSize()` 方法:** 每次点击按钮时将 `fontSize` 属性增加 2 个单位，从而动态地更改文本大小。

**Tip:**
- Use style binding for dynamic style changes such as hover effects, responsive layouts, or user interaction effects.
- **中文提示:** 使用样式绑定进行动态样式更改，例如悬停效果、响应式布局或用户交互效果。

**Warning:**
- Ensure that the style property names in `[style]` or `[style.style-property]` are correctly spelled and match the CSS property names.
- **中文警告:** 确保 `[style]` 或 `[style.style-property]` 中的样式属性名称拼写正确，并与 CSS 属性名称匹配。

**5 Interview Questions & Answers:**

1. **Q:** What is style binding in Angular?  
   **A:** Style binding is a data binding technique used to bind component properties to CSS style properties of HTML elements dynamically.

   **中文问答:**  
   **问:** Angular 中的样式绑定是什么？  
   **答:** 样式绑定是一种数据绑定技术，用于将组件属性动态地绑定到 HTML 元素的 CSS 样式属性。

2. **Q:** How do you dynamically set a CSS property using style binding?  
   **A:** Use `[style.style-property]="expression"`, where `style-property` is the CSS property to bind, and `expression` is a component property.

   **中文问答:**  
   **问:** 如何使用样式绑定动态地设置 CSS 属性？  
   **答:** 使用

 `[style.style-property]="expression"`，其中 `style-property` 是要绑定的 CSS 属性，`expression` 是组件属性。

3. **Q:** Can you use style binding for setting styles like `px`, `em`, or `%`?  
   **A:** Yes, you can specify units such as `px`, `em`, or `%` using `[style.property.unit]="value"` syntax, e.g., `[style.width.px]="width"`.

   **中文问答:**  
   **问:** 样式绑定能否用于设置 `px`、`em` 或 `%` 等单位的样式？  
   **答:** 可以，使用 `[style.property.unit]="value"` 语法指定单位，例如 `[style.width.px]="width"`。

4. **Q:** How do you apply multiple styles dynamically using style binding?  
   **A:** Use `[style]="styleObject"`, where `styleObject` is an object containing key-value pairs of style properties and their values.

   **中文问答:**  
   **问:** 如何使用样式绑定动态地应用多个样式？  
   **答:** 使用 `[style]="styleObject"`，其中 `styleObject` 是一个包含样式属性及其值的键值对对象。

5. **Q:** What is the difference between `[style]` and `[ngStyle]`?  
   **A:** `[style]` is used for binding a single style property, whereas `[ngStyle]` is used for binding multiple styles at once using an object.

   **中文问答:**  
   **问:** `[style]` 和 `[ngStyle]` 有何区别？  
   **答:** `[style]` 用于绑定单个样式属性，而 `[ngStyle]` 用于使用对象一次性绑定多个样式。

---

### 18. What is Event Binding?
**English:**  
Event Binding in Angular is a technique used to listen to events, such as user interactions, and execute component logic based on those events. It uses the `()` syntax, where the event name (e.g., `click`, `input`, `change`) is placed inside the parentheses. Event Binding allows you to respond to user actions such as button clicks, keyboard inputs, mouse movements, and more.

**中文:**  
Angular 中的事件绑定是一种用于监听事件（如用户交互）并基于这些事件执行组件逻辑的技术。它使用 `()` 语法，其中事件名称（如 `click`、`input`、`change`）放置在括号内。事件绑定使您能够响应用户操作，例如按钮点击、键盘输入、鼠标移动等。

**Code Example:**

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-event-binding',
  template: `
    <button (click)="onClick()">Click Me</button>
    <input (input)="onInputChange($event)" placeholder="Type something..." />
    <p>{{ inputText }}</p>
  `
})
export class EventBindingComponent {
  inputText = '';

  onClick() {
    alert('Button was clicked!');
  }

  onInputChange(event: any) {
    this.inputText = event.target.value;
  }
}
```

**Explanation:**
1. **`(click)="onClick()"`:** Binds the `click` event of the button to the `onClick()` method, which displays an alert message.
2. **`(input)="onInputChange($event)"`:** Binds the `input` event of the text input field to the `onInputChange()` method, which updates the `inputText` property with the value typed by the user.

**中文解释:**
1. **`(click)="onClick()"`:** 将按钮的 `click` 事件绑定到 `onClick()` 方法，该方法显示一个提示消息。
2. **`(input)="onInputChange($event)"`:** 将文本输入框的 `input` 事件绑定到 `onInputChange()` 方法，该方法使用用户输入的值更新 `inputText` 属性。

**Tip:**
- Use event binding to handle user interactions such as form submissions, button clicks, and keypress events to trigger corresponding component logic.
- **中文提示:** 使用事件绑定处理用户交互，例如表单提交、按钮点击和按键事件，以触发相应的组件逻辑。

**Warning:**
- Avoid using event binding for heavy computational logic, as it can cause performance issues and slow down the UI.
- **中文警告:** 避免在事件绑定中使用繁重的计算逻辑，因为这可能会导致性能问题并减慢 UI 的响应速度。

**5 Interview Questions & Answers:**

1. **Q:** What is event binding in Angular?  
   **A:** Event binding is a technique used to bind an event (e.g., click, input) in the HTML template to a method in the component class.

   **中文问答:**  
   **问:** Angular 中的事件绑定是什么？  
   **答:** 事件绑定是一种将 HTML 模板中的事件（如 click、input）与组件类中的方法绑定的技术。

2. **Q:** How do you pass event data to a method using event binding?  
   **A:** Use `$event` to pass the event data to the method, e.g., `(click)="methodName($event)"`.

   **中文问答:**  
   **问:** 如何使用事件绑定将事件数据传递给方法？  
   **答:** 使用 `$event` 将事件数据传递给方法，例如 `(click)="methodName($event)"`。

3. **Q:** Can event binding be used for custom events?  
   **A:** Yes, event binding can be used for both native events (e.g., click) and custom events emitted by child components.

   **中文问答:**  
   **问:** 事件绑定能否用于自定义事件？  
   **答:** 可以，事件绑定既可以用于原生事件（如 click），也可以用于子组件发射的自定义事件。

4. **Q:** What is the difference between property binding and event binding?  
   **A:** Property binding binds data from the component to the view, whereas event binding binds an event in the view to a method in the component.

   **中文问答:**  
   **问:** 属性绑定和事件绑定有什么区别？  
   **答:** 属性绑定将数据从组件绑定到视图，而事件绑定将视图中的事件绑定到组件中的方法。

5. **Q:** How can you prevent default event actions in event binding?  
   **A:** Use `$event.preventDefault()` inside the event handler method to prevent the default action of an event.

   **中文问答:**  
   **问:** 如何在事件绑定中阻止默认事件操作？  
   **答:** 在事件处理方法中使用 `$event.preventDefault()` 来阻止事件的默认操作。

---

### 19. What is Event Filtering?
**English:**  
Event Filtering in Angular is a technique used to listen for specific events or to conditionally execute logic based on event properties. Event filtering allows you to filter out certain events (e.g., key presses) and execute code only if specific conditions are met. This technique is useful when you want to restrict event handling to specific keys or inputs.

**中文:**  
Angular 中的事件过滤是一种用于监听特定事件或根据事件属性有条件地执行逻辑的技术。事件过滤允许您筛选出某些事件（如按键）并仅在满足特定条件时执行代码。这种技术在您希望将事件处理限制为特定按键或输入时特别有用。

**Code Example:**

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-event-filtering',
  template: `
    <input (keydown)="onKeyDown($event)" placeholder="Type something..." />
    <p>{{ message }}</p>
  `
})
export class EventFilteringComponent {
  message = '';

  onKeyDown(event: KeyboardEvent) {
    if (event.key === 'Enter') {
      this.message = 'Enter key pressed!';
    } else {
      this.message = 'Please press the Enter key.';
    }
  }
}
```

**Explanation:**
1. **`(keydown)="onKeyDown($event)"`:** Binds the `keydown` event of the input field to the `onKeyDown()` method.
2. **Event Filtering:** The `onKeyDown()` method checks if the pressed key is `Enter`. If it is, a message is displayed; otherwise, a different message is shown.

**中文解释:**
1. **`(keydown)="onKeyDown($event)"`:** 将输入框的 `keydown` 事件绑定到 `onKeyDown()` 方法。
2. **事件过滤:** `onKeyDown()` 方法检查按下的是否是 `Enter` 键。如果是，则显示一条消息；否则，显示另一条消息。

**Tip:**
- Use event filtering to handle keyboard events, such as executing logic only when the `Enter` key is pressed or preventing unwanted keypresses.
- **中文提示:** 使用事件过滤处理键盘事件，例如仅在按下 `Enter` 键时执行逻辑或阻止不需要的按键。

**Warning:**
- Avoid using complex logic in event filtering, as it can make the code harder to maintain and understand.
- **中文警告:** 避免在事件过滤中使用复杂逻辑，因为这会使代码难以维护和理解。

**5 Interview Questions & Answers:**

1. **Q:** What is event filtering in Angular?  
   **A:** Event filtering is a technique used to listen for specific events or conditionally execute logic based on event properties, such as filtering key presses or mouse events.

   **中文问答:**  
   **问:** Angular 中的事件过滤是什么？  
   **答:** 事件过滤是一种用于监听特定事件或根据事件属性有条件地执行逻辑的技术，例如筛选按键事件或鼠标事件。

2. **Q:** How can you filter keyboard events in Angular?  
   **A:** Use event filtering with the `keydown` or `keypress` events and check the `event.key` or `event.keyCode` properties to filter specific keys.

   **中文问答:**  
   **问:** 如何在 Angular 中过滤键盘事件？  
   **答:** 使用 `keydown` 或 `keypress` 事件进行事件过滤，并检查 `event.key` 或 `event.keyCode` 属性来过滤特定按键。

3. **Q:** Can event filtering be used with custom events?  
   **A:** Yes, event filtering can be applied to both native and custom events by checking specific event properties.

   **中文问答:**  
   **问:** 事件过滤能否用于自定义事件？  
   **答:** 可以，事件过滤既可以用于原生事件，也可以用于自定义事件，通过检查特定的事件属性进行过滤。

4. **Q:** What is the difference between event binding and event filtering?  
   **A:** Event binding connects an event in the template to a method in the component, while event filtering adds conditional logic to execute code based on event properties.

   **中文问答:**  
   **问:** 事件绑定和事件过滤的区别是什么？  
   **答:** 事件绑定将模板中的事件与组件中的方法连接起来，而事件过滤在事件属性的基础上添加条件

逻辑以执行代码。

5. **Q:** How can you prevent certain keys from being pressed using event filtering?  
   **A:** Use `event.preventDefault()` inside the event handler method when the undesired key is detected.

   **中文问答:**  
   **问:** 如何使用事件过滤防止按下某些键？  
   **答:** 当检测到不需要的按键时，在事件处理方法中使用 `event.preventDefault()`。

---


### 20. What is Template Variable?
**English:**  
A Template Variable in Angular is a way to reference a DOM element or an Angular component within the HTML template. It is declared using the `#variableName` syntax. Template variables can be used to access DOM properties, call component methods, or pass data between different parts of the template. They provide a means to manipulate or interact with elements directly within the view.

**中文:**  
Angular 中的模板变量是一种在 HTML 模板中引用 DOM 元素或 Angular 组件的方法。它使用 `#variableName` 语法声明。模板变量可以用于访问 DOM 属性、调用组件方法或在模板的不同部分之间传递数据。它们提供了一种直接在视图中操作或与元素交互的方式。

**Code Example:**

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-template-variable',
  template: `
    <input #inputBox type="text" placeholder="Enter text" />
    <button (click)="logInput(inputBox.value)">Log Input</button>
  `
})
export class TemplateVariableComponent {
  logInput(value: string) {
    console.log('Input Value:', value);
  }
}
```

**Explanation:**
1. **`#inputBox` Template Variable:** Declares a template variable named `inputBox` for the input element.
2. **`inputBox.value`:** Uses the template variable to access the value of the input element and passes it to the `logInput()` method when the button is clicked.

**中文解释:**
1. **`#inputBox` 模板变量:** 为输入元素声明一个名为 `inputBox` 的模板变量。
2. **`inputBox.value`:** 使用模板变量访问输入元素的值，并在按钮点击时将其传递给 `logInput()` 方法。

**Tip:**
- Use template variables when you need to directly access or manipulate a DOM element's properties in the component’s template.
- **中文提示:** 当需要在组件的模板中直接访问或操作 DOM 元素的属性时，可以使用模板变量。

**Warning:**
- Template variables are limited to the scope of the template in which they are declared and cannot be accessed in other templates or components.
- **中文警告:** 模板变量仅限于在声明它们的模板中使用，不能在其他模板或组件中访问。

**5 Interview Questions & Answers:**

1. **Q:** What is a template variable in Angular?  
   **A:** A template variable is a reference to a DOM element or component instance that can be accessed within the template using `#variableName`.

   **中文问答:**  
   **问:** Angular 中的模板变量是什么？  
   **答:** 模板变量是对 DOM 元素或组件实例的引用，可以在模板中使用 `#variableName` 访问。

2. **Q:** How do you declare a template variable in Angular?  
   **A:** Use the `#variableName` syntax within the HTML template to declare a template variable.

   **中文问答:**  
   **问:** 如何在 Angular 中声明模板变量？  
   **答:** 在 HTML 模板中使用 `#variableName` 语法声明模板变量。

3. **Q:** Can you use template variables to call methods of a component?  
   **A:** Yes, you can use template variables to call methods of a component if the variable is referencing that component.

   **中文问答:**  
   **问:** 能否使用模板变量调用组件的方法？  
   **答:** 可以，如果模板变量引用的是该组件，则可以使用模板变量调用组件的方法。

4. **Q:** What are some limitations of template variables?  
   **A:** Template variables are limited to the scope of the template in which they are declared and cannot be used to communicate across different components or templates.

   **中文问答:**  
   **问:** 模板变量有哪些局限性？  
   **答:** 模板变量仅限于声明它们的模板作用域中使用，不能用于不同组件或模板之间的通信。

5. **Q:** How can you access a DOM element’s property using a template variable?  
   **A:** Use `#variableName.property`, where `variableName` is the template variable name and `property` is the DOM property, e.g., `inputBox.value`.

   **中文问答:**  
   **问:** 如何使用模板变量访问 DOM 元素的属性？  
   **答:** 使用 `#variableName.property`，其中 `variableName` 是模板变量名，`property` 是 DOM 属性，例如 `inputBox.value`。

---


