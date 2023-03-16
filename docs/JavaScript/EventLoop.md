# Event Loop

```js
console.log("1");
setTimeout(() => {
  console.log("2");
}, 1000);
console.log("3");
// 1 3 2
```

- setTimeout is a web api provided by the browser
- When we execute the above code, first of all, one call stack is created, then
- At line number 1, js engine console logs 1.
- At line number 2, js engine encounters setTimeout and it puts it in web api environment for further execution. setTimeout waits for 1 second in web api environment.
- At the same time, js runtime console logs 3.
- After setTimeout completes 1 second, it gets pushed into callback queue.
- Now, there is something called event loop. Event loop monitors the call stack and when call stack is empty it puts the first item of call back queue into callstack for the execution.
- setTimeout gets finally executed in the callstack.

- Even if setTimeout has 0 millisecond, output will be 1 3 2
- Because evenloop only puts item from callback queue into call stack when the call stack is empty.
