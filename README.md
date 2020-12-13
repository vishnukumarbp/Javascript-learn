# Javascript-learn
Self learning of Javascript in depth

#### Definition: Javascript (JS)

It is a Interpreted or JIT compiled Programming Language with first class function (function treated as variable). Also known as scripting language for web pages. Also used in non-browser environment like node.js, apache couchDB and Adobe Acrobat. JS is prototype-based, dynamic language.

Protoype-based: is a style of Object Oriented programming in which classes are not explicitly defined, but rather dervied by adding properties and methods to instance of another object or to an empty object.

### Prototype:

As stated, Javascript is prototype based programming. When a function is created in JavaScript, JavaScript engine adds a *prototype* property to the function. This prototype property is an object, and it has has a constructor property by default. constructor property points back to the function on which prototype object is alive. We can access the function’s prototype property using the syntax functionName.prototype. 

```javascript
function f1() {
  let name = "javascript";
  return 1;
 }
 ```
 
 *Test it in console*
 
 ```javascript
 typeof f1
"function"

 typeof f1.prototype
"object"
```
Looks fine. As said, *f1* is a function. and protoype of f1 is derived from object. so its type is "object".

*Inspecting more*

```javascript
f1.prototype
>{constructor: ƒ}
  >constructor: ƒ f1()
  >__proto__: Object
```


### Not Every Object is a function and every function is Object [refer](https://stackoverflow.com/questions/3449596/every-object-is-a-function-and-every-function-is-object-which-is-correct)


- Most of the non-primitive type has prototype property where all inherited stuff lives. Math doesn't have prototype.

- All `objects` inherit from `Object.prototype` which inherits from null.
`object` <- `Object.prototype` <- `null`

- All native functions inherit from `Function.prototype` which inherits from `Object.prototype`.
`function` <- `Function.prototype` <- `Object.prototype` <- `null`

- Arrays inherit from `Array.prototype` which inherits from `Object.prototype`.
`array` <- `Array.prototype` <- `Object.prototype` <- `null`



Notes:

[Global object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects) - The term "global objects" (or standard built-in objects) here is not to be confused with the global object. Here, "global objects" refer to objects in the global scope.

Object.keys are not a prototype method of Object type.


### Traditional way of wring a class like structure (Constructor Function) vs ES6 Class keyword:

Points to note from the article (attached below):

- body of a function act as constructure in traditional way. 
- to call parent construcutor (i.e super in ES6), we have to pass reference to parent construcutor (using .call)
- and to inherit (extend) we need to use Object.create and assign it to child prototype. This is way, we are manually creating the prototype chain between parent and child.
- use `new` keyword to create instance of the Constructor Function or Class

https://medium.com/@apalshah/javascript-class-difference-between-es5-and-es6-classes-a37b6c90c7f8



## Nullish coalescing operator '??'
?? returns the first argument if it’s not null/undefined. Otherwise, the second one.

#### || vs ??

|| doesn’t distinguish between false, 0, an empty string "" and null/undefined. They are all the same – falsy values. If any of these is the first argument of ||, then we’ll get the second argument as the result.

```javascript
let height = 0;

alert(height || 100); // 100
alert(height ?? 100); // 0
```


### When to choose Function Declaration versus Function Expression?
As a rule of thumb, when we need to declare a function, the first to consider is Function Declaration syntax. It gives more freedom in how to organize our code, because we can call such functions before they are declared.

That’s also better for readability, as it’s easier to look up function f(…) {…} in the code than let f = function(…) {…};. Function Declarations are more “eye-catching”.

…But if a Function Declaration does not suit us for some reason, or we need a conditional declaration (we’ve just seen an example), then Function Expression should be used.


## Testing with mocha
https://javascript.info/testing-mocha

```HTML
<!DOCTYPE html>
<html>
<head>
  <!-- add mocha css, to show results -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/mocha/3.2.0/mocha.css">
  <!-- add mocha framework code -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/mocha/3.2.0/mocha.js"></script>
  <script>
    mocha.setup('bdd'); // minimal setup
  </script>
  <!-- add chai -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/chai/3.5.0/chai.js"></script>
  <script>
    // chai has a lot of stuff, let's make assert global
    let assert = chai.assert;
  </script>
</head>

<body>

  <script>
    function pow(x, n) {
      /* function code is to be written, empty now */
    }
  </script>

  <!-- the script with tests (describe, it...) -->
  <script src="test.js"></script>

  <!-- the element with id="mocha" will contain test results -->
  <div id="mocha"></div>

  <!-- run tests! -->
  <script>
    mocha.run();
  </script>
</body>

</html>
```
