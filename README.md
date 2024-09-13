# frappe-app-documentation

In Frappe, **Display Dependency** is used to conditionally show or hide fields based on the value of other fields. You can control the visibility of fields by evaluating conditions using JavaScript expressions. Below is a list of common display dependency expressions and examples of how you can use them:

### Common Display Dependency Expressions:

1. **Equality Check** (`==`)
   - Show a field when another field matches a specific value.
   - Example: 
     ```javascript
     eval:doc.status == "Approved"
     ```
   - This will display the field if `status` is equal to "Approved."

2. **Inequality Check** (`!=`)
   - Show a field when another field does **not** match a specific value.
   - Example:
     ```javascript
     eval:doc.status != "Rejected"
     ```
   - This will display the field if `status` is anything other than "Rejected."

3. **Checking Multiple Values** (with `||` or `&&`)
   - Combine conditions to show the field if **any** or **all** of the conditions are met.
   - Example with OR (`||`):
     ```javascript
     eval:doc.payment_status == "Paid" || doc.payment_status == "Pending"
     ```
   - Example with AND (`&&`):
     ```javascript
     eval:doc.status == "Approved" && doc.payment_status == "Paid"
     ```
   - The field will be displayed only if both conditions are true.

4. **Check if Field is Set** (i.e., non-empty values)
   - Show a field only if another field has a value (is not empty or null).
   - Example:
     ```javascript
     eval:doc.customer_name
     ```
   - The field will be displayed if `customer_name` is not empty.

5. **Check if Field is Empty**
   - Show a field only if another field is empty.
   - Example:
     ```javascript
     eval:!doc.customer_name
     ```
   - The field will be displayed if `customer_name` is empty.

6. **Check if Field Contains a Specific Pattern (Regex)**
   - Use JavaScript's `match()` function to match patterns in strings.
   - Example:
     ```javascript
     eval:doc.email && doc.email.match(/@example\.com$/)
     ```
   - This will display the field only if `email` ends with "@example.com."

7. **Greater Than / Less Than**
   - Show a field if a numerical field is greater than or less than a certain value.
   - Example:
     ```javascript
     eval:doc.total_amount > 1000
     ```
   - The field will be displayed if `total_amount` is greater than 1000.

8. **Boolean Check**
   - Show a field based on the value of a boolean field (checkbox or switch).
   - Example:
     ```javascript
     eval:doc.is_active == 1
     ```
   - The field will be displayed if `is_active` is checked (set to 1).

9. **Check for Date or Time Comparisons**
   - Show a field based on date or time comparisons.
   - Example:
     ```javascript
     eval: new Date(doc.due_date) < new Date()
     ```
   - This will display the field if `due_date` is before the current date.

### How to Set Display Dependency in Frappe:

1. Go to the Doctype where you want to set the display dependency.
2. Edit the field for which you want to set the condition.
3. In the field properties, look for the **"Depends On"** section.
4. Set your condition using the `eval:` prefix followed by a JavaScript expression (e.g., `eval:doc.fieldname == "value"`).

### Example of Complex Condition:
```javascript
eval:doc.status == "Approved" && doc.payment_status == "Paid" && doc.total_amount > 1000
```
This will display the field only if `status` is "Approved", `payment_status` is "Paid", and `total_amount` is greater than 1000.

### Key Operators to Use in Display Dependency:
- `==` : Equals
- `!=` : Not equals
- `&&` : Logical AND
- `||` : Logical OR
- `>` : Greater than
- `<` : Less than
- `>=` : Greater than or equal to
- `<=` : Less than or equal to
- `!` : Negation (used to check if a field is empty)

You can combine these operators to create custom conditions for controlling field visibility dynamically.
