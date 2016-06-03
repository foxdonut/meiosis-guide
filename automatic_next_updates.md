# Automatic Next Updates

After sending an update, you might want to trigger another update automatically, depending on the update and the resulting model.

For example, after saving data from a form to the server, we may want to clear out the form. Using an update for that is much cleaner than clearing out the form directly. Indeed, an update keeps the data flow clean and Meiosis reflects the change by automatically refreshing the view, in the same manner as any other update.

To add a function that can trigger an automatic next update, use the `nextUpdate` property when creating a component. Meiosis passes the `model`, `update`, and `actions` object to the function.

In the [rocket-laucher](https://github.com/foxdonut/meiosis-examples/tree/master/examples/rocket-launcher) example, the `nextUpdate` function determines whether to keep the countdown going, or to launch the rocket:

```javascript
ref.nextUpdate = function(model, update, actions) {
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

Specify the `nextUpdate` when creating the component:

```javascript
var Main = createComponent({
  // ...
  nextUpdate: ref.nextUpdate
});
```

Meiosis calls the `nextUpdate` after `receiveUpdate` has completed and the view has been refreshed. Notice that the `nextUpdate` doesn't need to return anything. It should either trigger another update, or do nothing.

## Examples

The [todomvc](https://github.com/foxdonut/meiosis-examples/tree/master/examples/todomvc), [todo-list](https://github.com/foxdonut/meiosis-examples/tree/master/examples/todo-list), and [rocket-laucher](https://github.com/foxdonut/meiosis-examples/tree/master/examples/rocket-launcher) examples use `nextUpdate` functions.
