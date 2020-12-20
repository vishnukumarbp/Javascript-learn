# Javascript-learn
Self learning of Javascript in depth - Note: Topics are randomly placed. And it is purely for self reference

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
Note: instance of Object has no `.prototype` property. instead it has `__proto__`

## The Object Prototype (__proto__ or [[Prototype]])
This object doesn’t have a prototype, right?
`let obj = {};`
Try running this in your browser’s console:
```javascript
let obj = {};
console.log(obj.__proto__); // Play with it!
```
Surprisingly, `obj.__proto__` is not null or undefined! Instead, you’ll see a curious object with a bunch of properties, including hasOwnProperty.
We’re going to call that special object the Object Prototype.

<img src="https://user-images.githubusercontent.com/10495294/102712143-b4e7d100-42e4-11eb-87e5-4b1482178283.png" height="400" width="550" alt="Object prototype" />

### An Object with No Prototype

```javascript
let weirdo = {
  __proto__: null
};

console.log(weirdo.hasOwnProperty); // undefined
console.log(weirdo.toString); // undefined
```

### Polluting the prototype

```javascript
let obj = {};
obj.__proto__.smell = 'banana';
```

Above code is valid, and it pollutes the Object prototype. Which is not recommended.

<img src="https://user-images.githubusercontent.com/10495294/102712230-7a326880-42e5-11eb-870e-8b6d5ad2162d.png" height="300" width="550" alt="Object prototype" />

### __proto__ vs prototype

You might be wondering: what in the world is the prototype property? You might have seen it in the MDN page titles.
Bad news: the prototype property is almost unrelated to the core idea of prototypes! It’s more related to the new operator, which we haven’t used yet.
Remember that __proto__ means an object’s prototype. The prototype property and the new operator are a whole different topic we’ll skip for now.


## Lexical Scoping: (also called as static scoping)
Lexical Scoping defines how variable names are resolved in nested functions: inner functions contain the scope of parent functions even if the parent function has returned.

"Even if the parent function has returned" is called **closure**

Refer: [SO](https://stackoverflow.com/questions/1047454/what-is-lexical-scope)


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


## new keyword on Constructor function

When a function is executed with new, it does the following steps:

A new empty object is created and assigned to this.
The function body executes. Usually it modifies this, adds new properties to it.
The value of this is returned.
In other words, new User(...) does something like:

```javascript
function User(name) {
  // this = {};  (implicitly)

  // add properties to this
  this.name = name;
  this.isAdmin = false;

  // return this;  (implicitly)
}
```

### Return from constructors
Usually, constructors do not have a return statement. Their task is to write all necessary stuff into this, and it automatically becomes the result.

But if there is a return statement, then the rule is simple:

If return is called with an object, then the object is returned instead of this.
If return is called with a primitive, it’s ignored.
In other words, return with an object returns that object, in all other cases this is returned.


## Optional chaining '?.'

The optional chaining ?. is a safe way to access nested object properties, even if an intermediate property doesn’t exist.
The optional chaining ?. stops the evaluation if the part before ?. is undefined or null and returns that part.

### Other variants: ?.(), ?.[]
`userAdmin.admin?.();`
`userAdmin?.[key];`

## Symbols
A “symbol” represents a unique identifier.

A value of this type can be created using Symbol():

```javascript
// id is a new symbol
let id = Symbol();
```
We can give symbol a description (also called a symbol name), mostly useful for debugging purposes:

```javascript
// id is a symbol with the description "id"
let id = Symbol("id");
```

Symbols are guaranteed to be unique. Even if we create many symbols with the same description, they are different values. The description is just a label that doesn’t affect anything.

To print: use .toString() on symbol
```javascript
let id = Symbol("id");
alert(id.toString()); // Symbol(id), now it works
```

### “Hidden” properties
Symbols allow us to create “hidden” properties of an object, that no other part of code can accidentally access or overwrite.

Symbols are skipped by for…in, also by Object.keys(symbol)

### Global symbols
As we’ve seen, usually all symbols are different, even if they have the same name. But sometimes we want same-named symbols to be same entities. For instance, different parts of our application want to access symbol "id" meaning exactly the same property.

To achieve that, there exists a global symbol registry. We can create symbols in it and access them later, and it guarantees that repeated accesses by the same name return exactly the same symbol.

In order to read (create if absent) a symbol from the registry, use Symbol.for(key).

That call checks the global registry, and if there’s a symbol described as key, then returns it, otherwise creates a new symbol Symbol(key) and stores it in the registry by the given key.

For instance:

```javascript
// read from the global registry
let id = Symbol.for("id"); // if the symbol did not exist, it is created

// read it again (maybe from another part of the code)
let idAgain = Symbol.for("id");

// the same symbol
alert( id === idAgain ); // true
```

Refer for more details [here](https://javascript.info/symbol)


## setTimeout and setInterval

We may decide to execute a function not right now, but at a certain time later. That’s called “scheduling a call”.

There are two methods for it:

- setTimeout allows us to run a function once after the interval of time.
- setInterval allows us to run a function repeatedly, starting after the interval of time, then repeating continuously at that interval.

### Nested setTimeout
The nested setTimeout is a more flexible method than setInterval. This way the next call may be scheduled differently, depending on the results of the current one.

For instance, we need to write a service that sends a request to the server every 5 seconds asking for data, but in case the server is overloaded, it should increase the interval to 10, 20, 40 seconds…

Here’s the pseudocode:
```javascript
let delay = 5000;

let timerId = setTimeout(function request() {
  ...send request...

  if (request failed due to server overload) {
    // increase the interval to the next run
    delay *= 2;
  }

  timerId = setTimeout(request, delay);

}, delay);
```
The nested setTimeout guarantees the fixed delay
Refer more at [here](https://javascript.info/settimeout-setinterval#nested-settimeout)


## Decorators, forwarding with call, apply

Decorator is a wrapper around a function that alters its behavior. The main job is still carried out by the function.

Decorators can be seen as “features” or “aspects” that can be added to a function. We can add one or add many. And all this without changing its code!

To implement cachingDecorator, we studied methods:

`func.call(context, arg1, arg2…)` – calls func with given context and arguments.
`func.apply(context, args)` – calls func passing context as this and array-like args into a list of arguments.

The generic *call forwarding* is usually done with apply:

```javascript
let wrapper = function() {
  return original.apply(this, arguments);
};
```

We also saw an example of *method borrowing* when we take a method from an object and call it in the context of another object. It is quite common to take array methods and apply them to arguments. The alternative is to use rest parameters object that is a real array.

There are many decorators there in the wild. Check how well you got them by solving the tasks of this chapter.

[More](https://javascript.info/call-apply-decorators)
