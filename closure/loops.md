##Loops
```javascript
for(var i = 1; i <= 5; i++){
  setTimeout(function(){
    console.log("i: " + i);
  }, i*1000);
}
```

- In the spirit of this exercise, we expect this loop to print out `i` and the second we are currently on, up until the fifth second. However, `i: 6` will print to the console 5 times instead.
- What's missing from this example that would make the loop work as intended? Why don't we have five different `i` values?
- These functions do not get a different `i` each time. Since they are closed over the same lexical scope, they use the same `i`.
- We can solve this problem using an IIFE!

```javascript
for(var i = 1; i <= 5; i++){
  (function(i){
    setTimeout(function(){
      console.log("i: " + i);
    }, i*1000);
    })(i);
}
```
- Using an IIFE, each loop gets its own `i`. Functions create scope, and a whole new scope will be created for each iteration thanks to an IIFE.

##ES6's `let`
```javascript
for (let i = 1; i<5; i++) {
  setTImeout(function() {
    console.log("i: " + i);
  }, i*1000);
}
```
- Using `let` inside of a loop, our `i` is not just bound to the `for` loop-it is bound to each iteration of the `for` loop as well.
- This means we'll have a brand-new `i` for each iteration, meaning that our `for` loop will work as originally intended, without the need for an IIFE.