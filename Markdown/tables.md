

In Markdown, tables are created using pipes (`|`) and dashes (`-`) to define rows and columns. Here's the syntax:

### Basic Markdown Table Syntax

```markdown
| Column 1 Header | Column 2 Header | Column 3 Header |
|------------------|-----------------|-----------------|
| Row 1 Col 1     | Row 1 Col 2     | Row 1 Col 3     |
| Row 2 Col 1     | Row 2 Col 2     | Row 2 Col 3     |
| Row 3 Col 1     | Row 3 Col 2     | Row 3 Col 3     |
```

### Rendered Output:

| Column 1 Header | Column 2 Header | Column 3 Header |
|------------------|-----------------|-----------------|
| Row 1 Col 1     | Row 1 Col 2     | Row 1 Col 3     |
| Row 2 Col 1     | Row 2 Col 2     | Row 2 Col 3     |
| Row 3 Col 1     | Row 3 Col 2     | Row 3 Col 3     |

---

### Key Points:
1. **Headers**: 
   - The first row contains the headers for the table.
   - Headers are separated by `|`.
   
2. **Alignment**:
   - Use colons (`:`) in the separator row to define alignment:
     - `:---` aligns text to the left.
     - `:---:` centers text.
     - `---:` aligns text to the right.
     
   Example:

   ```markdown
   | Left Align  | Center Align | Right Align  |
   |:------------|:------------:|-------------:|
   | Left text   | Center text  | Right text   |
   | More text   | More text    | More text    |
   ```

   Rendered:

   | Left Align  | Center Align | Right Align  |
   |:------------|:------------:|-------------:|
   | Left text   | Center text  | Right text   |
   | More text   | More text    | More text    |

3. **Cell Content**:
   - You can leave cells blank, and you don’t have to align pipes (`|`) perfectly.
   - Extra spaces in the markdown do not affect rendering.

4. **Nested Markdown**: 
   - Text in table cells can include other Markdown elements like **bold**, *italic*, or `code`.

### Example with Formatting:

```markdown
| **Feature**       | *Description*                      | `Code Example` |
|--------------------|------------------------------------|----------------|
| **Bold Text**      | Text styled in bold.              | `**Bold**`     |
| *Italic Text*      | Text styled in italic.            | `*Italic*`     |
| Inline `code`      | Code inline with text.            | `` `Code` ``   |
```

### Rendered:

| **Feature**       | *Description*                      | `Code Example` |
|--------------------|------------------------------------|----------------|
| **Bold Text**      | Text styled in bold.              | `**Bold**`     |
| *Italic Text*      | Text styled in italic.            | `*Italic*`     |
| Inline `code`      | Code inline with text.            | `` `Code` ``   |

---

Markdown tables are straightforward, and with practice, you can create clean and organized tabular data presentations!
