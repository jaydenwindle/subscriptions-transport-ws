---
title: Lifecycle Events
---

`SubscriptionServer` exposes lifecycle hooks you can use to manage your subscription and clients:

* `onConnect` - called upon client connection, with the `connectionParams` passed to `SubscriptionsClient` - you can return a Promise and reject the connection by throwing an exception. The resolved return value will be appended to the GraphQL `context` of your subscriptions.
* `onDisconnect` - called when the client disconnects.
* `onOperation` - called when the client executes a GraphQL operation - use this method to create custom params that will be used when resolving the operation.
* `onOperationComplete` - called when client's operation has been done it's execution (for subscriptions called when unsubscribe, and for query/mutation called immediately).

```js
const subscriptionsServer = new SubscriptionServer(
  {
    onConnect: (connectionParams, webSocket, context) => {
      // ...
    },
    onOperation: (message, params, webSocket) => {
      // ...
    },
    onOperationComplete: webSocket => {
      // ...
    },
    onDisconnect: (webSocket, context) => {
      // ...
    },
  },
  {
    server: websocketServer,
  },
);
```
