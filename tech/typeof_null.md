**Why is the result of 'typeof null' an 'object'?**

Kernel

The result of 'typeof null' being "object" is a legacy issue of the JavaScript language.

In the original version of JavaScript, a 32-bit value was used to represent a variable, with the first 3 bits representing the type of the value. 000 represents an object, 010 represents a floating point number, 100 represents a string, 110 represents a Boolean value, and other values are all considered pointers.

In this representation, null was interpreted as an all-zero pointer, that is, it is considered to be an empty object reference, so the result of typeof null is "object".

expand

Although this design is a legacy issue, it has become part of the JavaScript language for historical reasons and cannot be fixed. Therefore, it is recommended to use the strict equality operator (===) when determining whether a variable is null.

Can variables globally declared with 'let' be accessed via the window object?

Variables declared with 'let' are not attached to the global 'window' object, and therefore cannot be accessed via 'window.variablename'. This is different from variables declared with 'var', which are mounted on the global object and can be accessed via 'window.variableName'.

For example, consider the following code:
```javascript
let foo = 'bar';
var baz = 'qux';
console.log(window.foo); // undefined
console.log(window.baz); // 'qux'
```
In this code, the variable 'foo' declared with 'let' is not accessible through 'window.foo', while the variable 'baz' declared with 'var' is accessible through 'window.baz'.