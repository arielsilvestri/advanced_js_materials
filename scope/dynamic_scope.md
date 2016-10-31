##Dynamic Scope
- Theoretical example:

```javascript
function foo() {
  console.log(bar); //dynamic!
}

function baz() {
  var bar = "bar";
  foo();
}

baz();
```
- In `foo()`, bar doesn't exist in the lexical scope. However, since `foo()` isn't called outside of `baz()`, the compiler will look for where it is called in the call stack. It's called in `baz()`, which has a reference to `bar`, thus it works!