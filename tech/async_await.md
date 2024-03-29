**Understanding of async/await**

Async/await is actually the syntax sugar of Generator. The effect it can achieve can be realized by the then chain. It was developed to optimize the then chain. Literally, async is the abbreviation of "asynchronous", await is waiting, so it is easy to understand that async is used to declare that a function is asynchronous, and await is used to wait for an asynchronous method to complete. Of course, the syntax forces that await can only appear in the asnyc function. 

An async function returns a Promise object. Async functions, including function statements, function expressions, and Lambda expressions, all return a Promise object. If a literal value is returned from the function, async wraps this value with Promise.resolve(), converting it into a Promise object. 

An async function returns a Promise object. Therefore, when it's not possible to use await at the outermost level to obtain its return value, the appropriate approach is to use the original method: handling the Promise object with a then() chain

What if the async function does not return a value? It is easy to imagine that it will return Promise. resolve (undefined) .

Think about the characteristics of Promises — namely, their non-blocking nature — executing an async function without await results in its immediate execution, returning a Promise object without blocking subsequent statements. This behavior is consistent with functions that return a Promise object.

Note: Promise.resolve(x) can be viewed as a shorthand for new Promise(resolve => resolve(x)). It is used to quickly wrap literal objects or other objects into Promise instances.