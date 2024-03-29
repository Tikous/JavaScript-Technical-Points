**What are the characteristics of setTimeout, setInterval and requestAnimationFrame?**

Timers are certainly essential for asynchronous programming. Common timer functions include setTimeout, setInterval, and requestAnimationFrame. The most commonly used is setTimeout, and many people believe that the delay specified in setTimeout dictates exactly when the function will execute.

In fact, this view is wrong, because JS is executed on a single thread. If the previous code affects the performance, it may result in setTimeout not executed as schedule. Of course, setTimeout can be adjusted by code to make the timer relatively more accurate.
```javascript
let period = 60 * 1000 * 60 * 2
let startTime = new Date().getTime()
let count = 0
let end = new Date().getTime() + period
let interval = 1000
let currentInterval = interval
function loop() {
  count++
  let offset = new Date().getTime() - (startTime + count * interval);
  let diff = end - new Date().getTime()
  let h = Math.floor(diff / (60 * 1000 * 60))
  let hdiff = diff % (60 * 1000 * 60)
  let m = Math.floor(hdiff / (60 * 1000))
  let mdiff = hdiff % (60 * 1000)
  let s = mdiff / (1000)
  let sCeil = Math.ceil(s)
  let sFloor = Math.floor(s)
  currentInterval = interval - offset 
  console.log(h, m, s, sCeil, offset, currentInterval) 
  setTimeout(loop, currentInterval)
}
setTimeout(loop, currentInterval)
```

Now let's look at 'setInterval' . This function is basically the same as setTimeout, except that it executes a callback function at regular time intervals. 

Generally, it is not recommended to use 'setInterval'. Firstly, similar to setTimeout, it cannot guarantee that the task will be executed exactly at the scheduled time. Secondly, it has an issue of execution accumulation.  See the following pseudo code.
```javascript
function demo() {
  setInterval(function(){
    console.log(2)
  },1000)
  sleep(2000)
}
demo()
```
In the browser environment, if a time-consuming operation occurs during timer execution, multiple callback functions may execute simultaneously once the operation is completed, potentially leading to performance issues. 

If a looping timer is needed, it can effectively be implemented using 'requestAnimationFrame'.
```javascript
function setInterval(callback, interval) {
  let timer
  const now = Date.now
  let startTime = now()
  let endTime = startTime
  const loop = () => {
    timer = window.requestAnimationFrame(loop)
    endTime = now()
    if (endTime - startTime >= interval) {
      startTime = endTime = now()
      callback(timer)
    }
  }
  timer = window.requestAnimationFrame(loop)
  return timer
}
let a = 0
setInterval(timer => {
  console.log(1)
  a++
  if (a === 3) cancelAnimationFrame(timer)
}, 1000)
```
With its intrinsic throttling feature, 'requestAnimationFrame' can largely ensure only one execution within 16.6 milliseconds, provided that there are no frame drop issues. Moreover, this function's delay effect is highly accurate, without the common timing issues of other timers, and it can also be used to serve the purpose of setTimeout.