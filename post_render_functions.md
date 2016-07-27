# The Post Render Function

Sometimes, you might need to run some code after every render of the view. This is probably rare when using virtual DOM libraries, or reactive template libraries. They usually have their own hooks or other mechanisms for that purpose. But if you are using plain HTML or templating engine, or for any other reason you may need to run code after each render, Meiosis accepts the `postRender` function. Specify your function using the `postRender` property when calling `createComponent`, and Meiosis will call it after each render.

## Examples

The [VanillaJs TodoMVC](https://github.com/foxdonut/meiosis-examples/tree/master/examples/todomvc/vanillajs) and [jQuery TodoMVC](https://github.com/foxdonut/meiosis-examples/tree/master/examples/todomvc/jquery) examples use a `postRender` function to give focus to the text input which appears when the user double-clicks on a todo.
