## Promises
- Imagine ordering food at a fast-food restaurant. You order food, you hand your cashier money. Rather than immediately getting food, you get a receipt and stand aside so other people can order.
- Once your order number is called, you exchange your receipt for your food.
- This action was completed asynchronously, and the cashier returned a promise-the receipt-that will eventually give me my desired end result-my food.

```javascript
var wait = jQuery.Deferred();
var p = wait.promise();

p.done(function(value){
  console.log(value);
})

setTimeout(function(){
  wait.resolve(Math.random());
}, 1000);
```

- The above is a jQuery-style promise. We defer an object and create a promise. Later on, we instruct our promise to resolve and console log its value. At the end, we create a setTimeout that will resolve our deferred object after a second, passing in a random numerical value.

- Here's an example that shows how we can chain promises together:

```javascript
function waitForN(n) {
  var d = $.Deferred();
  setTimeout(d.resolve, n);
  return d.promise();
}

waitForN(1000)
.then(function(){
  console.log("Hello World");
  return waitForN(2000);
})
.then(function(){
  console.log("finally!")
});
```

- And here is the ES6 implementation of chained promises, utilizing the `Promise` constructor.

```javascript
function getData(d){
  return new Promise(function(resolve, reject){
    setTimeout(function(){ resolve(d), 1000} )
  })
}

var x;

getData(10)
.then(function(num1){
  x = 1 + num1;
  return getData(30);
})
.then(function(num2){
  var y = 1 + num2;
  return getData("Meaning of life: " + (x + y));
})
.then(function(answer){
  console.log(answer);
  //Meaning of life: 42
})
```
- Synchronously written, Asynchronously executed.