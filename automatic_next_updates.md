# Automatic Next Updates

After sending an update, you might want to trigger another update automatically, depending on the update and the resulting model.

For example, after saving data from a form to the server, we may want to clear out the form. Using an update for that is much cleaner than clearing out the form directly. Indeed, an update keeps the data flow clean and Meiosis reflects the change by automatically refreshing the view, in the same manner as any other update.

To add a function that can trigger an automatic next update, use the `nextUpdate` property when creating a component. Meiosis passes the `model`, `update`, and `actions` object to the function.

## Examples

The [todomvc](https://github.com/foxdonut/meiosis-examples/tree/master/examples/todomvc), [todo-list](https://github.com/foxdonut/meiosis-examples/tree/master/examples/todo-list), and [rocket-laucher](https://github.com/foxdonut/meiosis-examples/tree/master/examples/rocket-launcher) examples use `nextUpdate` functions.
