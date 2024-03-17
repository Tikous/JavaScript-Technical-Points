**The difference between null and undefined**

First of all, Undefined and Null are both basic data types. Each of these two basic data types has only one value, which is undefined and null.

Undefined means undefined, while null means empty object. When a general variable is declared but not yet defined, it will return undefined. null is mainly used to assign values to variables that may return objects as initialization.

Undefined is not a reserved word in JavaScript, which means that it can be used as a variable name, but this approach is very dangerous as it can affect the judgment of the undefined value. We can obtain secure undefined values through some methods, such as void 0.

When using typeof to judge these two types, Null typing will return "object", which is a historical problem. Returns true when using a double equal sign to compare two types of values, and returns false when using a triple equal sign.