**Implementing the apply Function Manually**

Steps to implement the apply function:

1. Determine if the calling object is a function. Even though it's defined on the function's prototype, there may be instances where it is invoked using methods like call.

2. Check if the incoming context object exists; if not, set it to window.

3. Assign the function as a property of the context object.

4. Determine if the parameter values have been passed in.

5. Invoke the method using the context object and save the returned result.

6. Remove the property that was just added.

7. Return the result
```javascript
Function.prototype.myApply = function(context) {
  if (typeof this !== "function") {
    throw new TypeError("Error");
  }
  let result = null;
  context = context || window;
  context.fn = this;
  if (arguments[1]) {
    result = context.fn(...arguments[1]);
  } else {
    result = context.fn();
  }
  delete context.fn;
  return result;
};
```


**Implementing the bind Function Manually**

Steps to implement the bind function:

1. Determine if the calling object is a function. Even though it's defined on the function's prototype, there may be instances where it is invoked using methods like call.

2. Save a reference to the current function and retrieve the rest of the passed-in parameter values.

3. Return a new function.

4. Internally, the function uses apply to bind the function call. It's important to account for the function being used as a constructor. In such cases, the current function's 'this' needs to be passed to apply, while in all other cases, the specified context object is passed.
```javascript
Function.prototype.myBind = function(context) {
  if (typeof this !== "function") {
    throw new TypeError("Error");
  }
  var args = [...arguments].slice(1),
      fn = this;
  return function Fn() {
    return fn.apply(
      this instanceof Fn ? this : context,
      args.concat(...arguments
    );
  };
};
```
