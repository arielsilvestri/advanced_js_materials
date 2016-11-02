##Classic Module Pattern

```javascript
var foo = (function(){
  var o = {bar: "bar"}
  return {
    bar: function(){
      console.log(o.bar);
    }
  };
})();

foo.bar(); // "bar"
```
- There are two required characteristics of this pattern:
1. There must be an outer-enclosing function that gets executed, such as an IIFE.
2. There must be one or more inner functions that are returned from the function call that have a closure over the inner private scope/internal state.
- This is the idea of encapsulation, from the principle of least privelage, or the principle of least exposure.
- This design has a shortcomming-there is no way for me to access the property `bar` on the object `o`. While this may be intended, this restricts my API from things such as CRUD functionality.

##Modified Module Pattern
```javascript
var foo = (function(){
  var publicAPI = {
    bar: function() {
      publicAPI.baz();
    },
    baz: function(){
      console.log("baz")
    }
  };
  return publicAPI;
})();

foo.bar(); //"baz"
```
- Fixing part of the problem with the classic pattern, utilizing this pattern, we can update our publicAPI at runtime, such as adding or removing information, because both `foo` and `publicAPI` reference the same object.

# ES6+ Module Pattern
```javascript
var o = {bar: "bar"}
export function bar() {
  return o.bar;
}
```
- Heavily utilized in React.
- A file-based pattern, each file will act as a module which you can `export`.

```javascript
  import { bar } from "foo";
  bar(); // "bar"
```

- In conjunction with `import`, we can pull in specific parts of a file as a module.