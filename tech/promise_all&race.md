**The difference and usage scenarios between Promise.all and Promise.race**
（1）Promise.all
Promise.all can wrap multiple Promise instances into a single new Promise instance. Additionally, the return values for success and failure are different. On success, it returns an array of results, whereas on failure, it returns the value from the first Promise that was rejected.

In Promise.all, an array is passed in, and an array is also returned. The returned values from the inputted Promise objects are mapped and arranged in the array in the order they were passed in. However, it is important to note that the execution order of these Promises is not necessarily sequential, unless the iterable object is empty.

It should be noted that the order of data in the array of successful results obtained by Promise.all matches the order of the array received by Promise.all. This is particularly useful in scenarios where multiple requests are sent and data needs to be obtained and used in the order of these requests. Promise.all can be used to handle such situations.

（2）Promise.race
As implied by its name, Promise.race is analogous to a race. It means that in Promise.race([p1, p2, p3]), whichever result is obtained first, that result is returned, regardless of whether it's a success or a failure. This method can be useful when there's a need to perform an action only within a certain time frame; if the time is exceeded, the action is no longer pursued.

```javascript
Promise.race([promise1,timeOutPromise(5000)]).then(res=>{})
```

It is a common requirement in work. For instance, after sending a request A using ajax and successfully receiving data, I need to pass this data to request B. The code for this would typically look like this:
```javascript
let fs = require('fs')
fs.readFile('./a.txt','utf8',function(err,data){
  fs.readFile(data,'utf8',function(err,data){
    fs.readFile(data,'utf8',function(err,data){
      console.log(data)
    })
  })
})
```

The preceding code has the following disadvantages:

- The subsequent request depends on the success of the previous one to pass on the data, leading to a scenario where multiple ajax requests are nested, making the code less intuitive.

- if the first and second requests do not need to pass parameters, the next request needs to be executed after the previous request succeeds. In this case, the code needs to be written as above, resulting in insufficient intuitive code.

After the advent of Promises, the code becomes as follows:

```javascript
let fs = require('fs')
function read(url){
  return new Promise((resolve,reject)=>{
    fs.readFile(url,'utf8',function(error,data){
      error && reject(error)
      resolve(data)
    })
  })
}
read('./a.txt').then(data=>{
  return read(data) 
}).then(data=>{
  return read(data)  
}).then(data=>{
  console.log(data)
})
```
In this way, the code looks much simpler and solves the problem of Hell callback.