### What is the difference between Component, Attribute, and Structural Directives?

In Angular, directives are special instructions that can alter the behavior, appearance, or structure of the DOM. There are three types of directives: **Component**, **Attribute**, and **Structural Directives**. Each has distinct roles and characteristics.

---

### Differences between Component, Structural, and Attribute Directives

```markdown
| Type                  | Description                                                                 | Example                            | Starts With           |
|-----------------------|-----------------------------------------------------------------------------|------------------------------------|-----------------------|
| **Component Directive** | Responsible for displaying the first whole view. It is the most used directive. | `@Component`                      | `@`                   |
| **Structural Directive** | Responsible for adding or deleting HTML elements in the view.                | `*ngIf`, `*ngFor`, `*ngSwitch`     | `*`                   |
| **Attribute Directive**  | Responsible for changing the appearance of the view by adding or removing styles/CSS classes. | `[ngClass]`, `[ngStyle]`          | Square brackets `[]`  |
```


---

#### 1. **Component Directives**:
   - **Definition**: A component directive is a directive with a template. It controls a part of the user interface by defining a view and the logic behind that view.
   - **Use Case**: Used to create reusable components with their own view, styling, and behavior.
   - **Example**:
     ```typescript
     @Component({
       selector: 'app-hello',
       template: '<h1>Hello, {{name}}!</h1>',
     })
     export class HelloComponent {
       name = 'Angular';
     }
     ```

#### 2. **Attribute Directives**:
   - **Definition**: Attribute directives change the appearance or behavior of an element, component, or another directive. They don't modify the DOM structure but rather affect the element or component itself.
   - **Use Case**: Used to modify the attributes or properties of existing elements.
   - **Examples**:
     - **[ngClass]**: Applies classes conditionally.
     - **[ngStyle]**: Modifies the inline styles dynamically.
   - **Example**:
     ```html
     <div [ngClass]="{'active-class': isActive}">Styled Div</div>
     ```

#### 3. **Structural Directives**:
   - **Definition**: Structural directives change the DOM layout by adding or removing elements. They modify the DOM structure based on conditions or loops.
   - **Use Case**: Used to create or remove elements from the DOM dynamically.
   - **Examples**:
     - **\*ngIf**: Conditionally adds or removes an element.
     - **\*ngFor**: Repeats an element for each item in a list.
   - **Example**:
     ```html
     <p *ngIf="isLoggedIn">Welcome User</p>
     
     <ul>
       <li *ngFor="let item of items">{{ item }}</li>
     </ul>
     ```

---

### Comparison Table:

| Type                | Purpose                                       | Example                                    | Modifies DOM Structure?       |
|---------------------|-----------------------------------------------|--------------------------------------------|-------------------------------|
| **Component**        | Encapsulates UI logic and view                | `<app-hello></app-hello>`                  | No                            |
| **Attribute Directive** | Changes appearance or behavior of an element | `[ngClass]="{'active-class': isActive}"`    | No                            |
| **Structural Directive** | Changes DOM structure by adding/removing elements | `*ngIf`, `*ngFor`, `*ngSwitch`             | Yes                           |

---

### Summary:
- **Component Directives**: Control UI and encapsulate behavior and templates.
- **Attribute Directives**: Modify the behavior or appearance of existing elements without changing the DOM structure.
- **Structural Directives**: Modify the DOM by adding or removing elements based on certain conditions.

---

### Key Points:
- **Component Directives** are used for creating UI components with logic and templates.
- **Attribute Directives** change how elements are rendered without altering the structure of the DOM.
- **Structural Directives** modify the DOM by adding or removing elements.

---

### 5 Interview Questions on Directives:

1. **What is the purpose of Structural Directives in Angular?**
   - **Answer**: Structural Directives change the DOM layout by adding or removing elements dynamically.

2. **How does Angular identify Structural Directives?**
   - **Answer**: Angular identifies Structural Directives by the `*` prefix (e.g., `*ngIf`, `*ngFor`).

3. **Can you apply multiple Structural Directives on a single element?**
   - **Answer**: No, you cannot apply multiple structural directives on a single element. However, you can nest them within one another.

4. **What is the key difference between a Component and an Attribute Directive?**
   - **Answer**: A Component has a template and encapsulates both the UI and logic, while an Attribute Directive modifies the behavior or appearance of an existing element without a template.

5. **Give an example of when to use [ngClass] vs. *ngIf.**
   - **Answer**: Use `[ngClass]` to conditionally apply CSS classes without removing the element from the DOM, while `*ngIf` should be used to conditionally add or remove elements from the DOM.
