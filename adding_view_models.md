# Adding a View Model

Sometimes it may be convenient to write a *view model* function for a component. That function takes the model and produces extra properties that are convenient for the view (thus the name view model.) Having such a function cleanly separates what belongs to the model proper and what is only for the purpose of rendering the view. Another benefit is to keep the view code simple by separating out the code that does these computations into the view model function.

Adding a view model function does not require using an additional property when creating a Meiosis component. Instead, you can just wrap the model with the view model function, and pass that to the view function:

```javascript
var view = function(model) {
  return ...;
};

var viewModel = function(model) {
  // enhance model with convenience properties
};

var component = createComponent({
  view: function(model) {
    return view(viewModel(model))
  }
});
```

View model functions are used in the [TodoMVC](https://github.com/foxdonut/meiosis-examples/tree/master/examples/todomvc) example.
