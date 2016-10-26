##Function Declaration vs. Expression
```javascript
  var foo = function bar() {
    var foo = "baz";

    function baz(foo) {
      foo = bar;
      foo;
    }

    baz();
  };

  foo();
  bar();
```
- A function declaration occurs when the `function` keyword is the first thing in the statement. 
- In this example, this is a function expression, as `function` is not the first thing in the statement. Typically you see these as `anonymous functions`. In this example it is named, `bar()`, but it is not declared in the global scope, but rather in its own scope. Therefore, the line where we call `bar()` will throw an error, as there is no `bar()` RHS reference for it declared in the global scope.

Why do we name our functions? Anon functions have three major negatives:
- Anon functions cannot refer to themselves inside of themselves. Thus, recursion is impossible.
- Anon functions create unreadible error messages, particularly when reading from minified code.
- Anon functions require you to look around the code in order to understand what it is doing.

The line `foo()` will execute the function as written, once it is compiled.

##Block Scope
```javascript
  var foo;

  try {
    foo.length
  }
  catch (err) {
    console.log(err); //TypeError
  }

  console.log(err); //ReferenceError
``` 

- This is an example of `Block Scope`. The variable in your `catch` clause, `err`, is only defined in the `catch` block. Therefore, calling it on the final line raises a ReferenceError.