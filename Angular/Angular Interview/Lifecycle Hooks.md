### What are Lifecycle Hooks in Angular?

**Lifecycle Hooks** in Angular are special methods that allow developers to tap into key moments of a component or directive's life cycle. These hooks provide visibility into various stages from the initialization of a component or directive to its destruction. Angular calls these methods automatically during the different phases of a component's existence.

Lifecycle hooks are particularly useful for executing code at specific stages of a component's creation, update, and removal, such as fetching data when a component initializes or cleaning up resources when a component is destroyed.

---

### Key Lifecycle Hooks in Angular:

1. **`ngOnChanges()`**
   - **Purpose**: Invoked when any of the component's input properties change.
   - **Use Case**: Ideal for reacting to changes in `@Input` data.
   - **Example**:
     ```typescript
     @Component({ ... })
     export class MyComponent implements OnChanges {
       @Input() data: string;

       ngOnChanges(changes: SimpleChanges) {
         console.log('Data changed:', changes.data.currentValue);
       }
     }
     ```

2. **`ngOnInit()`**
   - **Purpose**: Called once after the first `ngOnChanges`. It is used for component initialization.
   - **Use Case**: Fetch data or initialize properties after component creation.
   - **Example**:
     ```typescript
     ngOnInit() {
       console.log('Component initialized');
     }
     ```

3. **`ngDoCheck()`**
   - **Purpose**: Invoked during every change detection run, whether Angular detects changes or not.
   - **Use Case**: Custom change detection logic.
   - **Example**:
     ```typescript
     ngDoCheck() {
       console.log('Change detection triggered');
     }
     ```

4. **`ngAfterContentInit()`**
   - **Purpose**: Called after Angular projects external content into the component’s view (content projection).
   - **Use Case**: Work with projected content, like using `<ng-content>`.
   - **Example**:
     ```typescript
     ngAfterContentInit() {
       console.log('Content projected');
     }
     ```

5. **`ngAfterContentChecked()`**
   - **Purpose**: Invoked after every check of the component’s content.
   - **Use Case**: Respond after Angular checks for changes in the projected content.
   - **Example**:
     ```typescript
     ngAfterContentChecked() {
       console.log('Content checked');
     }
     ```

6. **`ngAfterViewInit()`**
   - **Purpose**: Called after Angular initializes the component's view (and child views).
   - **Use Case**: Access and work with view children and other DOM elements after the view has been fully initialized.
   - **Example**:
     ```typescript
     ngAfterViewInit() {
       console.log('View initialized');
     }
     ```

7. **`ngAfterViewChecked()`**
   - **Purpose**: Invoked after every check of the component’s view.
   - **Use Case**: Respond to changes in the component’s view or child views.
   - **Example**:
     ```typescript
     ngAfterViewChecked() {
       console.log('View checked');
     }
     ```

8. **`ngOnDestroy()`**
   - **Purpose**: Called before Angular destroys the component.
   - **Use Case**: Perform cleanup, such as unsubscribing from observables, canceling HTTP requests, or removing event listeners.
   - **Example**:
     ```typescript
     ngOnDestroy() {
       console.log('Component destroyed');
     }
     ```

---

### Summary of Lifecycle Hooks:

| Hook                      | Description                                               | Use Case                                              |
|---------------------------|-----------------------------------------------------------|-------------------------------------------------------|
| **`ngOnChanges()`**        | Called when an input property changes                     | React to changes in `@Input()`                        |
| **`ngOnInit()`**           | Called after the first `ngOnChanges()`                    | Initialization logic, fetch data                      |
| **`ngDoCheck()`**          | Invoked during each change detection run                  | Custom change detection                               |
| **`ngAfterContentInit()`** | Called after content projection is initialized            | Work with projected content                           |
| **`ngAfterContentChecked()`** | Called after every check of projected content            | Respond to content checks                             |
| **`ngAfterViewInit()`**    | Called after the view is initialized                      | Access view children                                  |
| **`ngAfterViewChecked()`** | Called after every check of the view                      | Respond to view changes                               |
| **`ngOnDestroy()`**        | Called before the component is destroyed                  | Cleanup logic, unsubscribe from observables           |

---

### Key Points:
- **`ngOnInit()`** is the most commonly used lifecycle hook for initialization logic.
- **`ngOnDestroy()`** is important for cleaning up resources such as unsubscribing from observables to avoid memory leaks.
- **`ngOnChanges()`** is invoked when Angular detects changes in the `@Input()` properties of a component.
- Angular automatically calls these lifecycle hooks during the component's lifecycle.

---

### 5 Interview Questions on Lifecycle Hooks:

1. **What is the purpose of the `ngOnInit()` hook in Angular?**
   - **Answer**: `ngOnInit()` is called once after the first `ngOnChanges()` and is used for initialization tasks such as fetching data or setting up properties.

2. **What is the difference between `ngOnChanges()` and `ngDoCheck()`?**
   - **Answer**: `ngOnChanges()` is called only when input properties change, while `ngDoCheck()` is called during every change detection cycle, allowing you to implement custom change detection logic.

3. **When would you use `ngOnDestroy()` in Angular?**
   - **Answer**: `ngOnDestroy()` is used for cleanup before the component is destroyed, such as unsubscribing from observables or detaching event listeners.

4. **What is the difference between `ngAfterViewInit()` and `ngAfterContentInit()`?**
   - **Answer**: `ngAfterViewInit()` is called after the component's view and its child views have been initialized, whereas `ngAfterContentInit()` is called after external content (projected via `<ng-content>`) has been projected into the component.

5. **Why is it important to unsubscribe from observables in `ngOnDestroy()`?**
   - **Answer**: Failing to unsubscribe from observables can lead to memory leaks because the observable will continue running even after the component is destroyed, holding references to the component in memory.
