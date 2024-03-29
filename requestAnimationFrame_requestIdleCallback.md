**What are the uses of 'requestAnimationFrame' and 'requestIdleCallback', respectively?**

'RequestAnimationFrame' and 'requestIdleCallback' are both APIs used for performing animations or other high-performance tasks in the browser.

'RequestAnimationFrame' is a mechanism provided by browsers to request an animation frame. It executes a specified callback function right before the browser's next redraw. The advantage of this approach is that it allows the browser to automatically perform complex calculations and rendering tasks during the next draw, thus preventing the browser from repeating the same tasks within a short period. Using requestAnimationFrame can lead to smoother animations and reduce flickering and stuttering on web pages.

RequestIdleCallback is a relatively new API that performs a specified callback function when the browser is idle. The purpose of this API is to enable developers to perform time-consuming tasks such as computation and rendering when the browser is idle. The advantage of this is that it can improve the performance and responsiveness of the web page, while also avoiding blocking the main thread of the browser, resulting in a poor user experience.
```javascript
function doWork(deadline) {
 while (deadline.timeRemaining() > 0) {
   // something
 }
 if (still have task need to be executed) {
   requestIdleCallback(doWork);
 }
}
requestIdleCallback(doWork);
```

Note that the callback function of requestIdleCallback accepts an IdleDeadline parameter, which contains information about the current idle time. Developers can use this parameter to schedule and optimize tasks according to the idle time of the browser.

In summary, requestAnimationFrame is suitable for animation tasks that need to be executed before the next drawing, while requestIdleCallback is suitable for time-consuming tasks that need to be executed when the browser is idle.

