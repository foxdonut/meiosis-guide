# Application State

In the previous section, we saw how to specify the model. This is the *single source of truth*. All properties of the model should be independent. However, the view may need additional properties for convenience. These properties *depend* on other properties of the model. In other words, they are *computed* properties. When the model changes, these properties should also change accordingly.

With Meiosis you can specify a `state` property when calling the `run` function. This property should be a function of the model and return the *application state*, that is, everything that the view needs.

## The State Function in Components

Similarly to `initialModel`, the `state` function can be specified in `run` as well as in `createComponent`. Just as with `initialModel`, for the `state` function `run` is the starting point and `createComponent` gives each component the possibility to *augment* the application state.

When you specify a `state` function in `createComponent`, it gets passed the model and the state. Remember that the starting point for the state is the function passed to `run`. Each component then adds more computed properties to the state, and returns it.
