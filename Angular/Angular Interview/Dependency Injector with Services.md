### How to use Dependency Injector with Services in Angular

In Angular, **Dependency Injection (DI)** is a core concept that allows you to inject services and other dependencies into components, directives, and other services. This makes code modular, testable, and reusable by managing how instances of services are created and shared across the application.

---

### Steps to Use Dependency Injection with Services:

#### 1. **Create a Service**
   A service in Angular is a class that contains business logic, reusable methods, and data. Services are typically marked with the `@Injectable` decorator, which makes them eligible for dependency injection.
   
   ```typescript
   @Injectable({
     providedIn: 'root',
   })
   export class DataService {
     getData() {
       return ['Data 1', 'Data 2', 'Data 3'];
     }
   }
   ```
   - The `@Injectable` decorator tells Angular that this class can be injected into other components or services.
   - The `providedIn: 'root'` option ensures that this service is available globally (singleton).

#### 2. **Inject the Service into a Component**
   To inject a service into a component, declare it in the component's constructor. Angular automatically provides an instance of the service, thanks to DI.

   ```typescript
   @Component({
     selector: 'app-root',
     template: '<h1>{{ data }}</h1>',
   })
   export class AppComponent {
     data: string[];

     constructor(private dataService: DataService) {
       this.data = this.dataService.getData();
     }
   }
   ```
   - The service (`DataService`) is injected into the `AppComponent` by specifying it in the constructor with the `private` keyword.
   - Angular's dependency injector will automatically create an instance of `DataService` and inject it into the component.

#### 3. **Provide the Service at Different Levels**
   Services can be provided at different levels in Angular:
   - **Root Level** (Global Singleton): When provided in the root (using `providedIn: 'root'`), a single instance of the service is created and shared across the app.
   - **Component Level**: You can also provide services locally within specific modules or components, limiting the scope of the service to that module or component.

   Example of providing service at the component level:
   ```typescript
   @Component({
     selector: 'app-user',
     templateUrl: './user.component.html',
     providers: [UserService],  // Service is scoped to this component
   })
   export class UserComponent {
     constructor(private userService: UserService) {}
   }
   ```

#### 4. **Use the Service in the Template**
   The data fetched from the service can be used in the template through data binding.

   ```html
   <!-- app.component.html -->
   <ul>
     <li *ngFor="let item of data">{{ item }}</li>
   </ul>
   ```

---

### Summary:
- **Dependency Injection** is a design pattern used to inject dependencies (such as services) into classes like components.
- You create services using the `@Injectable` decorator and inject them into components using the constructor.
- Services can be provided globally or locally, depending on how you want to scope them.

---

### Key Points:
- Use `@Injectable` to define services eligible for injection.
- Inject services into components by adding them to the constructor.
- Services can be provided globally (via `providedIn: 'root'`) or locally at the component or module level.
- Dependency injection promotes loose coupling, making the code more modular and testable.

---

### 5 Interview Questions on Dependency Injection:

1. **What is Dependency Injection in Angular?**
   - **Answer**: Dependency Injection (DI) is a design pattern used in Angular to inject services and dependencies into components and other classes, which allows for better code modularity, reusability, and testing.

2. **How do you create and inject a service in Angular?**
   - **Answer**: A service is created with the `@Injectable` decorator and injected into a component by including it in the constructor.
   ```typescript
   constructor(private dataService: DataService) {}
   ```

3. **What is the purpose of `providedIn: 'root'` in services?**
   - **Answer**: The `providedIn: 'root'` option makes the service available globally as a singleton, so only one instance of the service is shared across the entire application.

4. **How do you provide a service only at the component level?**
   - **Answer**: You can provide a service at the component level by adding it to the `providers` array in the component metadata.
   ```typescript
   @Component({
     providers: [UserService],
   })
   ```

5. **What is the difference between `@Injectable` and `@Inject` in Angular?**
   - **Answer**: `@Injectable` marks a class as a service that can be injected, while `@Inject` is used to inject a specific instance of a service or value into a class manually.

---
### What is Hierarchical Dependency Injection?

**Hierarchical Dependency Injection (DI)** in Angular is a system in which injectors are arranged in a hierarchy, allowing child injectors to inherit or override services from parent injectors. This provides flexibility in managing service instances across different parts of an application. Angular injectors work hierarchically, meaning that a service can be scoped to a specific module, component, or the entire application.

The injector hierarchy in Angular enables the creation of multiple instances of services at different levels of the application, making services reusable and configurable depending on where they are needed.

---

### How Hierarchical Dependency Injection Works:

1. **Root Injector**:
   - The root injector is created when the application starts, and it is responsible for providing services globally across the entire app. Services provided at the root level are singletons, meaning the same instance is shared throughout the app.
   - **Example**: Services provided with `providedIn: 'root'`.

   ```typescript
   @Injectable({
     providedIn: 'root',
   })
   export class GlobalService {
     // This service is available globally.
   }
   ```

2. **Module Injector**:
   - Angular modules can have their own injectors. You can provide services within specific modules, which will limit the availability of the service to that module.
   - **Example**: Providing a service in a feature module.

   ```typescript
   @NgModule({
     providers: [FeatureService],
   })
   export class FeatureModule {}
   ```

3. **Component Injector**:
   - Each Angular component also has its own injector. Services provided at the component level are scoped only to that component and its child components, meaning different instances of the service can exist at different components.
   - **Example**: Providing a service in a specific component's metadata.

   ```typescript
   @Component({
     selector: 'app-user',
     providers: [UserService],  // Scoped to this component and its children
     template: '<p>User Component</p>',
   })
   export class UserComponent {
     constructor(private userService: UserService) {}
   }
   ```

4. **Child Injector**:
   - Each component’s child component inherits services from the parent’s injector unless overridden by a new provider. This means that child components can access services from their parent components but can also provide their own instances of services if necessary.

   ```typescript
   @Component({
     selector: 'app-child',
     providers: [ChildService],  // This overrides the parent's service
     template: '<p>Child Component</p>',
   })
   export class ChildComponent {
     constructor(private childService: ChildService) {}
   }
   ```

---

### Example of Hierarchical Dependency Injection:

```typescript
@Injectable({
  providedIn: 'root',
})
export class AppService {
  // This service is available globally (singleton)
}

@Component({
  selector: 'app-parent',
  providers: [ParentService],  // This service is scoped to the ParentComponent and its children
  template: '<app-child></app-child>',
})
export class ParentComponent {
  constructor(private parentService: ParentService) {}
}

@Component({
  selector: 'app-child',
  template: '<p>Child component</p>',
})
export class ChildComponent {
  constructor(private parentService: ParentService) {}  // This will use the parent's ParentService instance
}
```

---

### Key Features of Hierarchical Dependency Injection:

1. **Inheritance**: Services provided at higher levels (root or parent component) are inherited by child components unless explicitly overridden.
2. **Scoping**: Services can be scoped at the global (root), module, or component level, allowing for fine control over their lifecycle and usage.
3. **Instance Control**: Angular can create new instances of a service for a particular component or reuse existing instances from a parent injector.

---

### Summary:
- **Hierarchical DI** means that Angular injectors are organized in a hierarchy, where child injectors inherit services from parent injectors.
- You can provide services at different levels—global, module, or component—and control whether they are shared or unique at each level.
- Components in Angular can share services or have their own unique instances of a service, depending on how the service is provided.

---

### Key Points:
- The **root injector** provides services globally across the application.
- **Module injectors** provide services within a specific module.
- **Component injectors** provide services only to a specific component and its child components.
- Hierarchical DI allows child components to inherit services from parent components unless overridden.

---

### 5 Interview Questions on Hierarchical Dependency Injection:

1. **What is the role of the root injector in Angular?**
   - **Answer**: The root injector is responsible for providing services globally across the entire application. Services provided with `providedIn: 'root'` are available application-wide and are singletons.

2. **How can you limit the scope of a service to a specific module in Angular?**
   - **Answer**: You can provide the service in the `providers` array of the module to limit its availability to that specific module.
   ```typescript
   @NgModule({
     providers: [FeatureService],
   })
   export class FeatureModule {}
   ```

3. **What happens when a service is provided at both the parent and child component level?**
   - **Answer**: The child component will receive its own instance of the service if it provides the service locally. Otherwise, it will inherit the instance from the parent component.

4. **How does Angular handle service inheritance in hierarchical DI?**
   - **Answer**: In hierarchical DI, child components automatically inherit services from their parent component unless they explicitly provide their own instance of the service.

5. **How can you override a service provided by a parent component in a child component?**
   - **Answer**: You can override the service by providing a different instance of the service in the `providers` array of the child component.
   ```typescript
   @Component({
     providers: [ChildService],
   })
   export class ChildComponent {}
   ```
   ---
### What is the role of @Injectable Decorator in a Service?

The `@Injectable` decorator in Angular is used to define a class as a service that can participate in dependency injection. It tells Angular’s **Dependency Injection (DI)** system that the class is available to be injected as a dependency in other classes (such as components or other services). This allows Angular to manage the lifecycle of service instances and inject them where required.

The `@Injectable` decorator is typically used with service classes, making them part of Angular's dependency injection system. Without this decorator, Angular wouldn’t be able to provide an instance of the service, as it wouldn't know that the class is meant for injection.

---

### Key Features of the `@Injectable` Decorator:

1. **Marking a Service for Injection**:
   - The `@Injectable` decorator is necessary for making a service class injectable. This means Angular’s DI system knows that this class can be injected into other components or services.
   - **Example**:
     ```typescript
     @Injectable({
       providedIn: 'root',
     })
     export class DataService {
       getData() {
         return ['Data 1', 'Data 2', 'Data 3'];
       }
     }
     ```

2. **`providedIn` Property**:
   - The `providedIn` property defines where the service is provided. The most common value is `'root'`, which makes the service available globally (as a singleton) throughout the entire application.
   - **Options for `providedIn`**:
     - **`root`**: The service is available globally and provided by the root injector.
     - **`any`**: A new instance of the service is created with each lazy-loaded module.
     - **Module Name**: The service is available only in the specified module.

   - **Example**:
     ```typescript
     @Injectable({
       providedIn: 'root',
     })
     export class GlobalService {}
     ```

3. **Handling Dependency Injection**:
   - The `@Injectable` decorator allows Angular to resolve any dependencies a service might have, by injecting them into the constructor of the service.
   - If a service has dependencies on other services, the `@Injectable` decorator tells Angular to resolve those dependencies as well.
   - **Example**:
     ```typescript
     @Injectable()
     export class UserService {
       constructor(private http: HttpClient) {}
     }
     ```

4. **Enabling Singleton Instances**:
   - When the `providedIn: 'root'` is used, the service will be provided as a singleton across the entire application. This means only one instance of the service is created and shared across the app.

---

### Example of `@Injectable` in Use:

```typescript
@Injectable({
  providedIn: 'root',  // This service is provided globally
})
export class AuthService {
  constructor(private http: HttpClient) {}

  login(username: string, password: string) {
    return this.http.post('/api/login', { username, password });
  }
}
```

In this example:
- `AuthService` is marked with the `@Injectable` decorator, which means Angular can inject this service into any component or other service that needs it.
- The `providedIn: 'root'` makes the service available globally throughout the application.

---

### Summary:
- The `@Injectable` decorator tells Angular that a service can be injected into other components or services.
- It enables Angular's DI system to resolve dependencies and manage the lifecycle of the service.
- The `providedIn` property determines the scope of the service, typically using `'root'` to provide the service globally.

---

### Key Points:
- **`@Injectable`** makes a service available for injection throughout the application.
- The **`providedIn`** property defines where and how the service is provided (globally, by module, etc.).
- **Singleton services** can be created when using `providedIn: 'root'`.
- If a service requires other dependencies, they are injected through the constructor, thanks to the `@Injectable` decorator.

---

### 5 Interview Questions on `@Injectable` Decorator:

1. **Why is the `@Injectable` decorator necessary in Angular services?**
   - **Answer**: The `@Injectable` decorator marks a class as a service that can be injected via Angular's dependency injection system. Without it, Angular wouldn’t know that the class is meant to be injectable.

2. **What does `providedIn: 'root'` mean in the `@Injectable` decorator?**
   - **Answer**: `providedIn: 'root'` means the service is provided at the root level of the application and is available globally as a singleton.

3. **What happens if you don’t use `@Injectable` in a service class?**
   - **Answer**: Without `@Injectable`, Angular cannot inject the service into other components or services because it won't recognize the class as a part of its DI system.

4. **Can you inject a service into another service? How?**
   - **Answer**: Yes, you can inject a service into another service by using the `@Injectable` decorator in both services and then adding the dependent service to the constructor of the injecting service.
   ```typescript
   constructor(private authService: AuthService) {}
   ```

5. **What is the difference between providing a service in the `@Injectable` decorator and the `providers` array of a module/component?**
   - **Answer**: When using `providedIn: 'root'` in `@Injectable`, the service is provided globally across the application. When providing a service in the `providers` array, it is scoped to that module or component, and each time a new instance may be created.
