# Reducer Hook
```typescript
import React from 'react';

import compose from '@@react/universal/utils/compose';

function createEnhancedReducer<S>(
  reducer,
  initialState: S | Initializer<S>,
  enhancer: Function[] = [],
) {
  const _initialState = typeof initialState === 'function'
    ? (initialState as Function)()
    : initialState;

  const StoreContext = React.createContext<Store<S>>({
    dispatch: () => { throw new Error('dispatch is not yet available'); },
    state: _initialState,
  });

  const middlewares = Array.isArray(enhancer) ? enhancer : [enhancer];

  let currentMiddlewareDispatch;
  let middlewareDispatch = (_ = {}) => { // eslint-disable-line
    throw new Error(
      'Dispatching while constructing your middleware is not allowed. '
        + 'Other middleware would not be applied to this dispatch.',
    );
  };

  const useEnhancedReducer = () => {
    const ref = React.useRef((initialState));
    const [, setState] = React.useState(() => ref.current);

    if (currentMiddlewareDispatch === undefined) {
      const dispatch = (action) => {
        ref.current = reducer(ref.current, action);
        setState(ref.current);
        return action;
      };

      const middlewareAPI = {
        dispatch: (...args) => middlewareDispatch(...args),
        getState: () => ref.current,
      };

      const chain = middlewares.map((middleware) => middleware(middlewareAPI));
      middlewareDispatch = compose(...chain)(dispatch);
      currentMiddlewareDispatch = middlewareDispatch;
    }

    return [ref.current, currentMiddlewareDispatch];
  };

  return {
    StoreContext,
    useEnhancedReducer,
  };
}

export default createEnhancedReducer;

interface Store<S> {
  dispatch: Function;
  state: S;
}

type Initializer<S> = (args?: any[]) => S;
```
