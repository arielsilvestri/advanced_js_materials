##Hoisting
```javascript
a; // ???
b; // ???
var a = b;
var b = 2;
b; // 2
a; // ???
```
- This doesn't exist in the JS specs. We came up with it to understand how the compiler processes `var`.
- The compiler is not going to execute these lines in order. Remember, we have two run-throughs. The first run-through will find variable and function declarations and move them to the top, or hoist them. So, the code really looks like this after the first run through. Our LHS are processed in this phase:

```javascript
var a;
var b;
a; // Undefined -> a has no value assigned to it yet.
b; // Undefined -> b has no value assigned to it yet
a = b;
b = 2;
b; // 2
a; // Undefined -> a was assigned to b when b still did not have a value assigned to it. Thus, a remained undefined.
```

- During the second run-through, our RHS will be processed.
- This goes for functions as well:

```javascript
var a = b();
var c = d();
a; // ???
c; // ???

function b() {
  return c;
}

var d = function() {
  return b();
}

//Becomes...

function b() {
  return c;
}
var a;
var c;
var d;
a = b();
c = d();
a; // ???
c; // ???
d = function() {
  return b();
};
```
- Functions are hoisted first, then variables.
- The above code will error out, as on our second run through, `c=d()` will throw an error since our `d` function is an expression and its entire value was not hoisted.
- What happens when we have two functions with the same name?

```javascript
  foo(); // "foo"
  var foo = 2;

  function foo() {
    console.log("bar");
  }

  function foo() {
    console.log("foo")
  }
```

- Since both of the function declarations are hoisted to the top, the most recent declaration will be utilized via the flow of the compiler. 
- Don't re-declare stuff. Bad code smells.

- Function declarations implies that the values associated with it comes along, whereas with expressions, the value associated with `var` is left behind to be executable code.

##Mutual Recursion
- This occurs when two or more functions call one another inside their functions.
- Without hoisting, mutual recursion could not occur. 

```javascript
a(1); // ???

function a(foo) {
  if(foo > 20) return foo;
  return b(foo+2);
}

function b(foo){
  return c(foo) + 1;
}

function c(foo){
  return a(foo*2);
}
```
- Without hoisitng, one of these would always be called too late. Thus, mutual conversion isn't possible in an intepreted language.
