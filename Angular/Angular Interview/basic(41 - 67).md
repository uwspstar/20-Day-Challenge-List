### 41. What is `@Injectable` Decorator?
**English:**  
The `@Injectable` decorator in Angular marks a class as a service that can be injected into other classes using Angular’s dependency injection system. It tells Angular that this class is available to be provided and used by components or other services. The `@Injectable` decorator is required if a service needs to inject another service or if you want to configure how the service is provided.

**中文:**  
Angular 中的 `@Injectable` 装饰器将类标记为可使用 Angular 的依赖注入系统注入到其他类中的服务。它告诉 Angular 该类可由组件或其他服务提供和使用。如果服务需要注入另一个服务，或您希望配置服务的提供方式，则必须使用 `@Injectable` 装饰器。

**Code Example:**

```typescript
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class DataService {
  getData() {
    return ['Item 1', 'Item 2', 'Item 3'];
  }
}
```

**Explanation:**
1. **`@Injectable({ providedIn: 'root' })`**: Specifies that the `DataService` is a singleton service that is provided at the root level, making it available to the entire application.
2. **Singleton Service**: Since the service is provided at the root level, only one instance of the service is created and shared across the application.

**中文解释:**
1. **`@Injectable({ providedIn: 'root' })`**: 指定 `DataService` 为在根级别提供的单例服务，使其可用于整个应用程序。
2. **单例服务:** 由于服务在根级别提供，因此整个应用程序中只会创建一个服务实例并共享使用。

**Tip:**
- Use the `@Injectable` decorator to configure how a service is provided, making it easier to manage dependencies and control service instantiation.
- **中文提示:** 使用 `@Injectable` 装饰器配置服务的提供方式，从而更容易管理依赖项并控制服务的实例化。

**Warning:**
- Forgetting to add the `@Injectable` decorator to a service that injects other dependencies can lead to runtime errors.
- **中文警告:** 忘记在需要注入其他依赖项的服务中添加 `@Injectable` 装饰器可能会导致运行时错误。

**5 Interview Questions & Answers:**

1. **Q:** What is the purpose of the `@Injectable` decorator in Angular?  
   **A:** The `@Injectable` decorator marks a class as a service that can be injected into other components or services.

   **中文问答:**  
---
