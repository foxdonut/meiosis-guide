# The Elm Architecture

Meiosis has some inspiration from [The Elm Architecture](http://guide.elm-lang.org/architecture/index.html), by [Evan Czaplicki](http://evan.czaplicki.us/home).

The `receive` function is similar to the `update` function from the Elm architecture, but without requiring immutability, and without returning side effects to be executed. How Meiosis wires things together is analogous to Elm's `StartApp`, albeit different in implementation. Finally, the `view` function in Meiosis is similar to that of the Elm architecture, where the function receives a model to render and a means to trigger updates. That is the `propose` function or the `actions` object in Meiosis, equivalent to the `address` in Elm.
