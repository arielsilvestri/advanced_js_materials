## `Let` Keyword
- The `let` keyword binds a variable declaration to a specific scope. In essence, you hijack the current scope and bind the `let` declaration to that specific scope.

```javascript
function foo(bar) {
  if(bar){
    let baz = bar;
    if(baz) {
      let bam = baz;
    }
    console.log(bam); //Throws an Error. Only defined in the if(baz) scope.
  }

  console.log(baz); //Throws an error. Only defined in the if(bar) scope.
}

foo("bar");
```
## Pitfalls with `Let`

- The `let` keyword does not hoist variables. Unlike `var`, which will hoist, or move, a variable declaration to the top of a block, you will have to declare your `let` statements at the beginning of their associated block.
- Thus, we'll need to think more carefully about where we begin and end new blocks for proper scoping.
- As this is implicit block scoping, it is harder to maintain our block scope given how `let` will hijack the current scope and create a new, smaller scope to bind a declaration to.


