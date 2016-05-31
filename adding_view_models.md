# Adding View Models

Sometimes it may be convenient to write a *view model* function for a component. Meiosis will call this function with the updated model after `receiveUpdate`, and before calling `view`, so that the function can augment the model with properties that are convenient for the view.

## Examples

The [todomvc](https://github.com/foxdonut/meiosis-examples/tree/master/examples/todomvc) example uses a `viewModel` function.
