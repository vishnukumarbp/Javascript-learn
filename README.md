# Javascript-learn
Self learning of Javascript in depth

#### Definition: Javascript (JS)

It is a Interpreted or JIT compiled Programming Language with first class function (function treated as variable). Also known as scripting language for web pages. Also used in non-browser environment like node.js, apache couchDB and Adobe Acrobat. JS is prototype-based, dynamci language.

Protoype-based: is a style of Object Oriented programming in which classes are not explicitly defined, but rather dervied by adding properties and methods to instance of another class or to an empty object.

### Prototype:

As stated, Javascript is prototype based programming. When a function is created in JavaScript, JavaScript engine adds a *prototype* property to the function. This prototype property is an object has a constructor property by default. constructor property points back to the function on which prototype object is alive. We can access the function’s prototype property using the syntax functionName.prototype. 
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

