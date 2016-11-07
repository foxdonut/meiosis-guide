# The Ready Function

With virtual DOM libraries such as [React](https://facebook.github.io/react), [Inferno](http://github.com/trueadm/inferno), [Snabbdom](https://github.com/paldepind/snabbdom), [Mithril](http://mithril.js.org), and [others](http://vdom-benchmark.github.io/vdom-benchmark/), it is often easy to attach handlers from the view function. However, when returning plain HTML strings, for example from string concatenation, jQuery, or templating engines, it is convenient to attach handlers when the initial document is ready. For this and other code you need to run **only once** after rendering the initial view, use the Meiosis `ready` function.

## Examples

The [VanillaJs TodoMVC](https://github.com/foxdonut/meiosis-examples/tree/master/examples/todomvc/vanillajs) and [jQuery TodoMVC](https://github.com/foxdonut/meiosis-examples/tree/master/examples/todomvc/jquery) examples use a `ready` function to attach event handlers. All of the examples also use `ready` to listen to location changes using the [history](https://github.com/ReactJSTraining/history) library.
