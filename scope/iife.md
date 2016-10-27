##Immediately Invoked Function Expression (IIFE) Pattern
```javascript
var foo = "foo";
(function(){
  var foo = "foo2";
  console.log(foo); //"foo2"
})();

console.log(foo); // "foo"
```

- An IIFE prevents pollution of the current scope.
- Wrap the entire function in a parenthesis so it makes it a function expression instead of a declaration-`function` isn't the first thing in the statement, thus an expression!
- After we complete our function expression, immediately call, or invoke it, with a set of `()` braces.
- The second `var foo` is declared within this IIFE scope, preventing polliution of the global scope, where the first `var foo` is declared.
- Utilizing an IIFE is a good security measure and a method of privatizing certain bits of code. Utilize a public function that calls all these IIFE's, which would be hidden from the current user.
- Better to name your IIFE.
- You can pass values into an IIFE!

```javascript
var foo = "foo";
(function(bar){
  var foo = bar;
  console.log(foo); //"foo"
})(foo);

console.log(foo); // "foo"
```

- Handy for having a user pass information in in order to do something with their input.