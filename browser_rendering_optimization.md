Browser rendering optimization

（1）For JavaScript: As JavaScript blocks both HTML parsing and CSS parsing, we can optimize by changing the way JavaScript loads:

  Try to put the JavaScript file at the end of the body
  
  Try not to write &lt;script&gt; tags in the middle of the body
  
  There are three ways to include resources with the &lt;script&gt; tag: one is the commonly used direct inclusion, and the other two involve using the async and defer attributes for asynchronous inclusion. Both aim to asynchronously load external JavaScript files without blocking the parsing of the DOM (it's advisable to use asynchronous loading whenever possible). The differences among the three are as follows:

● script immediately stops the page rendering to load the resource file, executes the js code immediately after the resource is loaded, and continues to render the page after the js code is executed.

● async is loaded asynchronously immediately after the download is completed, and is executed immediately after loading. Multiple labels with async attributes cannot guarantee the order of loading;

● defer is loaded asynchronously immediately after the download is complete. After loading, if the DOM tree is not built, wait until the DOM tree is parsed before executing; If the DOM tree is ready, execute immediately. Multiple tags with defer attributes, executed in order.

(2) For CSS: There are three ways to use CSS: using link, @import, and inline styles, where link and @import import external styles. The difference between them:

● link: The browser sends a new isothread (HTTP thread) to load the resource file, while the GUI rendering thread continues to render the code downward

● @import: GUI rendering thread will temporarily stop rendering, go to the server to load the resource file, and will not continue rendering until the resource file is returned (blocking browser rendering)

● style: GUI direct rendering

If the external style is not loaded for a long time, the browser will use the default style for the user experience to ensure the speed of the first rendering. Therefore, CSS is usually written in head, so that the browser can send a request to get the css style as soon as possible.

So, during development, importing external styles uses link instead of @import. If there is little css, use inline styles where possible and write directly in the style tag.

(3) For DOM tree and CSSOM tree:

There are several ways to reduce rendering time:

● The code level of the HTML file should not be too deep

● Use semantic tags to avoid special processing that is not standard semantic

● Reduce the hierarchy of the CSS code because the selector parses from left to right

(4) Reduce reflow and redraw:

● When manipulating the DOM, try to operate the DOM node at a lower level

● Do not use the table layout, a small change may cause the entire table to be rearranged

● Expressions using CSS

● Do not frequently manipulate the style of the element, for static pages, you can change the class name, not the style.

● Use absolute or fixed to keep elements out of the document flow so that changes to them do not affect other elements

● Instead of manipulating the DOM too much, you can create a documentFragment, apply all the DOM operations to it, and then add it to the document

● Set the element to display: none first, and then display it after the operation is complete. Because DOM operations on elements with display attribute none do not cause reflow and redraw.

● Put multiple DOM read operations (or write operations) together, rather than read and write operations interspersed with write operations. This is thanks to the browser's rendering queue mechanism.

The browser has its own optimization for the reflow and redraw of the page - the render queue

The browser will put all the reflux and redraw operations in a queue, and when the number of operations in the queue reaches a certain number or a certain time interval, the browser will batch the queue. This will turn multiple reflux redraws into one reflux redraw.

Putting multiple reads (or writes) together will wait until all the reads are in the queue, so that what should be multiple reflow triggers only one reflow.