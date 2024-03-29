There are five types of threads in the browser's rendering process:

(1) GUI rendering thread

Responsible for rendering browser pages, parsing HTML, CSS, constructing DOM trees, CSSOM trees and render trees, as well as painting pages; This thread executes when the interface needs to be redrawn or when reflow is caused by some operation.

Note: The GUI rendering thread and the JS engine thread are mutually exclusive; the GUI thread will be suspended while the JS engine is executing. GUI updates will be queued and executed once the JS engine is idle.

(2) JS engine thread

The JS engine thread, also known as the JS kernel, is responsible for processing Javascript scripts, parsing Javascript scripts, and running code; The JS engine thread has been waiting for the task in the task queue to arrive, and then processing, a Tab page at any time only one JS engine thread is running the JS program;

Note: The GUI rendering thread and the JS engine thread are mutually exclusive, so if the JS execution time is too long, the page will be rendered incoherently, resulting in page rendering load blocking.

(3) Event-triggered the thread

The event-triggered thread belongs to the browser, not the JS engine, and is used to control the event loop. When the JS engine executes a block of code such as setTimeOut (but also other threads from the browser kernel, such as mouse clicks, AJAX asynchronous requests, etc.), the corresponding task is added to the event trigger thread; When the corresponding event meets the trigger conditions and is triggered, the thread will add the event to the end of the queue to be processed and wait for the JS engine to process it.

Note: Due to the single-threaded relationship of JS, these events in the queue have to queue for the JS engine to process (when the JS engine idle will be executed);

(4) Timer triggers the thread

The process triggered by timer is the thread where setInterval and setTimeout reside. The browser timing counter is not counted by the JS engine, because the JS engine is single-threaded, if the thread is blocked, it will affect the accuracy of the timing; Therefore, a separate thread is used to time and trigger the timer. After the timer is finished, it is added to the event queue and executed after waiting for the JS engine to be idle. Therefore, the task in the timer may not be executed on time at the set time point, and the timer only adds the task to the event queue at the specified time point.

Note: The W3C stipulates in the HTML standard that the timer timing time cannot be less than 4ms, if it is less than 4ms, the default is 4ms.

(5) Asynchronous http request threads

● The XMLHttpRequest connection opens a new thread request through the browser;
● When the status change is detected, if the callback function is set, the asynchronous thread will generate the status change event, put the callback function into the event queue, and wait for the JS engine to execute after idle;