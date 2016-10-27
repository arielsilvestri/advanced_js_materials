##Lexical Scope
- Lexical Scope refers to the parsing stage that occurs when the compiler compiles your code. It is compile-time scope.
- Imagine it like a building. Start at the bottom of the building, and work your way all the way to the metaphorical top. See the following code example:

```javascript
function foo() {
  var bar = "bar";
  function baz() {
    console.log(bar); //lexical!
  }
  baz();
}
foo();
```
- There is a bubble around the scope of `baz()`. Consider this our first floor.
- There is a bubble around the scope of `foo()`, which is our next level.
- There is a bubble around the global scope, or our top floor.

- Since our code is written this way, the compiler knows exactly the way the scope is defined-it knows the layout of the building-and is ready to execute it as necessary. This is known as an author-time decision.

##Cheating Lexical Scope
###`eval()`

```javascript
var bar = "bar";

function foo(str) {
  eval(str); //cheating!
  console.log(bar); //42
}

foo("var bar=42;")
```
- The `eval()` keyword allows us to cheat lexical scope. It will take any input strings into our function calls and treats them as if they existed as code during compilation.
- At compile time, there is no variable `bar` in the scope of `foo()`, so the `console.log` would print `"bar"`. However, since we passed the string into `foo()`, we now cheat that var into the function, thus modifying the lexical scope of function `foo()`.
- Anytime JS sees `eval()`, it slows down your code at runtime.
- `Strict mode` will create a new scope for the `eval()` call which prevents slow downs.
- Avoid using `eval()` as much as possible. Use it when writing a templating engine.

###`with()`
```javascript
var obj = {
  a: 2,
  b: 3,
  c: 4
}

obj.a = obj.b + obj.c;
obj.c = obj.b - obj.a;

with(obj) {
  a = b + c;
  c = b - a;
  d = 3; //??
}

obj.d; //undefined
d; //3 -- Bad!
```

- Using the `with()` block is a shorthand way to reference the properties of an object in JS.
- The `with()` statement creates a lexical scope. Meaning on line 13, `d` will be seen as a declaration since it is not on the object that is passed in. What happens?
- Hey Scope of With, I have an LHS for d, heard of it? Nope, go to the global scope, which will create it and set it equal to 3.
- We've now made a global variable with a value of 3.
- Where `eval()` modifies the existing lexical scope at runtime, `with()` makes a whole new lexical scope. Slows down code even worse than `eval()` `Strict mode` completely turns off `with()`