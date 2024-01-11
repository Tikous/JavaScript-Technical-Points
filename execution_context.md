**Understanding the execution context**
1. Execution context type 
（1）Global execution context
Anything that is not inside a function is a global execution context. It first creates a global window object and sets the value of 'this' to be this global object. There is only one global execution context in a program.
（2）Function execution context
When a function is called, a new execution context is created for that function. There can be any number of function execution contexts.
（3）eval function execution context
The code executed in the eval function has its own execution context. However, the eval function is not commonly used and will not be discussed further.


1. Execute the context stack

- the JavaScript engine uses the execution context stack to manage the execution context.

- When JavaScript executes code, it first encounters the global code, creates a global execution context, and pushes it onto the execution stack. Whenever a function call is encountered, a new execution context is created for that function and pushed onto the top of the stack. The engine then executes the function at the top of the execution context stack. After the function has finished executing, the execution context is popped off the stack, and the engine continues to execute the next context. Once all the code has been executed, the global execution context is popped off the stack.
```javascript
let a = 'Hello World!';
function first() {
  console.log('Inside first function');
  second();
  console.log('Again inside first function');
}
function second() {
  console.log('Inside second function');
}
first();
//second() first, then first()
```

1.Create an execution context 
there are two phases to create an execution context: creation phase and execution phase 
1）Creation phase 
（1）this binding 
- In the context of global execution, this points to the global object (window object).
- In the context of function execution, the value of this depends on how the function is called. If it is called by a reference object, this is set to that object; otherwise, this is set to the global object or undefined. 

（2）create lexical environment components 
- A lexical environment is a data structure that maps identifiers to variables. Identifiers refer to variable or function names, and variables are references to actual objects or primitive data.
- Environment recorder: used to store the actual location of variable function declarations references to external environments : allow access to the parent scope. 

（3）Create a variable environment component
- The variable environment is also a lexical environment. Its Environment Record holds the bindings created by variable declarations within the execution context.
- execution phase

At this stage, variables are allocated and the code is executed. 

In short, the execution context refers:

Before executing JS code, it needs to be parsed first. During parsing, a global execution context is created. Variables and function declarations that will be executed in the code are extracted first: variables are initially assigned as undefined, and functions are declared and made available. After this step is completed, the formal execution of the program begins.

Before a function is executed, a function execution context is also created, which is similar to the global execution context. However, the function execution context includes additional elements like this, arguments, and the function's parameters.
- global Context: variable definition, function declaration 
- function context: variable definition, function declaration, this , arguments