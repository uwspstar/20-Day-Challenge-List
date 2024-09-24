# Top 50

---

### 1. **What is Angular?**
Angular is a TypeScript-based open-source framework developed by Google, used to build web applications, especially single-page applications (SPAs).

```typescript
// Basic Angular component
@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
})
export class AppComponent {
  title = 'my-angular-app';
}
```

---

### 2. **What are Angular advantages?**
- **Modularity**: Code is organized in modules, making the application easier to maintain.
- **Two-way Data Binding**: Changes in the view are reflected in the model and vice versa.
- **Dependency Injection**: Promotes better testing and design by injecting dependencies.
- **TypeScript Support**: TypeScript adds strong typing and better tooling support.
- **High Performance**: Provides optimizations like Ahead-of-Time (AOT) compilation.

---

### 3. **What is the difference between AngularJS and Angular?**
- **AngularJS**: Based on JavaScript, uses a MVC architecture, and works with directives like `ng-bind`, `ng-model`.
- **Angular (Angular 2+)**: Based on TypeScript, uses a component-based architecture, and has improved performance.

```typescript
// AngularJS example
angular.module('myApp', []).controller('myCtrl', function($scope) {
  $scope.message = 'Hello AngularJS!';
});

// Angular example
@Component({
  selector: 'app-root',
  template: '<h1>{{ message }}</h1>',
})
export class AppComponent {
  message = 'Hello Angular!';
}
```

---

### 4. **What is NPM?**
NPM stands for Node Package Manager, a tool that allows you to install libraries, packages, and dependencies for your Angular project.

```bash
# Installing Angular CLI with npm
npm install -g @angular/cli
```

---

### 5. **What is CLI tool?**
CLI (Command Line Interface) is a tool that allows you to scaffold, build, and maintain Angular applications via commands.

```bash
# Creating a new Angular project
ng new my-angular-app

# Serving the Angular application
ng serve
```

---

### 6. **What are Components in Angular?**
Components are the fundamental building blocks of Angular applications. They control a part of the screen (view) and consist of a template, styles, and logic.

```typescript
@Component({
  selector: 'app-hello',
  template: '<h1>Hello {{ name }}</h1>',
})
export class HelloComponent {
  name = 'Angular';
}
```

---

### 7. **What is a Selector and Template?**
- **Selector**: Defines the HTML tag where the component will be rendered.
- **Template**: Defines the view, written in HTML, and optionally using Angular directives.

```typescript
@Component({
  selector: 'app-hello',
  template: '<h1>Hello {{ name }}</h1>',
})
export class HelloComponent {
  name = 'Angular';
}
```

---

### 8. **What is Module in Angular? What is app.module.ts file?**
Modules are containers for components, services, directives, etc. The `app.module.ts` file is the root module where components are declared, and the Angular app starts.

```typescript
@NgModule({
  declarations: [AppComponent],
  imports: [BrowserModule],
  providers: [],
  bootstrap: [AppComponent],
})
export class AppModule {}
```

---

### 9. **How an Angular App gets Loaded and Started? What are index.html, app-root, selector, and main.ts?**
- **index.html**: Entry HTML file, includes `<app-root></app-root>`.
- **app-root**: The selector for the root component, defined in `app.component.ts`.
- **main.ts**: The main entry point for the Angular app, bootstraps the `AppModule`.

```typescript
// main.ts
platformBrowserDynamic().bootstrapModule(AppModule)
  .catch(err => console.error(err));
```

---

### 10. **What is a Bootstrapped Module & Bootstrapped Component?**
- **Bootstrapped Module**: The root module that starts the Angular application.
- **Bootstrapped Component**: The root component that Angular renders when the application starts.

```typescript
// app.module.ts
@NgModule({
  declarations: [AppComponent],
  bootstrap: [AppComponent]
})
export class AppModule {}
```

---

### [11. **What is Data Binding in Angular?**](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/Angular/Angular%20Interview/What%20is%20Data%20Binding%20in%20Angular.md)
Data Binding refers to the synchronization between the model and the view in Angular.

```html
<!-- Two-way data binding -->
<input [(ngModel)]="username" />
<p>Your username is: {{ username }}</p>
```

---

### 12. **What is String Interpolation in Angular?**
String Interpolation allows you to embed expressions within the template.

```html
<!-- Example of string interpolation -->
<p>Hello, {{ name }}!</p>
```

---

### 13. **What is Property Binding in Angular?**
Property binding binds a property in the template to a component property.

```html
<!-- Property binding -->
<button [disabled]="isDisabled">Click me</button>
```

---

### 14. **What is Event Binding in Angular?**
Event binding binds an event in the template to a method in the component.

```html
<!-- Event binding -->
<button (click)="onClick()">Click me</button>
```

---

### 15. **What is Two-way Binding in Angular?**
Two-way binding allows the synchronization of data between the view and the component.

```html
<!-- Two-way binding with ngModel -->
<input [(ngModel)]="username" />
```

---

### 16. **What are Directives? What are the types of directives?**
Directives are special markers that Angular uses to apply behavior to elements.
- **Structural Directives**: Modify the DOM (e.g., `*ngIf`, `*ngFor`).
- **Attribute Directives**: Modify the appearance or behavior of elements (e.g., `[ngStyle]`, `[ngClass]`).

---

### 17. **What is *ngIf Structural directive?**
`*ngIf` adds or removes elements from the DOM based on a condition.

```html
<p *ngIf="isLoggedIn">Welcome back!</p>
```

---

### 18. **What is *ngFor Structural directive?**
`*ngFor` loops through an array and renders elements for each item.

```html
<ul>
  <li *ngFor="let item of items">{{ item }}</li>
</ul>
```

---

### 19. **What is *ngSwitch Structural directive?**
`*ngSwitch` allows you to conditionally display one element out of many options.

```html
<div [ngSwitch]="role">
  <p *ngSwitchCase="'admin'">Admin</p>
  <p *ngSwitchCase="'user'">User</p>
  <p *ngSwitchDefault>Guest</p>
</div>
```

---

### 20. **What is [ngStyle] Attribute directive?**
`[ngStyle]` dynamically sets the styles of an element based on a component property.

```html
<p [ngStyle]="{color: 'red', 'font-size': '20px'}">Styled Text</p>
```

---

### 21. **What is [ngClass] Attribute directive?**
`[ngClass]` dynamically sets CSS classes based on conditions in the component.

```html
<p [ngClass]="{active: isActive}">This is a paragraph</p>
```

---

### 22. **What is the difference between Component, Attribute, and Structural Directives?**
- **Component Directives**: Define a template with a selector (e.g., `<app-component>`).
- **Attribute Directives**: Modify the appearance or behavior of elements (e.g., `[ngClass]`).
- **Structural Directives**: Modify the structure of the DOM (e.g., `*ngIf`, `*ngFor`).

---

### 23. **What is Decorator?**
A decorator is a special type of declaration that modifies classes or properties.

```typescript
@Component({
  selector: 'app-root',
  template: '<h1>Hello</h1>',
})
export class AppComponent {}
```

---

### 24. **What are the types of Decorator?**
- **Class Decorators**: Used to define a component or service (e.g., `@Component`, `@Injectable`).
- **Property Decorators**: Used to define properties in a class (e.g., `@Input`, `@Output`).

---

### 25. **What are Pipes? What are the types of Pipes & Parameterized Pipes?**
Pipes transform output in the template. Parameterized pipes take arguments for transformation.

```html
<!-- Date pipe with parameter -->
<p>{{ today | date:'shortDate' }}</p>
```

---

### 26. **What is Chaining Pipes?**
Chaining pipes allows you to apply multiple transformations.

```html
<!-- Chaining pipes -->
<p>{{ price | currency:'USD':'symbol' | uppercase }}</p>
```

---

### 27. **Explain Services with Example?**
Services are singleton objects in Angular used to share logic across components.

```typescript
@Injectable()
export class DataService {
  getData() {
    return ['Data1', 'Data2'];
  }
}
```

---

### 28. **How to create Service in Angular?**
Use Angular CLI to create a service.

```bash
# Create a service
ng generate service data
```

---

### 29. **How to use Dependency Injector with Services

 in Angular?**
Inject services via the component constructor.

```typescript
constructor(private dataService: DataService) {}
```

---

### 30. **What is Hierarchical Dependency Injection?**
Angular’s DI allows services to be registered at different levels such as root, module, or component, giving you control over service scope.

---

### 31. **What is Provider in Angular?**
A provider tells Angular how to create a service.

---

### 32. **What is the role of @Injectable Decorator in a Service?**
Marks a class as injectable to be used in dependency injection.

```typescript
@Injectable({
  providedIn: 'root',
})
export class DataService {
  constructor() {}
}
```

---

### 33. **What are Parent-Child Components?**
Parent-child components are components that have a hierarchical relationship, where the parent passes data to the child.

```typescript
// Parent component
<app-child [childProperty]="parentData"></app-child>

// Child component
@Input() childProperty: string;
```

---

### 34. **What are Lifecycle Hooks in Angular?**
Lifecycle hooks are methods that allow you to hook into key events in a component's life cycle.

```typescript
ngOnInit() {
  console.log('Component initialized');
}
```

---

### 35. **What is a Constructor in Angular?**
A constructor is used for class instantiation in Angular and is called when the class is initialized.

---

### 36. **What is ngOnInit lifecycle hook in Angular?**
`ngOnInit` is called after Angular initializes the component's data-bound properties.

---

### 37. **What is the difference between constructor and ngOnInit?**
- **Constructor**: Used to initialize the class.
- **ngOnInit**: Used to handle additional initialization logic after the component’s properties are set.

---

### 38. **What are Asynchronous operations?**
Asynchronous operations run separately from the main program flow and are typically used for tasks like HTTP requests.

```typescript
this.http.get('https://api.example.com/data').subscribe(data => {
  console.log(data);
});
```

---

### 39. **What is the difference between Promise and Observable?**
- **Promise**: Handles a single asynchronous event.
- **Observable**: Handles multiple asynchronous events over time.

```typescript
// Observable example
this.dataService.getData().subscribe(data => console.log(data));
```

---

### 40. **What is RxJS?**
RxJS is a library for composing asynchronous and event-based programs using Observables.

---

### 41. **What is Observable? How to implement Observable?**
An observable is a stream of data that can emit multiple values over time.

```typescript
const observable = new Observable(observer => {
  observer.next('Data 1');
  observer.next('Data 2');
});
```

---

### 42. **What is the role of HttpClient in Angular?**
`HttpClient` is used to make HTTP requests and return Observables.

```typescript
this.http.get('https://api.example.com/data').subscribe(data => {
  console.log(data);
});
```

---

### 43. **What is Typescript? Or What is the difference between Typescript and Javascript?**
TypeScript is a strongly-typed superset of JavaScript that compiles down to JavaScript.

---

### 44. **What is the difference between let and var keyword?**
- **let**: Block-scoped.
- **var**: Function-scoped.

```typescript
let x = 10; // Block-scoped
var y = 20; // Function-scoped
```

---

### 45. **What is Type Annotation?**
Type annotation explicitly declares the type of a variable or function parameter.

```typescript
let name: string = 'John';
```

---

### 46. **What are Built-in/Primitive and User-Defined/Non-primitive Types in Typescript?**
- **Primitive types**: `string`, `number`, `boolean`, `null`, `undefined`.
- **User-defined types**: Interfaces, classes, and types defined by the user.

```typescript
interface User {
  name: string;
  age: number;
}
```

---

### 47. **What is "any" type in Typescript?**
The `any` type disables type-checking for that variable.

```typescript
let value: any = 'Hello';
value = 123; // No error
```

---

### 48. **What is Enum type in Typescript?**
Enums allow you to define a set of named constants.

```typescript
enum Role {
  Admin,
  User,
  Guest,
}
```

---

### 49. **What is Type Assertion in Typescript?**
Type assertion is a way to override the inferred type of a variable.

```typescript
let value: any = 'This is a string';
let strLength: number = (value as string).length;
```

---

### 50. **What are Arrow Functions in Typescript?**
Arrow functions provide a shorter syntax for writing functions and bind `this` lexically.

```typescript
const add = (a: number, b: number): number => a + b;
```

---

This list provides detailed answers and code examples for each question. You can modify or expand each example as needed.
