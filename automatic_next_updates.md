# Automatic Next Actions

After sending a proposal, you might want to trigger another action automatically. You would decide depending on the proposal and the resulting model.

For example, after saving data from a form to the server, we may want to clear out the form. Using a proposal for that is much cleaner than clearing out the form directly. Indeed, a proposal keeps the data flow clean. Meiosis reflects the change by automatically refreshing the view.

To add a function that can trigger an automatic next action, use the `nextAction` property when creating a component. Meiosis passes the `model`, `proposal`, and either `propose` or the `actions` object to the function.

In the [rocket-laucher](https://github.com/foxdonut/meiosis-examples/tree/master/examples/rocket-launcher) example, the `nextAction` function keeps the countdown going or launches the rocket:

```javascript
ref.nextAction = function(model, proposal, actions) {
  if (ref.state.counting(model)) {
    if (model.counter > 0) {
      actions.decrement(model.counter);
    }
    else if (model.counter === 0) {
      actions.launch();
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

Meiosis calls the `nextAction` after `receive` has completed and the view has refreshed. Notice that the `nextAction` doesn't need to return anything. It should either trigger another action, or do nothing.

## Examples

The [todomvc](https://github.com/foxdonut/meiosis-examples/tree/master/examples/todomvc), [todo-list](https://github.com/foxdonut/meiosis-examples/tree/master/examples/todo-list), and [rocket-laucher](https://github.com/foxdonut/meiosis-examples/tree/master/examples/rocket-launcher) examples use `nextAction` functions.
