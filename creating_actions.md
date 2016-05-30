# Creating Actions

As we saw in the counter example from the previous chapters, Meiosis passes an `actions` object to your functions. You can call `sendUpdate` to trigger an update. Your `receiveUpdate` function gets called with updates and decides how to change the model.

## Updates: Data or Actions?

In the counter example, the *update* that we send is a piece of data, such as `{ add: 1 }`.

## Specifying the `actions` Object

Optionally, you can create the `actions` object yourself. It will still have the `sendUpdate` function, but it will also contain the action functions that you define. You might prefer having these specific functions for certain actions, instead of just one generic `sendUpdate` function. Further, you might decide to encapsulate calls to services (AJAX calls, for example) within these actions.



