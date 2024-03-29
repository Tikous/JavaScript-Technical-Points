**Understanding of array-like objects and how to convert them into arrays**

An object with the length attribute and several Index attributes can be called a array-like object. Array-like objects are similar to arrays, but array methods cannot be called. Common array-like objects include arguments and DOM methods. Function parameters can also be considered as array-like objects because they contain the length attribute value, which represents the number of parameters that can be received. 

There are several common methods to convert array-likes into arrays: 
- Call the slice method of the array to implement conversion.
```javascript
Array.prototype.slice.call(arrayLike);
```

- Call the splice method of an array to implement conversion.
```javascript
Array.prototype.splice.call(arrayLike, 0);
```

- Use apply to call the concat method of an array to implement conversion
```javascript
Array.prototype.concat.apply([], arrayLike);
```


- Use the Array.from Method to implement conversion
```javascript
Array.from(arrayLike);
```
**Can the properties of const objects be modified**

const guarantees not that the value of a variable cannot be changed, but that the memory address to which the variable points cannot be changed.

For basic data types (numbers, strings, boolean values), their values are stored at the memory address the variable points to, so it is equivalent to a constant.

But for data of reference type (mainly objects and arrays), the variable points to the memory address of the data, saving only a pointer, const can only guarantee that the pointer is fixed, as it points to the data structure is not mutable, it can not control.


