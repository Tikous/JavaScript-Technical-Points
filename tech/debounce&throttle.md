**Implementing a Debounce Function Manually**

Debouncing a function means that the callback is executed n seconds after the event is triggered, and if the event is triggered again within these n seconds, the timer restarts. This can be applied to click-request events to prevent multiple requests from being sent to the backend due to multiple clicks by the user.
```javascript
function debounce(fn, wait) {
  let timer = null;
  return function() {
    let context = this,
        args = arguments;
    if (timer) {
      clearTimeout(timer);
      timer = null;
    }
    timer = setTimeout(() => {
      fn.apply(context, args);
    }, wait);
  };
}
```

**Implementing a Throttle Function Manually**

Function throttling is a technique where you specify a unit of time, and within this time frame, only one callback function for the triggered event can be executed. If the same event is triggered multiple times within the same unit of time, only one instance will take effect. Throttling can be applied to event listeners of scroll functions to reduce the frequency of event invocation by throttling events.
```javascript
function throttle(fn, delay) {
  let curTime = Date.now();
  return function() {
    let context = this,
        args = arguments,
        nowTime = Date.now();
    if (nowTime - curTime >= delay) {
      curTime = Date.now();
      return fn.apply(context, args);
    }
  };
}
```