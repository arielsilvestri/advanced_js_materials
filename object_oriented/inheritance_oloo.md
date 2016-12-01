## Prototypal Inheritance

- The inverse of classical inheritance. In classical inhertiance, objects that inherit from the parent class are "copy downs" of the parent class-the public code of a parent class will find its way down to the child classes.
- Prototypal inheritance works the opposite way: child classes will look up the prototype chain to parent classes for code, rather than the code being copied down into the child classes.
- It is more appropriate to refer to Prototypal Inhertiance as Behavior Delegation.

## OLOO: Objects Linked to Other Objects
- One way of looking at Behavior Delegation and how it works.
- Drawing on a previous example where `Bar` extended `Foo`, here is how we delegate `Bar` to `Foo` and create an OLOO.

```javascript
var Foo = {
  init: function(who){
    this.me = who;
  },
  identify: function() {
    return "I am " + this.me;
  }
};

var Bar = Object.create(Foo);

Bar.speak = function() {
  alert("Hello, " + this.identify() + ".");
};

var bi = Object.create(Bar);
b1.init("b1");
b1.speak // alerts: "Hello, I am b1."
```
- Both `Foo` and `Bar` are objects with methods on them. `b1` is just an object that is linked to `Bar`, which is linked to `Foo`. Thus, we have Prototypal Inheritance, aka Behavior Delegation, with easy-to-read syntax that is decoupled from class design.
