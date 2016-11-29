## Callbacks
- Callbacks are functions that don't immediately return some value. Typically loading photos, files, etc.-things that take time to find and load-are done so via callbacks.
- Callback hell occurs when we nest callbacks inside of callbacks. Code starts to get messy and difficult to read!
- Inversion of control occurs when we utilize third-party resources to hand off and resolve our callbacks. We are giving another party control of our information without knowing for sure if everything works properly!

## Generators (ES6 only)
- In JS, we assume as soon as a function starts executing, it will finish executing the entirety of that function before moving along.
- This holds true of all functions except for Generators, introduced in ES6.

```javascript
  function* gen() {
    console.log("Hello");
    yield null;
    console.log("World");
  }

var it = gen();
it.next(); //prints "Hello"
it.next(); //prints "World"
```
- With `yield`, when we call the generator function, we receive an iterator as a return.
- By calling `next()`, we step through the function until we hit the next `yield`, or the end of the function.
- Once we get to this point, a generator will pause itself unless it has reached the end of the function, and will continue once we call `next()`.
- With `yield`, we can pass messages into our generator and receive messages back.

```javascript
var run = coroutine(function*(){
  var x = 1 + (yield null);
  var y = 1 + (yield null);
  yield (x + y)
});

run();
run(10);
console.log(
  "Meaning of life: " + run(30).value
);
```
- When we pass a value into run, that value will take the place of the first `yield null` that it finds. The function then pauses once it resolves that `yield null` and hits another `yield null`
- So, `run(10)` will set a `x` equal to 11. Then, `run(30)` will set `y` equal to 31. Finally, by calling `.value`, we will receive the result of `(x + y)`, which is 42.

- The following generator hides its asynchronousty behind syntax that appears and reads as synchronous, making the code easy to read, follow, and understand:

```javascript
function getData(d){
  setTimeout(function(){run(d);}, 1000);

  var run = coroutine(function*(){
    var x = 1 + (yield(getData(10));
    var y = 1 + (yield(getData(30));
    var answer = (yield getData(
      "Meaning of life: " + (x+y)
    ));
    console.log(answer); //Meaning of life: 42
  })

run();
}
``` 