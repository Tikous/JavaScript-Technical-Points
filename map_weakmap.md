**Differences between map and weakMap**

(1) Map
map is essentially a set of key-value pairs, but the key in a common Object can only be a string. The Map data structure provided by ES6 is similar to that of an object, but its keys do not limit the range. It can be of any type and is a more complete Hash structure. If the Map key is an original data type, it is considered the same key as long as the two keys are strictly the same. 

In fact, Map is an array, and each of its data is also an array, with the following format:
```javascript
const map = [
  ["name","张三"],
  ["age",18],
]
```

The Map data structure has the following operation methods:
- size: this method returns the total number of members of the Map structure.
- set(key,value): set the key value corresponding to the key name, and then return the entire Map structure. If the key already has a value, the key value is updated. Otherwise, the key is generated. (Because the current Map object is returned, it can be called in chain) 
- get(key): This method reads the key value corresponding to the key. If the key cannot be found, the undefined is returned. 
- has(key): This method returns a boolean value indicating whether a key is in the current Map object. 
- delete(key): This method deletes a key and returns true. If the key fails to be deleted, false is returned.
- clear(): map.clear() clears all members. No return value is returned. 

**The Map structure provides three traversal functions and a traversal method.**

- keys(): Returns an iterator for keys.
- values(): Returns an iterator for values.
- entries():  Returns an iterator for all members.
- forEach(): Traverses all members of the Map.

```javascript
const map = new Map([
  ["foo",1],
  ["bar",2],
])
for(let key of map.keys()){
  console.log(key);  // foo bar
}
for(let value of map.values()){
  console.log(value); // 1 2
}
for(let items of map.entries()){
  console.log(items);  // ["foo",1]  ["bar",2]
}
map.forEach( (value,key,map) => {
  console.log(key,value); // foo 1    bar 2
})
```

(2) WeakMap

WeakMap object is also a set of key-value pairs sets, where keys are weakly referenced. The key must be an object, the original data type cannot be used as a key value, but the value can be arbitrary. 
 
This object also has the following methods: 
- set(key,value): set the key value corresponding to the key name, and then return the entire Map structure. If the key already has a value, the key value is updated. Otherwise, the key is generated. (Because the current Map object is returned, it can be called in chain)
- get(key): This method reads the key value corresponding to the key. If the key cannot be found, the undefined is returned. 
- has(key): This method returns a boolean value indicating whether a key is in the current Map object. 
- delete(key): This method deletes a key and returns true. If the key fails to be deleted, false is returned. 

The clear() method has been deprecated, so you can clear it by creating an empty WeakMap and replacing the original object.

The purpose of WeakMap is to store some data on an object sometimes, but this will form a reference to the object. Once the two objects are no longer needed, you must manually delete the reference. Otherwise, the garbage collection mechanism will not release the memory occupied by the objects.

And WeakMap the objects referenced by key names are all weak references. , that is, the garbage collection mechanism does not take this reference into account. Therefore, as long as other references of the referenced object are cleared, the garbage collection mechanism releases the memory occupied by the object. That is to say, once it is no longer needed, WeakMap the key name object and the corresponding key-value pair disappear automatically. You do not need to delete the reference manually. 

Summary: 
- Map data structure. It is similar to an object and is also a set of key-value pairs. However, the range of "keys" is not limited to strings. Various types of values (including objects) can be treated as keys.
- The WeakMap structure is similar to the Map structure and is also used to generate the key-value pairs. However, WeakMap only accept objects as key names (except null) and do not accept other types of values as key names. The objects pointed to by the key name of the WeakMap are not included in the garbage collection mechanism.