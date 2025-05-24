<iframe width="560" height="315" src="https://www.youtube.com/embed/EvfRXyKa_GI" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

**Hoisting** is a JavaScript mechanism in which **variable declarations** (using `var`, `let`, `const`) and **function declarations** are moved to the top of their containing scope during the compile phase, before the code execution begins. However, only the **declarations** are hoisted, not the **initializations**.

### Key Concepts of Hoisting:

1. **Hoisting of Variable Declarations**:
    
    - In JavaScript, **variable declarations** (but not initializations) are hoisted to the top of their scope.
        
    - If you try to use a variable before declaring it, JavaScript will _hoist_ the declaration but not the initialization, leading to different behavior depending on the variable declaration method (`var`, `let`, `const`).
        
2. **Hoisting of Function Declarations**:
    
    - Function declarations are also hoisted. This means you can invoke a function before it’s declared in your code.
        
3. **Hoisting with `var`**:
    
    - Variables declared using `var` are hoisted to the top of the function or global scope, but they are initialized with **`undefined`**. This can sometimes lead to unexpected behavior.
        
4. **Hoisting with `let` and `const`**:
    
    - **`let`** and **`const`** declarations are also hoisted to the top of their block scope, but they are not initialized. Accessing them before their declaration results in a **ReferenceError** due to the **temporal dead zone** (TDZ).
        
5. **Hoisting and Execution Context**:
    
    - Hoisting occurs during the **compilation phase**, which happens before the code is actually executed. JavaScript allocates memory for variables and functions, and only the **declarations** are hoisted.
        

---

### Hoisting with `var`:

When you declare a variable using `var`, only the declaration is hoisted to the top of its scope. The assignment or initialization remains in its original position.

#### Example 1: Hoisting with `var`:

```javascript
console.log(myVar); // Output: undefined
var myVar = 5;
console.log(myVar); // Output: 5
```

#### Explanation:

- The `var myVar = 5;` statement is treated as if it were split into two parts:
    
    1. `var myVar;` (hoisted to the top, initialized to `undefined`)
        
    2. `myVar = 5;` (executed where it is written in the code)
        
- Therefore, when you log `myVar` before it’s initialized, it outputs `undefined`. Only after the assignment does it become `5`.
    

---

### Hoisting with `let` and `const`:

Both `let` and `const` are hoisted to the top of their block scope, but they are not initialized. Accessing these variables before the declaration will throw a **ReferenceError** because they are in a "temporal dead zone" (TDZ) between the start of the block and the actual declaration.

#### Example 2: Hoisting with `let`:

```javascript
console.log(myVar); // ReferenceError: Cannot access 'myVar' before initialization
let myVar = 5;
```

#### Example 3: Hoisting with `const`:

```javascript
console.log(myConst); // ReferenceError: Cannot access 'myConst' before initialization
const myConst = 10;
```

#### Explanation:

- `let` and `const` are hoisted like `var`, but they are not initialized until their declaration is encountered in the code. Attempting to access them before their declaration results in a **ReferenceError** due to the temporal dead zone (TDZ).
    

---

### Hoisting with Function Declarations:

Function declarations are hoisted with both their **definition** and **body**, which means you can call a function before it is declared in your code.

#### Example 4: Hoisting with Function Declarations:

```javascript
myFunction(); // Output: "Hello, world!"

function myFunction() {
  console.log("Hello, world!");
}
```

#### Explanation:

- In this case, the function declaration is hoisted to the top of the scope, so the function can be called before it’s defined in the code.
    

---

### Function Expressions and Hoisting:

Unlike function declarations, **function expressions** are not hoisted in the same way. If you declare a function as part of a variable (using `var`, `let`, or `const`), only the variable declaration is hoisted, not the function definition.

#### Example 5: Hoisting with Function Expressions:

```javascript
myFunction(); // TypeError: myFunction is not a function

var myFunction = function() {
  console.log("Hello, world!");
};
```

#### Explanation:

- The variable `myFunction` is hoisted, but it is initially set to `undefined`. Therefore, when you try to call `myFunction()` before it is assigned the function, you get a `TypeError` because `undefined` is not callable.
    

---

### Hoisting Behavior Summary:

1. **Variables declared with `var`**:
    
    - The declaration is hoisted to the top, but the assignment happens at the original position in the code. The variable is initially set to `undefined`.
        
2. **Variables declared with `let` and `const`**:
    
    - The declaration is hoisted to the top of the block, but they are **not initialized**. They are in the **temporal dead zone** (TDZ) until the code execution reaches the actual declaration.
        
3. **Function declarations**:
    
    - The entire function definition (including the body) is hoisted, so you can call the function before it appears in the code.
        
4. **Function expressions**:
    
    - Function expressions (assigned to variables) are hoisted only with their variable declaration, not the function body. If you try to call the function before its definition, you will encounter an error.
        

---

### Conclusion:

**Hoisting** in JavaScript refers to the behavior where variable and function declarations are moved to the top of their respective scopes during the **compilation phase**, before the code is executed. While this behavior is mostly intuitive for function declarations, it behaves differently for `var`, `let`, and `const`. Understanding hoisting is crucial to avoid unexpected results in your code, especially when dealing with variable declarations and function expressions

## Resource
- [W3Schools - Hoisting](https://www.w3schools.com/js/js_hoisting.asp)