**Differences among Ajax, axios, and fetch**
（1）AJAX
Ajax stands for "Asynchronous JavaScript and XML." It's a way to make web pages interactive without reloading the whole page. Ajax updates parts of a page by fetching a bit of data from the server behind the scenes. This means updates can happen without a full page refresh. Traditional web pages without Ajax need a full reload to update. However, Ajax is not perfect:
- It's more suited for MVC programming, not quite in line with the front-end MVVM trend.
- Built on the not-so-clear architecture of native XHR.
- Doesn't quite stick to the Separation of Concerns principle.
- Setup and calling methods can be a bit messy, and its event-based async model isn't friendly.

（2）Fetch
Fetch is often seen as AJAX's replacement, coming into play with ES6 and using its promise objects. It's all about promises, making its code structure way simpler than Ajax. Fetch isn't just a rewrap of Ajax; it's native JavaScript and does not use XMLHttpRequest objects.
The cool things about fetch:
- Straightforward syntax, more semantic.
- Built on the standard Promise, supports async/await.
- More fundamental, comes with a rich set of APIs (request, response).
- Moves away from XHR, offering a new approach in ES standards.
The not-so-cool things about fetch:
- It only throws errors for network issues, treating 400s and 500s as successes. It won't reject for these server errors unless it's a network problem.
- By default, fetch won't carry cookies. You need to tweak it with: fetch(url, {credentials: 'include'}).
- Lacks support for aborting requests or controlling timeouts. Workarounds like setTimeout and Promise.reject can't stop the ongoing background process, wasting data.
- Can't natively track the progress of requests, unlike XHR.
（3）Axios
Axios is a Promise-based HTTP client. It's features are as follows:
- Launches XMLHttpRequests from browsers.
- Handles HTTP requests in Node.js.
- Supports the Promise API.
- Tracks requests and responses.
- Transforms requests and responses.
- Can cancel requests.
- Automatically handles JSON data.
- The client side supports to guard against XSRF attacks.