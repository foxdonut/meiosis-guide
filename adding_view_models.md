# Adding a View Model

Sometimes it may be convenient to write a *view model* function for a component. That function takes the model and produces extra properties that are convenient for the view (thus the name view model.) Having such a function cleanly separates what belongs to the model proper and what is only for the purpose of rendering the view. Another benefit is to keep the view code simple by separating out the code that does these computations into the view model function.

Adding a view model function does not require using an additional property when creating a Meiosis component. Instead, you can just write a *higher order function* (a function that takes another function as a parameter, or that returns a function as a result; the function below does both.)

```javascript
var display = function(view) {
  return function(model, actions) {
    return view(viewModel(model), actions);
  };
};
```

We now have a `display` function that takes the `view` function as a parameter, and returns a *new* function that will act as the `view` function that we will use when creating the component. The `display` function calls the `view` function, but instead of passing the model, it passes the result of calling `viewModel(model)`. The `viewModel` is another function that we write, which does the work of producing whatever extra data that will make the life of the `view` function easier:

```javascript
var viewModel = function(model) {
  var viewModel = Object.assign({}, model);

  viewModel.someConvenientProperty = someFunction(model);
  // ...

  return viewModel;
};
```

Now, we just need to wrap the `view` function with the `display` function when creating the component:

```javascript
var Component = createComponent({
  // ...
  view: display(view),
  // ...
});
```

The [todomvc](https://github.com/foxdonut/meiosis-examples/tree/master/examples/todomvc) example uses a [view model function](https://github.com/foxdonut/meiosis-examples/blob/master/examples/todomvc/common/display.js) in this manner.
