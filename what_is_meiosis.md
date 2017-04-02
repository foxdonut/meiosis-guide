# What is Meiosis?

PLEASE NOTE that Meiosis has changed starting with version 1.0.0. This guide applies only to version 0.9.x and is kept for reference purposes.

Meiosis is a *small*, *dependency-free* library that helps you organize the data flow of your web applications. It is a UWYL library - Use What You Like! Meiosis works with:

- [React](https://facebook.github.io/react/),  [Inferno](http://github.com/trueadm/inferno)
- [Snabbdom](http://github.com/paldepind/snabbdom), [Mithril](http://mithril.js.org)
- [jQuery](http://jquery.com)
- Or just plain [Vanilla JS](http://vanilla-js.com)!

You choose what you like to use for creating views. Meiosis organizes how the data flows in your application by:

- Creating and maintaining a *single root model* - the *single source of truth*
- Optionally supporting a `state` function that takes the model and computes additional properties, producing the *application state*
- Letting you hook in functions that receive *proposals* and change the model accordingly
- Passing action objects to your views so that they can trigger proposals
- Automatically re-rendering your views
- Letting you define logic for actions that should automatically trigger.

Meiosis is about managing the application data flow. Create components by specifying functions, and Meiosis takes care of the wiring. Every part of the process is optional, so you can specify what you need for each component.

If you are familiar with the [SAM pattern](http://sam.js.org) by [Jean-Jacques Dubray](http://www.ebpml.org/about), you will recognize these concepts. Indeed, Meiosis is an implementation of the SAM pattern.

The general idea behind Meiosis is to start with a model. Optionally write a `state` function that adds computed properties to produce the *application state*. Write a function that creates the view. Meiosis will pass the model/application state to that function, along with a *propose* function to send proposals. You can also configure an *actions* object instead. In that case, the view can call functions without needing to know the details of the proposals. Finally, create a function that receives proposals and determines the resulting model. Meiosis calls the view with the updated model. You can also define a function to determine if another action should automatically trigger.

The best part is that you end up with *plain JavaScript functions*. Meiosis wires things together, but most of your code is not tied directly to Meiosis. The only library-specific code is the view code, and you get to choose whichever library you like. As can be seen in some of the examples, you could switch from one library to another and only need to change the view code. The rest of the code (the model, receiving proposals, actions, and so on) *remains the same*.
