# Automatic Next Actions

After propose - receive - model - render view has completed, you might want to trigger another proposal automatically. You would decide depending on the last proposal and the resulting model.

To add a function that can trigger an automatic next action, use the `nextAction` property when creating a component. Meiosis passes a single object parameter with the `model`, `proposal`, and either `propose` or the `actions` object to the function.

In the [rocket-laucher](https://github.com/foxdonut/meiosis-examples/tree/v0.9.0/examples/rocket-launcher) example, the `nextAction` function keeps the countdown going or launches the rocket:

```javascript
ref.nextAction = function(context) {
  if (ref.state.counting(context.model)) {
    if (context.model.counter > 0) {
      context.actions.decrement(context.model.counter);
    }
    else if (context.model.counter === 0) {
      context.actions.launch();
    }
  }
};
```

Specify the `nextAction` when creating the component:

```javascript
var Main = createComponent({
  // ...
  nextAction: nextAction
});
```

Meiosis calls the `nextAction` after `receive` has completed and the view has refreshed. Notice that the `nextAction` doesn't need to return anything. It should either trigger another action by calling `propose(...)` or `actions.someAction(...)`, or do nothing.

## Examples

The [rocket-laucher](https://github.com/foxdonut/meiosis-examples/tree/v0.9.0/examples/rocket-launcher),
[temperatures](https://github.com/foxdonut/meiosis-examples/tree/v0.9.0/examples/temperatures), and
[todo-list](https://github.com/foxdonut/meiosis-examples/tree/v0.9.0/examples/todo-list) examples use a `nextAction` function.
