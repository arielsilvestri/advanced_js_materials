##Determining Scope in terms of Compiler
- Summary: The JavaScript interpreter make two passes on a section of JavaScript code. The first pass processes variables and function declarations and lifts them to the top (the ‘hoisting’). The second pass processes the function expressions and undeclared variables. 

- The following code has two statements, not one:
```javascript
var foo = "bar";
```
- First, the variable is declared, `var foo`. Then it is initalized: `var foo = "bar"` 

- The compiler will go through and find declarations. It will define those declarations in the scope where it finds them. So, if the above code sample were just written without being inside a function, it would make a variable declaration in the global scope.

```javascript
function bar() {
  var foo = "baz";
}
```
- In the above code, the function `bar()` is declared in the global scope, and the variable `var foo` is declared in the scope of function `bar()`. As this is not an IIFE, the compiler will return to this function later to compile it. 

- When the compiler hits a different scope, such as moving from the global scope into a new function scope, it will recursively enter that scope and find declarations. Once it finishes in that scope, it will return to the global scope, repeating this process as necessary.

- A compiler will guess that what a function should do. It'll compile the function a few times until it makes the correct guess and compile the function.

```javascript
function baz(foo) {
  foo = "bam";
  bam = "yay";
}
```
- In this function scope, the first declaration is the parameter `foo`, within the scope of `baz`. There are no more declarations in this scope.

- In the execution phase, `var`'s are gone, as they are compiled in the declaration operation. Now we come to the initialization operation.

##LHS vs RHS
- LHS: The left-hand side of the assignment-in our case, the `=` sign.
- RHS: The right-hand side of the assignment.
```javascript
  var foo = "bar";
```
- Remember, var is gone at this phase, so the LHS is `foo` and the RHS is `bar`
The LHS is the target, and the RHS is the source. We put the RHS on its target, the LHS.