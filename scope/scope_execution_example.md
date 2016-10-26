```javascript
  var foo = "bar";

  function bar() {
    var foo = "bar";

    function baz(foo) {
      foo = "bam";
      bam = "yay";
    }
    baz();
  }

  bar();
  foo;
  bam;
  baz();
```

What happens:

Declaration:
-Hey Global Scope, I have a variable `foo` to declare.
-Hey Global Scope, I have a function `bar()` to declare.
-Hey Function Bar Scope, I have a variable `foo` to declare.
-Hey Function Bar Scope, I have a function `baz()` to declare.
-Hey Function Baz Scope, I have a parameter `foo` to declare.


Execution:
-Hey Global Scope, I have a LHS reference for a variable `foo`, heard of it? Response: Yes, here you go. Assign `foo` to `"bar"`
-Functions are compiled away.

**-Skips down to `bar();`**
-Hey Global Scope, I have an RHS reference for the function `bar();`, heard of it? Response: yes, here you go. Execute function `bar();`
-Hey Function Bar Scope, I have an LHS reference for variable `foo`, heard of it? Response: Yes, here you go. Referencing local `foo`, as it comes first in the scope of that function.
-Hey Function Bar Scope, I have an RHS reference for a variable called `baz();`, heard of it? Response: Yes, here you go. Execute function `baz();`
-Hey Function Baz Scope, I have an LHS reference for a variable `foo`, heard of it? Response: Yes, it is a parameter. Here you go. Assign `"bam"` to Function Baz Scope `foo`
-Hey Function Baz Scope, I have an LHS reference for `bam`, heard of it? Nope, moves to Function Bar Scope, heard of it? Nope, moves to Global Scope, heard of it? Yes, just made it for you since this is not in strict mode and is a global variable declaration!
**-Complete `bar();` execution.**

**-Execute `foo`**
-Hey Global Scope, I have an RHS reference for variable `foo`, heard of it? Yes, it is declared as `"bar"`, here you go.
**-Complete `foo` execution.**

**-Execute `bam`**
-Hey Global Scope, I have an RHS reference for variable `bam`, heard of it? Yes, because of our execution of `bar();`, `bam` is equal to `"yay"`. Here you go.
**-Complete `bam` execution.**

**-Execute `baz();`**
-Hey Global Scope, I have an RHS reference for `baz();`, heard of it? Nope. This will be a ReferenceError. 