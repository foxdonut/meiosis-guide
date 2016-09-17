# The Post Render Function

Sometimes, you might need to run some code after every render of the view. If you are using plain HTML or a templating engine, you may need to run some extra code on the DOM elements. This is probably rare when using virtual DOM libraries, or reactive template libraries. They usually have their own hooks or other mechanisms for that purpose. But you may still need to run code for other reasons, such as opening a modal dialog. For these or any other reasons that you may need to run code after each render, Meiosis accepts the `postRender` function. Specify your function using the `postRender` property when calling `createComponent`, and Meiosis will call it after each render, passing in the model.

## Examples

The [VanillaJs TodoMVC](https://github.com/foxdonut/meiosis-examples/tree/master/examples/todomvc/vanillajs) and [jQuery TodoMVC](https://github.com/foxdonut/meiosis-examples/tree/master/examples/todomvc/jquery) examples use a `postRender` function to give focus to the text input which appears when the user double-clicks on a todo.
