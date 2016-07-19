# What is Meiosis?

Meiosis is a *small*, *dependency-free* library that helps you organize the data flow of your web applications. It is a UWYL library - Use What You Like! Meiosis works with:

- React
- Virtual DOM libraries (Snabbdom, Mithril, ...)
- Reactive template libraries (Riot, Vue, ...)
- jQuery
- Or just plain Vanilla JS!

You choose what you like to use for creating views. Meiosis organizes how the data flows in your application by:

- Creating and maintaining a *single root model*
- Letting you hook in function(s) that receive *proposals* and change the model accordingly
- Passing action objects to your views so that they can trigger proposals
- Automatically re-rendering your views
- Letting you define logic for actions that should automatically trigger
- And more.

Meiosis boils down to creating components. Specify functions for each part of the process, and Meiosis takes care of the wiring. Every part of the process is optional, so you can specify what you need for each component.

The general idea behind Meiosis is to start with a model. Write a function that creates the view. Meiosis will pass the model to that function, along with a *propose* function to send proposals. You can also configure an *actions* object instead. In that case, the view can call functions without needing to know the details of the proposals. Finally, create a function that receives proposals and determines the resulting model. Meiosis calls the view with the updated model.

The best part is that you end up with *plain JavaScript functions*. Meiosis wires things together, but most of your code is not tied directly to Meiosis. The only library-specific code is the view code, and you get to choose whichever library you like. As can be seen in some of the examples, you could switch from one library to another and only need to change the view code. The rest of the code (the model, receiving proposals, actions, and so on) *remains the same*.
