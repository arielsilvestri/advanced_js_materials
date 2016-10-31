##`This` Keyword
- Every function, **while executing**, has a reference to its current execution context, called `this`.
- JavaScript's version of dynamic scoping is `this`.

```javascript
function foo() {
  console.log(this.bar);
}

var bar = "bar1";
var o2 = {bar: "bar2", foo: foo};
var o3 = {bar: "bar3", foo: foo};

foo(); //"bar1"
o2.foo(); //"bar2"
o3.foo(); //"bar3"
```
- Depending on the call site-the place in code where a function is executed-there are four rules for how `this` is bound. The above code covers the 3rd and 4th rules, in terms of priority: 
- **Implicit Binding:** `This` is assigned to its parent object if it has one that isn't the global object.
- **Default Binding:** If you are in strict mode, default the value of `this` to `undefined`. If you are not in strict mode, `this` is automatically bound to the global object.

##Explicit Binding 
```javascript
function foo() {
  console.log(this.bar);
}

var bar = "bar1";
var obj = {bar: "bar2"}

foo(); // "bar1"
foo.call(obj); // "bar2"
```
- This presents the second highest priority rule for `this`, referred to as explicit binding:
- **Explicit Binding:** If you use `.call()` or `.apply()` at the call site, both will take a `this` argument as their first parameter. If I pass in `obj` to `foo.call()`, it will operate as `obj.foo();`

##`new` Keyword
- The following is the highest-priority rule for assigning `this`: 
```javascript
function foo() {
  this.baz = "baz";
  console.log(this.bar + " " + baz);
}

var bar = "bar"
var baz = new foo(); // ???
```
- Four things occur when `new` is placed in front of a function call:
1. A brand-new empty object is created.
2. This new object gets linked to a different object.
3. This new object is bound to `this`.
4. If that function doesn't return anything, it will implicitly `return this` into its function call.

- The above code will print "undefined undefined", as there is no `this.bar` based on these rules, since `this` is `foo`. `Baz` doesn't exist anywhere, so it is also undefined.

## The Four Golden Questions of `this`
1. Was the function called with `new`? Use that object.
2. Was the function called with `call` or `apply` specifiy an explicit `this`? Use that object.
3. Was the function called via a containing/owning object (context)? Use that object.
4. Default to the global object.
