**What are the differences in asynchronous loading of JS scripts?**

In Web applications, the asynchronous loading of JavaScript scripts can be achieved in the following ways:

1. Dynamically create a script tag and set its src attribute to the URL of the script to be loaded. You can use the onload or onreadystatechange event to check if the script has finished loading.
```javascript
const script = document.createElement('script');
script.src = 'path/to/script.js';
script.onload = function() {
};
document.body.appendChild(script);
```
2. Use the XMLHttpRequest object or the Fetch API to send an asynchronous request. After a successful request, parse the response text into JavaScript code, and then use the eval() function or Function() constructor to execute the script.
```javascript
const xhr = new XMLHttpRequest();
xhr.open('GET', 'path/to/script.js');
xhr.onload = function() {
 const script = document.createElement('script');
 script.textContent = xhr.responseText;
 document.head.appendChild(script);
};
xhr.send();
```

These two methods can be used to implement the asynchronous loading of JavaScript scripts. Compared to synchronous loading, asynchronous loading has the following differences:
1. Asynchronous loading can improve the loading speed and response performance of the page, and avoid the situation that the page is stuck due to JavaScript blocking.

2. Asynchronous loading avoids the blocking caused by loading scripts and allows other resources of the page to load and render faster.

3. Asynchronous loading allows you to flexibly control the loading sequence and the execution time of scripts, and dynamically load and unload scripts based on page requirements, thus improving page maintainability and expansibility.