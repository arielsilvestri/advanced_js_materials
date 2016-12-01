##Prototypes

- Every single `object` is built by a constructor function/call.
- Each time a constructor is called, a new object is created.
- A constructor makes an object linked to its own prototype.

```javascript
 1 function Foo(who) {
    this.me = who;
  }

4  Foo.prototype.identify = function() {
    return "I am " + this.me;
  }

8  var a1 = new Foo("a1");
9  var a2 = new Foo("a2");

11  a2.speak = function() {
    alert("Hello, " this.identify() + ".");
  }

15  a1.constructor === Foo;
16  a1.constructor === a2.constructor;
17  a1.__proto__ === Foo.prototype;
18  a1.__proto__ === a2.__proto__;
```
- Here is how the compiler inteprets this code:
- Before anything even happens, a function called `Object` is created. Linked to that function is an object with common JavaScript functions attached, and the link to that object is called `Object.prototype`.

1. Line 1 will create a function, `Foo`, and a link called `.prototype` to an object. 
The link here is a two-way one-the object has a link to `Foo` called `constructor`. That object is linked to `Object`'s object., and that link is referred to as `[[Prototype]]`
2. On Line 4, we add an `identify` function into the objected linked to `Foo`.
3. On Line 8, a brand new object is created. This object is linked to the object linked to `Foo`. The context-a1-is set to `this` and gets a `me` property. It then returns all of this and assigns it to the object `a1`.
4. On Line 9, the same exact thing that occurred on line 8 occurs.
5. On Line 11, we add a `speak` function to the `a2` object.
6. On Line 15, we ask if `a1` has a constructor property. Since `a1` does not have one, it will go up the prototype chain to find one. The linkages that `a1` and `a2` have to `Foo`'s object are referred to as `[[Prototype]]`. This will return true.
7. On Line 16, the same occurs as on Line 15.
8. On Line 17, we ask if `a1` has a dunder proto property. There is none, so it moves up the protoype chain to `Foo`'s object. There is none there, and it moves up the chain to `Object`'s object, which has one. Dunder proto is a getter function that will return the internal prototype linkage of whatever the `this` binding is. In other words, it returns what `this` is for a given object. Alternatively, we can use `Object.getPrototypeOf(a1)` to get `a1`'s internal prototype linkage to `this`. We return true.
9. On Line 18, the same happens as on Line 17.
