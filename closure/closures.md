##Closures
```javascript
function foo() {
  var bar = "bar";

  function baz() {
    console.log(bar);
  }

  bam(baz);
}

function bam(baz) {
  baz(); // "bar"
}

foo();
```

- Closure is when a function "remembers" its lexical scope even when the function is exectued outside that lexical scope.

```javascript
function foo() {
  var bar = "bar";

  return function() {
    console.log(bar);
  };
}

function bam() {
  foo()(); // "bar"
}

bam();
```
- You can return an inner anonymous function to execute a closure.

```javascript
function foo() {
  var bar = "bar";

  setTimeout(function(){
    console.log(bar);
  }, 1000);
}

foo();
```
- Closures are commonly utilized with callback functions such as `setTimeout`.

```javascript
function foo() {
  var bar = "bar";

  $("#btn").click(function(event) {
    console.log(bar);
  });
}

foo();
```
- Click-handlers are another common example of closure usage.

```javascript
function foo() {
  var bar = 0;
  setTimeout(function(){
    console.log(bar++);
  }, 100);
  setTimeout(function(){
    console.log(bar++);
  }, 200);
}

foo(); // 0 1
```
- If two functions have closure over the same lexical scope, they will update the same variable in the example above.

```javascript
function foo() {
  var bar = 0;
  setTimeout(function(){
    var baz = 1;
    console.log(bar++);

    setTimeout(function(){
      console.log(bar + baz);
    }, 200);
  }, 100);
}
foo(); // 0, 2
```
- Even when our functions become nested, they will maintain the same closure around their lexical scope, thus producing "2" as a response.