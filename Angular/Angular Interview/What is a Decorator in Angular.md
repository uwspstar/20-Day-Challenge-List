### What is a Decorator in Angular?

A **decorator** in Angular is a special type of function that is applied to classes, methods, or properties to add metadata, modify behavior, or extend functionality. Angular heavily relies on decorators to define key aspects of an application such as components, services, and modules.

Decorators are a core feature of TypeScript, used by Angular to define and configure how classes work under the hood. They allow Angular to identify and process these classes and methods with additional functionalities.

---

#### Types of Decorators in Angular:

1. **Class Decorators**
   - Used to define components, directives, modules, and services.
   - **Example**: `@Component`, `@NgModule`, `@Injectable`
   ```typescript
   @Component({
     selector: 'app-root',
     templateUrl: './app.component.html',
   })
   export class AppComponent {
     title = 'my-angular-app';
   }
   ```

2. **Property Decorators**
   - Used to bind properties inside the class.
   - **Example**: `@Input`, `@Output`
   ```typescript
   export class ChildComponent {
     @Input() childProperty: string;
   }
   ```

3. **Method Decorators**
   - Used to attach metadata to methods in classes.
   - **Example**: `@HostListener`
   ```typescript
   export class AppComponent {
     @HostListener('click', ['$event'])
     onClick(event: Event) {
       console.log('Element clicked:', event);
     }
   }
   ```

4. **Parameter Decorators**
   - Used to define metadata on function parameters.
   - **Example**: `@Inject` for Dependency Injection
   ```typescript
   constructor(@Inject(SomeService) private service: SomeService) {}
   ```
### What are the types of Decorators in Angular?

Angular provides several types of decorators to define classes, methods, properties, and parameters. These decorators help Angular interpret and compile code, making it easier to work with metadata, dependency injection, and component binding.

#### Types of Decorators:

1. **Class Decorators**: 
   - Used to define classes and attach metadata.
   - **Examples**: `@Component`, `@NgModule`, `@Injectable`, `@Directive`, `@Pipe`
   
2. **Property Decorators**: 
   - Used to bind properties of a class, typically for parent-child communication or DOM manipulation.
   - **Examples**: `@Input`, `@Output`, `@ContentChild`, `@ViewChild`, `@HostBinding`
   
3. **Method Decorators**: 
   - Used to modify or listen to methods or DOM events.
   - **Examples**: `@HostListener`
   
4. **Parameter Decorators**: 
   - Used to inject metadata into class constructors.
   - **Examples**: `@Inject`, `@Self`, `@Host`, `@SkipSelf`, `@Optional`

---

### Comparison Table:

| Type                 | Purpose                                           | Common Examples                                     |
|----------------------|---------------------------------------------------|-----------------------------------------------------|
| **Class Decorators**  | Define components, modules, services, and pipes   | `@Component`, `@NgModule`, `@Injectable`, `@Pipe`   |
| **Property Decorators** | Bind properties, manage data flow between components | `@Input`, `@Output`, `@ViewChild`, `@HostBinding`   |
| **Method Decorators** | Listen to or modify DOM events and methods        | `@HostListener`                                     |
| **Parameter Decorators** | Inject dependencies into constructors            | `@Inject`, `@Self`, `@Host`, `@Optional`, `@SkipSelf` |

---

### Summary:

- **Class Decorators** are used to define the metadata for components, services, and modules.
- **Property Decorators** allow data flow between components and elements.
- **Method Decorators** manage how methods are executed or listened to.
- **Parameter Decorators** inject dependencies into classes, handling how services and other data are provided.

---

### 5 Interview Questions on Decorators:

1. **What is the purpose of the `@Component` decorator in Angular?**
   - **Answer**: The `@Component` decorator is used to define a class as a component and includes metadata like the selector, template, and style files.

2. **How do you use `@Input` and `@Output` decorators?**
   - **Answer**: `@Input` is used to pass data from a parent component to a child, and `@Output` is used to emit events from the child to the parent.

3. **What is the role of `@HostListener` in Angular?**
   - **Answer**: `@HostListener` listens to events on the host element and allows you to handle DOM events like `click`, `mouseover`, etc., in the component.

4. **How do you inject a service into a component using decorators?**
   - **Answer**: Use `@Injectable` to mark a service class, and Angular's `@Inject` or constructor to inject it into a component.

5. **Can you explain the difference between `@Inject` and `@Optional` decorators?**
   - **Answer**: `@Inject` is used to inject a dependency into a class, while `@Optional` makes the dependency injection optional, meaning if the service isn’t provided, the class can still function.
---

### Summary:
Decorators in Angular are functions that add metadata and modify the behavior of classes, methods, or properties. They play a key role in Angular by helping define components, services, modules, and how dependencies are injected into these elements.

---

### Key Points:
- **Class Decorators**: Define metadata for components, services, and modules.
- **Property Decorators**: Bind properties in components.
- **Method Decorators**: Define how methods behave.
- **Parameter Decorators**: Inject dependencies into constructors.

---

### 5 Interview Questions on Decorators:

1. **What is the purpose of a decorator in Angular?**
   - **Answer**: Decorators add metadata to classes, methods, or properties, allowing Angular to define and modify their behavior.

2. **How do you define a Component in Angular?**
   - **Answer**: A component is defined using the `@Component` decorator, which includes metadata like `selector` and `template`.
   ```typescript
   @Component({
     selector: 'app-root',
     templateUrl: './app.component.html',
   })
   ```

3. **What is the role of the `@Injectable` decorator?**
   - **Answer**: The `@Injectable` decorator marks a class as available for dependency injection.

4. **How do you pass data from a parent component to a child component using a decorator?**
   - **Answer**: You use the `@Input()` decorator to pass data from a parent to a child component.
   ```typescript
   @Input() childProperty: string;
   ```

5. **What is the difference between `@Input` and `@Output`?**
   - **Answer**: `@Input` is used to pass data **into** a component, while `@Output` is used to emit events **out** of a component to the parent.

