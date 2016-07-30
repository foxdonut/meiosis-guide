# Using a State Object

As [described in the SAM pattern](http://sam.js.org/#state), the State Object computes the current state of the application, and processes the next-action predicate.

In Meiosis, the next-action predicate is already handled by the `nextUpdate` function. That leaves computing the state of the application.

## Computing the State of the application

Much like the [view model](adding_view_models.md), the State Object can contain convenience functions. In this case, these functions describe the current state of the model.

In the [TodoMVC](https://github.com/foxdonut/meiosis-examples/tree/master/examples/todomvc) example, one State Object has a function to determine whether all todos have been completed:

```javascript
var state = {
  allCompleted: function(model) {
    var result = true;

    for (var i = 0, t = model.filteredTodos.length; i < t; i++) {
      if (!model.filteredTodos[i].completed) {
        result = false;
        break;
      }
    }
    return result;
  }
};
```

This state object can then be used in the view model:

```javascript
var viewModel = function(state, model) {
  var viewModel = model;

  viewModel.allCompleted = state.allCompleted(model);

  return viewModel;
};
```

Finally the `allCompleted` property can be used in the view to determine whether the check-all checkbox should be checked.
