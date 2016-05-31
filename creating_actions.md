# Creating Actions

As we saw in the counter example from the previous chapters, Meiosis passes an `actions` object to your functions. You can call `sendUpdate` to trigger an update. Your `receiveUpdate` function gets called with updates and decides how to change the model.

## Updates: Data or Actions?

In the counter example, the *update* that we send is a piece of data, such as `{ add: 1 }`. The `receiveUpdate` function then adds that value to the counter.

You can send whatever you want as an update. You may decide that you prefer sending an *action* as an update, such as a [Flux Standard Action](https://github.com/acdlite/flux-standard-action), that is, an object with a `type` and a `payload`. In that case, you would perhaps send `{ type: "ADD", payload: 1 }` or even just `{ type: "INCREMENT" }`. The `receiveUpdate` function would use the `type` and `payload` to determine how to change the model.

Another option would be to use [union-type](https://github.com/paldepind/union-type) to define possible actions. The `receiveUpdate` function would then look like:

```javascript
var Action = Type({ ... });

var receiveUpdate = function(model, update) {
  return Action.case({
    ...
  }, update);
};
```

The point is, you are free to choose how to send and receive updates.

## Specifying the `actions` Object

You can also create the `actions` object yourself. It will still have the `sendUpdate` function, but it will also contain the action functions that you define. You might prefer having these specific functions for certain actions, instead of just one generic `sendUpdate` function. Further, you might decide to encapsulate calls to services (AJAX calls, for example) within these actions.

This allows to encapsulate the details of what to send in the update in named functions that the view event handler can call directly. In the counter example, this would mean calling functions like `actions.increaseCounter()` and `actions.decreaseCounter()` instead of `actions.sendUpdate({ add: 1 })`.

To create the `actions` object, simply write a function that accepts `sendUpdate` as a parameter and returns an object with the actions that you wish to make available. For example:

```javascript
var actions = function(sendUpdate) {
  return {
    increaseCounter: function() {
      sendUpdate({ add: 1 });
    },
    decreaseCounter: function() {
      sendUpdate({ add: -1 });
    },
    addValue: function(value) {
      sendUpdate({ add: value });
    }
  };
};
```

Then, specify the function when creating the component:

```javascript
var Main = createComponent({
  initialModel: ...,
  view: ...,
  actions: actions
})
```

Now, functions that are given the `actions` object will be able to call `increaseCounter`, `decreaseCounter`, `addValue`, and `sendUpdate`.
