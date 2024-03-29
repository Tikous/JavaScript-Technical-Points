**What is the purpose of the newly added primitive data type "Symbol"?**

**Discuss conceptual questions**

'Symbol' is a primitive data type introduced in ES6. Its primary purpose is to create a unique identifier, which is used in scenarios such as naming object properties, defining constants, and so on.

**Understanding with Examples**

Each 'Symbol' is unique and can be used as a property name for objects, which helps to avoid conflicts with property names. For example:
```javascript
const s1 = Symbol();
const s2 = Symbol();
const obj = {
 [s1]: 'hello',
 [s2]: 'world'
};
console.log(obj[s1]); // "hello"
console.log(obj[s2]); // "world"
```

In addition, symbol can also be used to implement constants or enumeration values, which are immutable and unique, such as:
```javascript
const Colors = {
 Red: Symbol('Red'),
 Green: Symbol('Green'),
 Blue: Symbol('Blue')
};
console.log(Colors.Red); // Symbol(Red)
console.log(Colors.Green); // Symbol(Green)
console.log(Colors.Blue); // Symbol(Blue)
```
As Symbol is a primitive data type, it offers high performance and reliability, making it suitable for scenarios requiring efficient and secure creation and usage of identifiers.

**Important Considerations**

Another significant characteristic of Symbol is that it does not appear in object property iteration methods like for...in, for...of, Object.keys(), Object.getOwnPropertyNames(), and so on. Therefore, it can be used to define properties that should not be iterated over, such as internal implementation details or hidden attributes.