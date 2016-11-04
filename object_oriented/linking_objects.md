##Linking Objects
```javascript
function Foo(who) {
  this.me = who;
}

Foo.prototype.identify = function() {
  return "I am " + this.me;
}

function Bar(who) {
  Foo.call(this, who);
}

Bar.prototype = Object.create(Foo.prototype);

Bar.prototype.speak = function() {
  alert("Hello, " + this.identify() + ".");
};

var b1 = new Bar("b1");
var b2 = new Bar("b2");

b1.speak(); //alerts: "Hello, I am b1."
b2.speak(); //alerts: "Hello, I am b2."
```
- Here, `Foo` will represent a class. `Bar` represents a child class of `Foo`, and extends it.
- In order to accomplish classical Class design in JavaScript, we would need have Bar's prototype extend Foo's prototype, thus the need for the code: `Bar.prototype = Object.create(Foo.prototype);`
- Now we will have proper access to `Foo.prototype.identify`.
- `Object.create` will create a new object and link it to its constructor, thus accomplishing this faux Class design.
- When we call `b1.speak()`, `b1` will go up the prototype chain to `Bar` and find `speak()`. Within `speak()`, we have `this.identify()`. `b1` will go up the prototype chain to `Bar`, but won't find it. Thanks to our linkage, the next point in the chain is `Foo`, where we will find an `identify()` function.
- Using this method, we destroy `Bar.constructor` due to our use of `Object.create`. Calling `b1.constructor` will return `Foo`.