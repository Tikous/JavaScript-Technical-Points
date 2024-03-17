**Do splice and slice change the original array? How to delete the last element of an array?**
splice() and slice() are both methods of JavaScript arrays, but they work differently.

1. The splice() method can add, remove, or replace elements in an array and return the deleted element. It modifiies the original array.

2. The slice() method creates a new array with elements from the original array, specified by start and end positions, without changing the original array.

Therefore, using the splice() method may change the original array, while the slice() method does not.

To delete the last element of an array, there are several ways:

1. To delete the last element of an array, use the pop() method to delete and return the last element:
```javascript
const arr = [1, 2, 3, 4];
const lastElement = arr.pop(); // [1, 2, 3]
```
2. Delete the last element of an array using the splice() method:
```javascript
const arr = [1, 2, 3, 4];
arr.splice(-1, 1); // [1, 2, 3]
```
3. Use the slice() method and the spread operator (...) to create a new array containing all the elements except the last one:
```javascript
const arr = [1, 2, 3, 4];
const newArr = [...arr.slice(0, -1)];
console.log(newArr); // [1, 2, 3]
```
It should be noted that all the above methods either change the original array or create a new one, without preserving the last element in the original array. If you want to retrieve only the last element, you can use indexing or the array method slice():
```javascript
const arr = [1, 2, 3, 4];
const lastElement = arr[arr.length - 1]; // 4
const lastElement2 = arr.slice(-1)[0]; // 4
```
