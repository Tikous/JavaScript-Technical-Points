**Flatten the array**

(1) Recursive implementation
The common idea behind recursion is straightforward, involving a circular recursion approach where each item is iterated over. If an item is still an array, the process continues recursively to achieve the concatenation of each array item.
(2) reduce function iteration
From the ordinary recursive function described above, it's clear that each array item is processed individually. In fact, the reduce method can also be used for array concatenation, thus simplifying the code from the first method. The transformed code is as follows:
(3) Extension operator implementation
This method's implementation involves the use of the spread operator and the some method, both used in conjunction to achieve array flattening:
（4）split and toString
The split and toString methods are used to flatten the array. Since the array has a toString method by default, you can convert the array directly to a comma-separated string, and then use the split method to convert the string back to the array, as shown in the following code:
Using these two methods, a multidimensional array can be directly converted into a comma-separated string, which is then split back into an array.
(5) flat in ES6
We can also directly call the flat method in ES6 to implement array flattening. Syntax for the flat method: arr.flat([depth])
depth is the parameter of flat, depth is the expansion depth of the array can be passed (the default is not filled, the value is 1), that is, expand a layer of array. If the number of layers is uncertain, the parameter can be passed into Infinity, which means that no matter how many layers are expanded:
```javascript
let arr = [1, [2, [3, 4]]];
function flatten(arr) {
  return arr.flat(Infinity);
}
console.log(flatten(arr)); //  [1, 2, 3, 4，5]
```
As you can see, a nested array of two layers achieves the desired effect by setting the parameter of the flat method to Infinity. In fact, it can also be set to 2, which can also achieve this effect. In the programming process, if the number of nested layers of the array is uncertain, it is best to use Infinity directly, which can achieve flatness.
(6) RE and JSON methods
The toString method is already used in the fourth method, which still uses the JSON.stringify method to convert it to a string, then filters out the array square brackets in the string through regular expressions, and finally converts it to an array using JSON.parse:
```javascript
let arr = [1, [2, [3, [4, 5]]], 6];
function flatten(arr) {
  let str = JSON.stringify(arr);
  str = str.replace(/(\[|\])/g, '');
  str = '[' + str + ']';
  return JSON.parse(str); 
}
console.log(flatten(arr)); //  [1, 2, 3, 4，5]
```
