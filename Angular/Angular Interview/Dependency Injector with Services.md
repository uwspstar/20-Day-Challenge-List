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
