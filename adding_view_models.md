# Adding a View Model

Sometimes it may be convenient to write a *view model* function for a component. Meiosis will call this function with the updated model after `receiveUpdate`, and before calling `view`, so that the function can augment the model with properties that are convenient for the view.

To add a view model function to a component, simply specify a `viewModel` property when creating the component. The function should accept the model as a parameter and return the view model. Whether the function mutates the model or returns a new object is really up to you.

## Examples

The [todomvc](https://github.com/foxdonut/meiosis-examples/tree/master/examples/todomvc) example uses a `viewModel` function.
