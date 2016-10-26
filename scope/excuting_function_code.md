##Executing Function Code
When the compiler hits a new function, it will enter that scope and execute the code inside the function. 
```javascript
function bar() {
  var foo = "baz";
}
```
The compiler will ask if the scope of `bar()` has an LHS reference for `"baz"`, which it will respond with yes because it was declared during the declaration operation.

```javascript
function baz(foo) {
  foo = "bam";
  bam = "yay";
}
```
In our function declaration, our compiler will ask if it has heard of the parameter 'foo', and it will respond yes. However, on the next line, when we ask the compiler if it has an LHS for `"bam"` in the function scope, the answer is no. Now, the compiler goes into the global scope to find it. The global scope is the final scope where the compiler looks.

In essence, we have declared a variable in the global scope while inside a function scope. In `strict mode`, the compiler will throw an error instead of defining the variable in the global scope.

The same is true for the LHS of '"yay"' in this function.

