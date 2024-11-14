
# JavaScript: The Hard Parts, v2 | Frontend Masters

### Introduction


### JavaScript Principles

**Thread of Execution**
- JS goes through our code line by line and run it i.e (Thread of execution). and Saves data in the memory so it can be use later.
- When saving data to memory, we do not save data liek function bcos it is meant to do something. we only saves the fixed value not the one that need further actions.
- Call stack is where JS keep track of what is currently running (Thread of execution). When will run a function its been add to the top of the stack and when we reach return keyword it basically removes the function from the call stack.
- For every call stack we have a global call stack that get return to when it is done running.

- 


### Functions & Callbacks

**Generalized Functions**

- Paramenters for placeholder and arugment for the actual value the function is been call up on. 
- Paramenters means we do not need to decided what data to run our functionality on untill we run the function, we provide actual value argument when we run the function, HOF follow this same principle. We may not want to decide exactly what some of our functionality is untill we run out function.
- We could geeralise our function and pass in out specific instruction only when we run the fuction.
- HOF is possible bcos Function in js is like an OBJECT. HOF is any function that takes in or return out a function.
- HOF is the outer function that takes in a function, Callback is a function we insert to the HOF.(Just a term to describe these functions, but there's nothing different about them inherently).
- When pass a funtion  or object as paramenter to a HOF, we are making a reference copy of them, so if you change or update the function or object we are modifying the whole function or object a good one is to have a local function or object to work with. 
- for loop is not an execution stack. it get it own protected namespace.
- Callbacks are a core  aspect of async JS and are under the hood of promises, async/await.


### Closure

**Closure Introduction**

- Functions never remember anything from their previous running. The local memory from previous running that store previous arugment value in memory is not remeber again, as it get a new fresh execution context everytime.
- The function local memory can also be call STATE, VARIABLE ENVIRONMENT
- Function defination is a value, it can be store with a label or identify.
- When a HOF return a function, the function defination which is a value get returns without the identify just the value(the code), the return function previous name is gone and it will have a new identify or label. we loose the former function label.
- The function return by th HOF is permanent and has the live data(also permanent and does not get wipe out in the execution context). When a new identify is been assign to the function , the live data get the initial state.
- Lexical(means physical) or static scoping means where a function is born/save/define determines what data it has access to when that function runs or being call, for the rest of it life, under whatever new label.not the dynamic scope that means the scoping depends on where the fuction is called.
- The language of JS has a very popular scope rule called Lexical or static scoping and bcos of this rule we have closure(Backpack, Persistent Lexical Scope Reference Data(PLSRD)).
- Closure or backpack is a result of JS being a Lexically scope language, once that bring the data with the function whenever the function goes.

- [00:01:37](https://frontendmasters.com/courses/javascript-hard-parts-v2/closure-introduction?t=97)
Here's a link to Will's [other courses](https://frontendmasters.com/teachers/will-sentance/)


- [00:00:41](https://frontendmasters.com/courses/javascript-hard-parts-v2/closure-exercises?t=41)
Here's a link to the [closures solutions](https://github.com/FrontendMasters/fm-snippets/blob/main/javascript-hard-parts-v2/closures.js)

### Asynchronous JavaScript

**Single Threaded Execution Review**

- JS is Single threaded (one command runs at a time) and  Synchronously executed (each line is run in order the code appears). which is a problem bcos slow function blocks further code running hence why Asynchronous.
- To do Async, JS is not enough, we need some new features which are not JS atall. JS has three main part(Thread of execution same as execution context, Memory/variavle enviroment and call stack). but we need to add some new component that are not JS(web Browser api node api, eventloop, microtasks, callback queue etc).
- JS runs in the browser and the browser has so much in it than just JS, Browser has alots features that js does not has(e.g Network request, Rendering,HTML DOM,Socket, devtools,timer) all of these features are in browser but not in JS but JS allow us to interact with them with the help of facade function JS provided e.g(settimout) that help us to use the timer features from browser, same as Document, fetch/xhr ETC. the big part of what we are doing in js is not even in js at all.
- when the facade function runs they just call features from the browser and throw the function that suppose to run and all the neccessary info the browser feature's need to the run outside the js to the brower.when the features is done working(e.g timer from setimeout) the function been throw will be pass to the event loop not the callstack.
- The Event loop is JS triage(referring to the assignment of priority levels to tasks or individuals to determine the most effective order in which to deal with tasks).
- Since we are interacting with the world outside JS we have some new rules on how to run our code so it can be predictable,
- The functions that get runs by the facade feature when they complete running, this function get run in the call stack only when the Global execution is done(all synchroniuos cde, all regular execution) and when the call stack is done before we cal push the callback queue back. This is the work of EVENT LOOP. does a very fast checking constantly if the call stack empty, is any global code to run, is anything in the queue. 

- [00:01:27](https://frontendmasters.com/courses/javascript-hard-parts-v2/single-threaded-execution-review?t=87)
Here's a link to Jake Archibald's [article on microtasks](https://jakearchibald.com/2015/tasks-microtasks-queues-and-schedules/)

**Callback Hell & Async Exercises**

- In Es5 web browser API with callback functions, our response data is only available in the callback fuction i.e calllback hell. and its error handling is not as clean as the promises.

### Promises

**Promises Introduction**

- With promises we get a two-pronged facade function that do two things at same time(Initiate background web browser work and Return a placeholder object (promise) immediately in JavaScript), when the background work is done in the browser.
- In order to get track what the browser feature is doing for us in JS we have to have an object.
- fetch has two consequeces, in the js where fetch return an promisE object that has value and unfullfill property, and the web browser to use feature of a network request via the url(address) given. 
- The value inside the object fetch return will have the data when the request return the data. the unfullfill array is going to have any code /functions we want to run when the request return (i.e when the data comes back) and this function or code can make use of the data the request returns.
- Special objects built into JavaScript that get returned immediately when we make a call to a web browser API/feature (e.g. fetch) that’s set up to return promises (not all are)
- Promises act as a placeholder for the data we expect to get back from the web browser feature’s background work
- Any code we want to run on the returned data must also be saved on the promise object Added using .then method to the hidden property ‘onFulfilment’. Promise objects will automatically trigger the attached function to run (with its input being the returned data)
- The promise-deferred functionality get back into the JS to be run via another queue that is not the callback queue but MICROTASK QUEUE.MQ is priorize than the callback queue. hence the code in there is been run first before the CBQ function
- Hold promise-deferred functions in a microtask queue and callback function in a Task queue (Callback queue) when the Web Browser Feature (API) finishes Add the function to the Call stack (i.e. run the function) when:
- Call stack is empty & all global code run (Have the Event Loop check this condition).
- Prioritize functions in the microtask queue over the Callback queue

[00:02:49](https://frontendmasters.com/courses/javascript-hard-parts-v2/promises-and-asynchronous-q-a?t=169)
Here's a link to a list of the [MDN Web APIs](https://developer.mozilla.org/en-US/docs/Web/API)

### Classes & Prototypes|"?
**Class & OOP Introduction**




