### What are Directives? What are the types of directives?

**Directives** in Angular are special markers in the DOM that Angular uses to attach behavior to elements. Directives can change the appearance, behavior, or layout of a DOM element in the Angular application. They are an essential feature of Angular for manipulating the DOM, adding dynamic functionality, and controlling the structure of the view.

---

#### Types of Directives in Angular:

1. **Component Directives**
   - These directives are actually components. A component is a directive with a template. They control a piece of the user interface (UI).
   - **Example**: 
     ```typescript
     @Component({
       selector: 'app-hello',
       template: '<h1>Hello Angular!</h1>',
     })
     export class HelloComponent {}
     ```

2. **Attribute Directives**
   - Attribute directives change the appearance or behavior of an element, component, or another directive.
   - **Examples**:
     - **[ngStyle]**: Used to modify an element’s style dynamically.
     - **[ngClass]**: Used to conditionally apply CSS classes.

     ```html
     <p [ngStyle]="{'color': isActive ? 'green' : 'red'}">This is a colored text.</p>
     ```

3. **Structural Directives**
   - Structural directives change the DOM layout by adding or removing elements. They typically use the `*` prefix.
   - **Examples**:
     - **\*ngIf**: Adds or removes an element based on a condition.
     - **\*ngFor**: Repeats an element for each item in a list.
     - **\*ngSwitch**: Conditionally switches between elements based on a case.

     ```html
     <!-- ngIf Example -->
     <div *ngIf="isLoggedIn">Welcome, User!</div>
     
     <!-- ngFor Example -->
     <ul>
       <li *ngFor="let item of items">{{ item }}</li>
     </ul>
     ```

---

### Summary:
Directives in Angular are key to modifying the behavior or structure of the DOM. Components themselves are special directives with a template. Attribute directives are used for appearance and behavior changes, while structural directives handle DOM structure manipulation.

---

### Key Points:
- **Component Directives**: Control sections of the UI using templates.
- **Attribute Directives**: Modify appearance and behavior of elements.
- **Structural Directives**: Add or remove elements from the DOM.

---

### 5 Interview Questions on Directives:

1. **What is the difference between an Attribute Directive and a Structural Directive?**
   - **Answer**: Attribute directives modify the appearance or behavior of elements without changing the DOM structure, while structural directives modify the DOM structure by adding or removing elements.

2. **How do you conditionally apply a class to an element using Angular?**
   - **Answer**: You can use the `[ngClass]` directive to apply classes based on conditions.
   ```html
   <div [ngClass]="{'active-class': isActive}">This is a div</div>
   ```

3. **Can a component be considered a directive?**
   - **Answer**: Yes, a component is a special type of directive with a template attached.

4. **How can you render a list of items using a directive in Angular?**
   - **Answer**: You can use the `*ngFor` structural directive to loop through an array and render each item.
   ```html
   <li *ngFor="let item of items">{{ item }}</li>
   ```

5. **What happens if the condition for `*ngIf` is false?**
   - **Answer**: If the condition is false, the element with `*ngIf` will not be rendered in the DOM.

