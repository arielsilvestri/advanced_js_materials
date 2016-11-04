##Prototype Linkages

```javascript
function Foo(who) {
  this.me = who;
}

Foo.prototype.identify = funciton() {
  return "I am" + this.me;
}

var a1 = new Foo("a1");
a1.identify(); // "I am a1"

a1.identify = function() { // <-- Shadowing
  alert("Hello, " + Foo.prototype.identify.call(this) + ".")
}

a1.identify(); // alerts: "Hello, I am a1."
```
- When we call `a1.identify` the first time, we will move up the protoype chain to find `Foo.prototype.identify`, as it does not exist on `a1`.
- When we add an `identify` method to `a1`, we aren't changing `Foo.prototype.identify`, but just adding it to `a1`. Now when we call `a1.identify`, we call the identify found on `a1`. This is referred to as shadowing, because it will always find `a1.identify` whenever we call identify on `a1` now.
- Because of shadowing, we need to utilize `call(this)` in order to get back to the original instance of `identify` found on `Foo`.
- If we called our new `identify` anything but `identify`, we could say `this.identify()` rather than `Foo.prototype.identify.call(this)`. 