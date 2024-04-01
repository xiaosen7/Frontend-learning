# implement once

Today, I'm going to share a coding question which had been immplementated in lodash, this function is used to force a function to be called only once, later calls only returns the result of first call.

```js
function func(num) {
  return num;
}

const onced = once(func);
onced(1); // => 1
onced(2); // => even 2 is passed, previous result is returned.
```

This is called high-level function, high-level function is function that there is a parameter to receive a function or the result is a function.

```js
function once(func) {
  // your code here
  let called = false;
  let result = null;
  return function onced(...args) {
    if (called) {
      return result;
    }

    called = true;
    result = func.call(this, ...args);
    return result;
  }
}
```

As you can see, I declared two variables named "called" to mark this function had been called or not, "result" to record the result of first result. In side of the return function, if called is true, we can just return the result,
if not, assign 'called' to true and 'result' to the result of the input function.
