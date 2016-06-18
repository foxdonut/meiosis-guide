# Using a State Object

As [described in the SAM pattern](http://sam.js.org/#state), the State Object computes the current state of the application, decides which view to use to represent that state, and processes the next-action predicate.

In Meiosis, the next-action predicate is already handled by the `nextUpdate` function. That leaves computing the state of the application, and deciding which view to call to represent the state.

## Computing the State of the application

Much like the [view model](adding_view_models.md), the State Object can contain convenience functions. In this case, these functions describe the current state of the model.

## Using Views to Represent the State

Again, we can achieve this with higher-order functions.
