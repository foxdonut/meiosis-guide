# What is Meiosis?

Meiosis is a *small*, *dependency-free* library that helps you organize the data flow of your web applications. It is a UWYL library - Use What You Like! Meiosis works with:

- React
- Virtual DOM libraries (Snabbdom, Mithril, ...)
- jQuery
- Or just plain Vanilla JS!

You choose what you like to use for creating views. Meiosis organizes how the data flows in your application by:

- Creating and maintaining a single root model
- Letting you hook in function(s) that receive updates and change the model accordingly
- Passing action objects to your views so that they can send updates
- Automatically re-rendering your views
- Letting you define logic for actions that should automatically trigger
- And more.

Meiosis boils down to creating components. Specify functions for each part of the process, and Meiosis takes care of the wiring. Every part of the process is optional, so you can specify what you need for each component.

The best part is that you end up with *plain JavaScript functions*. Meiosis wires things together, but most of your code is not tied directly to Meiosis. The only library-specific code is the view code, and you get to choose whichever library you like. As can be seen in some of the examples, you could switch from one library to another and only change the view code. The rest of the code (the model, receiving updates, actions, and so on) *remains the same*.

## A Quick Example

To give you a more concrete idea of Meiosis, let's look at a quick example.