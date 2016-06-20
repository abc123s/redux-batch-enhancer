# redux-batch-enhancer
Store enhancer and action creator that enables batching subscriber notifications for an array of actions, including complex actions (e.g. thunks) enabled by middleware. Inspired by [redux-batched-actions](https://github.com/tshelburne/redux-batched-actions) and [redux-batched-subscribe](https://github.com/tappleby/redux-batched-subscribe).

# Installation
```
npm install --save redux-batch-enhancer
```
Then to enable, apply the provided store enhancer (```batchStoreEnhancer```) and middleware (```batchMiddleware```):
```javascript
import { createStore } from 'redux'
import { batchEnhancer, batchMiddleware } from 'redux-batch-enhancer'

const store = createStore(
  reducer,
  compose(
    applyMiddleware(batchMiddleware, thunk, logger, perflogger),
    batchStoreEnhancer,
  )
);
```
Note: ```batchStoreEnhancer``` overwrites dispatch and subscribe on the original redux store, and thus must be applied before any middleware or store enhancers that depend on these two methods.

# Example Usage
```javascript
import { batchActions } from 'redux-batch-enhancer'

dispatch(batchActions([{ type: 'vanillaAction' }, createThunkAction()]));
```
