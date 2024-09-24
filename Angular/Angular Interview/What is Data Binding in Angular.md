### What is Data Binding in Angular?

**Data Binding** in Angular refers to the automatic synchronization between the data in the component class (model) and the user interface (view). Angular supports different types of data binding:

1. **Interpolation (String Interpolation)**: Displaying dynamic data from the component in the view.
2. **Property Binding**: Binding a property of a DOM element to a component property.
3. **Event Binding**: Binding an event in the view (such as a button click) to a method in the component.
4. **Two-way Data Binding**: A combination of property and event binding that keeps the model and the view in sync.

---

#### Types of Data Binding in Angular:

1. **Interpolation (String Interpolation)**

   Interpolation is used to display dynamic data from the component class inside the HTML.

   ```html
   <!-- Interpolation Example -->
   <p>Hello, {{ username }}!</p>
   ```

   ```typescript
   export class AppComponent {
     username = 'Angular User';
   }
   ```

2. **Property Binding**

   Property binding is used to bind an element's property to a component property.

   ```html
   <!-- Property Binding Example -->
   <img [src]="imageUrl" alt="Angular Logo" />
   ```

   ```typescript
   export class AppComponent {
     imageUrl = 'https://angular.io/assets/images/logos/angular/angular.svg';
   }
   ```

3. **Event Binding**

   Event binding is used to listen to DOM events and trigger component methods.

   ```html
   <!-- Event Binding Example -->
   <button (click)="handleClick()">Click Me</button>
   ```

   ```typescript
   export class AppComponent {
     handleClick() {
       console.log('Button clicked!');
     }
   }
   ```

4. **Two-way Data Binding**

   Two-way data binding combines property and event binding. It allows you to bind form inputs or other elements in the UI to a component property, so that changes in the UI are reflected in the component and vice versa.

   ```html
   <!-- Two-way Data Binding Example -->
   <input [(ngModel)]="name" />
   <p>Your name is: {{ name }}</p>
   ```

   ```typescript
   export class AppComponent {
     name = 'John';
   }
   ```

---

### Summary:
Data Binding in Angular helps establish a communication channel between the view and the model, making it easier to manage dynamic data in the UI.

---

### Key Points:
- **Interpolation**: Binds data from the component to the view.
- **Property Binding**: Binds a property of a DOM element to a component property.
- **Event Binding**: Binds DOM events to component methods.
- **Two-way Data Binding**: Synchronizes the view and the model.

---

### 5 Interview Questions on Data Binding:

1. **What is the difference between Property Binding and Interpolation?**
   - **Answer**: Interpolation only works for strings, while property binding works for all kinds of properties, including boolean and object properties.

2. **Can we use Two-way Data Binding without ngModel?**
   - **Answer**: No, `[(ngModel)]` directive is required for two-way data binding. Without it, you would have to manually bind both the property and the event.

3. **What happens if a model property in Two-way Binding is undefined?**
   - **Answer**: If the model is `undefined`, the view will not display any data, and the input field will be blank.

4. **How can you disable a button conditionally using Property Binding?**
   - **Answer**: You can bind the `disabled` property to a component variable.
   ```html
   <button [disabled]="isDisabled">Click Me</button>
   ```

5. **How is Event Binding different from Two-way Data Binding?**
   - **Answer**: Event binding only listens to and handles user actions (like clicks), while two-way binding also updates the model whenever the user interacts with the form controls or elements.
