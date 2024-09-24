### What are Pipes? What are the types of Pipes & Parameterized Pipes?

**Pipes** in Angular are used to transform the output displayed in the template. They take in data, process it, and return the transformed result, which is then displayed in the view. Pipes are typically used for formatting data such as strings, numbers, dates, or even custom formats.

---

#### Types of Pipes in Angular:

1. **Built-in Pipes**:
   Angular provides several built-in pipes for common data transformations.
   - **Examples**:
     - **DatePipe**: Formats date values.
     - **CurrencyPipe**: Formats numbers as currency.
     - **DecimalPipe**: Transforms numbers with decimal points.
     - **PercentPipe**: Formats numbers as percentages.
     - **UpperCasePipe**: Transforms strings to uppercase.
     - **LowerCasePipe**: Transforms strings to lowercase.
     - **SlicePipe**: Extracts a subset of an array or string.

   ```html
   <!-- Built-in Pipes Example -->
   <p>{{ today | date:'short' }}</p>  <!-- DatePipe Example -->
   <p>{{ price | currency:'USD' }}</p> <!-- CurrencyPipe Example -->
   ```

2. **Custom Pipes**:
   You can create custom pipes when the built-in pipes don’t meet your needs.
   - **Example**: Creating a pipe that reverses a string.
   ```typescript
   @Pipe({ name: 'reverse' })
   export class ReversePipe implements PipeTransform {
     transform(value: string): string {
       return value.split('').reverse().join('');
     }
   }
   ```

3. **Parameterized Pipes**:
   Pipes can accept parameters to further customize the transformation. For instance, you can specify how many decimal places a number should be rounded to, or how a date should be formatted.
   - **Examples**:
     - **DatePipe with parameters**: You can specify the format of the date.
     - **CurrencyPipe with parameters**: Specify the currency symbol and formatting.
     
     ```html
     <!-- Parameterized Pipe Example -->
     <p>{{ today | date:'fullDate' }}</p>  <!-- DatePipe with parameter -->
     <p>{{ price | currency:'USD':'symbol':'4.2-2' }}</p> <!-- CurrencyPipe with parameter -->
     ```

---

### How to Use Pipes:

- **Syntax**: Pipes are used in the template with the pipe symbol `|`.
- **Example**:
   ```html
   <p>{{ birthday | date:'longDate' }}</p>
   <p>{{ price | currency:'USD' }}</p>
   ```

---

### Summary:
- **Pipes** in Angular are useful for transforming and formatting data before displaying it in the view.
- **Built-in Pipes** include DatePipe, CurrencyPipe, DecimalPipe, etc.
- **Custom Pipes** can be created when you need custom transformations.
- **Parameterized Pipes** allow you to pass arguments to control how the data should be transformed.

---

### Key Points:
- Pipes are a simple way to transform data in the template.
- Built-in pipes cover common needs such as date, currency, and string transformations.
- Custom pipes can be developed for specific use cases.
- Parameterized pipes accept additional parameters to customize transformations.

---

### 5 Interview Questions on Pipes:

1. **What are Pipes in Angular, and how are they used?**
   - **Answer**: Pipes are functions that transform data before it is displayed in the template. They are used by placing a pipe (`|`) symbol in the template, followed by the pipe name and any parameters.

2. **How do you create a custom Pipe in Angular?**
   - **Answer**: You can create a custom pipe by using the `@Pipe` decorator and implementing the `PipeTransform` interface. The `transform` method defines the custom logic.
   ```typescript
   @Pipe({ name: 'reverse' })
   export class ReversePipe implements PipeTransform {
     transform(value: string): string {
       return value.split('').reverse().join('');
     }
   }
   ```

3. **What is the difference between a Built-in Pipe and a Custom Pipe?**
   - **Answer**: Built-in pipes are provided by Angular (e.g., DatePipe, CurrencyPipe), while custom pipes are user-defined for more specific transformations that built-in pipes do not cover.

4. **How do you pass parameters to a Pipe?**
   - **Answer**: You pass parameters to a pipe by following the pipe name with a colon (`:`) and the parameter. For example:
   ```html
   <p>{{ birthday | date:'shortDate' }}</p>
   ```

5. **Can Pipes be used for multiple transformations?**
   - **Answer**: Yes, you can chain pipes together to perform multiple transformations in sequence.
   ```html
   <p>{{ price | currency:'USD' | uppercase }}</p>  <!-- First CurrencyPipe, then UpperCasePipe -->
   ```
