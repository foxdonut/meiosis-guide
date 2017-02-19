# Creating Actions

As we saw in the counter example from the previous chapters, Meiosis passes `propose` to your `view` and `ready` functions. You can call `propose` to trigger a proposal. Your `receive` function gets called with the proposal and decides how to change the model.

## Proposals

In the counter example, the *proposal* that we send is `{ add: 1 }`. The `receive` function then adds that value to the counter.

Another option would be to use [union-type](https://github.com/paldepind/union-type) to define possible proposals. The `receive` function would then look like:

```javascript
var Action = Type({ ... });

var receive = function(model, proposal) {
  return Action.case({
    ...
  }, proposal);
};
```

In any case, you might prefer to hide the details of proposals from the view. For that, you can create an `actions` object.

## Specifying the `actions` Object

You can create the `actions` object to encapsulate the details of how you construct proposals. You might prefer having these specific functions for your actions, instead of just one generic `propose` function. Further, you might decide to encapsulate calls to services (AJAX calls, for example) within these actions.

This allows to encapsulate the details of what proposal to send. The view can call named functions directly. In the counter example, this would mean calling functions like `actions.increaseCounter()` and `actions.decreaseCounter()` instead of `propose({ add: 1 })`.

To create the `actions` object, simply write a function that accepts `propose` as a parameter and returns an object with the actions that you wish to make available. For example:

```javascript
var actions = function(propose) {
  return {
    increaseCounter: function() {
      propose({ add: 1 });
    },
    decreaseCounter: function() {
      propose({ add: -1 });
    },
    addValue: function(value) {
      propose({ add: value });
    }
  };
};
```

Then, specify the function when creating the component:

```javascript
var Main = createComponent({
  view: ...,
  actions: actions
})
```

Now, instead of `propose`, the `view` and `ready` functions will be given the  `actions` object and be able to call `actions.increaseCounter()`, `actions.decreaseCounter()`, and `actions.addValue(value)`.

## Examples

The [todomvc](https://github.com/foxdonut/meiosis-examples/tree/v0.9.0/examples/todomvc), [todo-list](https://github.com/foxdonut/meiosis-examples/tree/v0.9.0/examples/todo-list), and [rocket-laucher](https://github.com/foxdonut/meiosis-examples/tree/v0.9.0/examples/rocket-launcher) examples create `actions` objects.
