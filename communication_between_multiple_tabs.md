How to realize the communication between multiple tabs in the browser?

The implementation of communication between multiple tabs is essentially achieved through the Mediator Pattern. Since tabs cannot communicate directly with each other, we can use a mediator to facilitate communication between the tabs and the mediator, and then let the mediator forward the messages. The methods of communication are as follows:

● Using the WebSocket protocol, because the WebSocket protocol can implement server push, the server can serve as this mediator. Tabs communicate with the server by sending data, and then the server pushes and forwards to other tabs.
● Using a SharedWorker. A SharedWorker creates a unique thread within the page's lifetime, and opening multiple pages will still only use the same thread. At this point, the shared thread can act as the mediator. Tabs communicate by sharing a thread, and then data exchange is realized through this shared thread.
● Using localStorage, we can listen for changes to localStorage in one tab, and then when another tab modifies the data, we can get the data through this listening event. At this time, the localStorage object acts as the mediator.
● Using the postMessage method, if we can obtain a reference to the corresponding tab, we can communicate using the postMessage method.