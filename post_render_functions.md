# Post Render Functions

With virtual DOM libraries such as [React](https://facebook.github.io/react), [Snabbdom](https://github.com/paldepind/snabbdom), [Mithril](http://mithril.js.org), and [others](http://vdom-benchmark.github.io/vdom-benchmark/), it is often easy to attach handlers from the view function. However, when returning plain HTML strings, for example from string concatenation, jQuery, or templating engines, it is convenient to attach handlers after the view has rendered. For this and other code you need to run after rendering the view, Meiosis accepts the `postRender` function.

## Examples

The [VanillaJs todomvc](https://github.com/foxdonut/meiosis-examples/tree/master/examples/todomvc/vanillajs) and [jQuery todomvc](https://github.com/foxdonut/meiosis-examples/tree/master/examples/todomvc/jquery) examples uses a `postRender` function.
