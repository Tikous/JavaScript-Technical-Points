**What happens if you create a new arrow function**

The arrow function is introduced in ES6. It does not have a prototype, nor does it have its own this reference, and it cannot use the arguments parameter. Therefore, it is not possible to use the new operator with an arrow function.

**The steps to implement the new operator are as follows:**

1. Create a new object
2. Assign the constructor function's scope to the new object (in other words, set the object's proto property to point to the constructor function's prototype property)
3. Point to the code in the constructor, and this in the constructor points to the object (That is, to add properties and methods to the object)
4. Return a new object
Therefore, the arrow functions in the above steps cannot be executed.

**The difference between arrow functions and ordinary functions**

(1) Arrow functions are more concise than ordinary functions

- If there are no arguments, just write an empty parenthesis

- If there is only one parameter, you can omit the parentheses for the parameter

- If there are multiple parameters, separate them with commas
- If the return value of the function body is only one sentence, you can omit the braces
- If the function body does not require a return value and only has one sentence, you can prefix the statement with a void keyword. The most common is to call a function:

```javascript
let fn = () => void doesNotReturn();
```

(2) Arrow functions do not have their own 'this' keyword. 

The arrow function doesn't create its own this, so it doesn't have its own this, it just inherits this at the level above its own scope. So the pointer to this in the arrow function was already fixed when it was defined, and it doesn't change after that.

(3) This pointer inherited from the arrow function never changes

```javascript
var id = 'GLOBAL';
var obj = {
  id: 'OBJ',
  a: function(){
    console.log(this.id);
  },
  b: () => {
    console.log(this.id);
  }
};
obj.a();    // 'OBJ'
obj.b();    // 'GLOBAL'
new obj.a()  // undefined
new obj.b()  // Uncaught TypeError: obj.b is not a constructor
```

Method b of object obj is defined using an arrow function, and this in this function always points to this in the global execution environment in which it was defined, even if the function is called as a method of object obj, this still points to the Window object.

It is worth noting that the curly brackets {} used to define objects cannot form a separate execution environment, they still remain in the global execution environment.

(4) The methods call(), apply(), bind(), etc. cannot change the reference of 'this' in arrow functions.

```javascript
var id = 'Global';
let fun1 = () => {
    console.log(this.id)
};
fun1();                     // 'Global'
fun1.call({id: 'Obj'});     // 'Global'
fun1.apply({id: 'Obj'});    // 'Global'
fun1.bind({id: 'Obj'})();   // 'Global'
```

(5) The process of constructing a function with 'new' has been explained above. In fact, the second step is to refer the 'this' in the function to the object. However, since arrow functions do not have their own 'this' and the 'this' refers to the outer execution environment, and cannot be changed, they cannot be used as constructors.

(6) The arrow function does not have its own arguments object. Accessing arguments in an arrow function actually gets the arguments value of its outer function.

(7) prototype
Arrow functions do not have a prototype.

(8) Arrow functions cannot be used as Generator functions and cannot use the yeild keyword