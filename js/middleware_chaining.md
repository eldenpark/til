# Middleware Chaining
```js
function compose(...funcs: Function[]): Function {
  if (funcs.length === 0) {
    return (arg) => arg;
  }

  if (funcs.length === 1) {
    return funcs[0];
  }

  return funcs.reduce((a, b) => {
    return (...args) => a(b(...args));
  });
}

function c(next) {
  console.log('c called, next', next);
  return (action) => {
    console.log('c1 next action', next, action);
    // const x = next(action);
    console.log('c2 action', x);
  };
}

function b(next) {
  console.log('b called, next', next);
  return (action) => {
    console.log('b1, next, action', next, action);
    const x = next(action);
    console.log('b2', x);
  };
}

const x = ((...arg) => c(b(...arg)))(() => {
  console.log('dispatch!');
});
console.log(555, x(5));
```
