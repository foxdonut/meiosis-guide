# Counter Example with jQuery

To give you a more concrete idea of Meiosis, let's look at a quick example. We'll create a simple counter with buttons to increase and decrease the value.

You can run this example online [here](http://codepen.io/foxdonut/pen/ezYgNo?editors=1010). You will also find it in the [meiosis-examples](https://github.com/foxdonut/meiosis-examples/tree/master/examples/counter) repository.

## Creating a Model and a View

We'll start with a model for the counter:

```javascript
var initialModel = { counter: 0 };
```

Next, let's write a view function:

```javascript
var view = function(model) {
  return "<div><span>Counter: " + model.counter + "</span></div>" +
    "<div><button id='inc'>+</button> <button id='decr'>-</button></div>";
};
```

The function accepts the model as a parameter and returns the view. The view displays the counter and buttons to increase and decrease the value.

Now, don't run away screaming *HTML with string concatenation! OH NOES!* You can use whatever you like to create views. Virtual DOM libraries such React, Snabbdom, and Mithril. Reactive template libraries such as Riot and Vue. Templating engines such as Handlebars. Or anything else. We'll switch to React later in this example. The point is, you don't *need* to use any particular library. If creating the HTML from simple string concatenation suits your needs, that is fine with Meiosis.

## Specifying a Renderer

The way you tell Meiosis how you want to create your views is by specifying a *renderer*. Meiosis currently provides renderers for:

- Vanilla JS (String concatenation, or template engines such as [Handlebars](http://handlebarsjs.com))
- [Mithril](http://mithril.js.org)
- [React](https://facebook.github.io/react/)
- [Riot](http://riotjs.com)
- [Snabbdom](http://github.com/paldepind/snabbdom)
- [Vue](http://vuejs.org)

Implementing a renderer for other libraries is easy. Refer to the [Renderers](renderers.md) section.

Let's specify the Vanilla JS renderer for our counter example:

```javascript
var renderer = meiosisVanillaJs.renderer();
```

## Running Meiosis

Next, we'll create a component:

```javascript
var Main = meiosis.createComponent({
  initialModel: initialModel,
  view: view
});
```

The `createComponent` function accepts properties, all of which are optional. Here, we've indicated the `initialModel` and the `view` function.

The `Main` component that we've created is also the *root*, or *top-level*, component of our application. We need to pass the renderer and the root component to `meiosis.run` to start Meiosis:

```javascript
meiosis.run(renderer.intoId(document, "app"), Main);
```

We've initialized the renderer and told it to render into the element with the `app` id. We just need a container with that id in our HTML page:

```html
<div id="app"></div>
```

Our view will render into that `div`.

Now, we will see the result of calling the `view` function with the `initialModel`.

## Sending Proposals

The view renders, but the buttons don't do anything yet. For them to work, they need to *send proposals*. Meiosis provides a `propose` function to do precisely that.

Let's use jQuery to attach event handlers to the buttons. Again, note that we'll also look at how we can do this with React.

When creating a component, we can indicate a `ready` function that will be called *once* after the initial view has finished rendering. This is where we attach our event handlers:

```javascript
var ready = function(propose) {
  var $root = $(document.getElementById("app"));

  $root.on("click", "button#inc", function(_evt) {
    propose({ add: 1 });
  });
  $root.on("click", "button#decr", function(_evt) {
    propose({ add: -1 });
  });
};
```

Meiosis passes the `propose` function to the `ready` function. We use it to send proposals. In this case, the proposal is to add an amount to the counter. We pass the `ready` function to `createComponent`, which is now:

```javascript
var Main = Meiosis.createComponent({
  initialModel: initialModel,
  view: view,
  ready: ready
});
```

Let's finish the example by receiving the proposals.

## Receiving Proposals

Finally, we need a function to receive proposals and decide how to change the model:

```javascript
var receive = function(model, proposal) {
  return { counter: model.counter + proposal.add };
};
```

We pass this `receive` function to `createComponent`:

```javascript
var Main = Meiosis.createComponent({
  initialModel: initialModel,
  view: view,
  ready: ready,
  receive: receive
});
```

Our example is complete!

## Try it out

To recap, here is the full code for the example:

```javascript
var initialModel = { counter: 0 };

var view = function(model) {
  return "<div><span>Counter: " + model.counter + "</span></div>" +
    "<div><button id='inc'>+</button> <button id='decr'>-</button></div>";
};

var receive = function(model, proposal) {
  return { counter: model.counter + proposal.add };
};

var ready = function(propose) {
  var $root = $(document.getElementById("app"));

  $root.on("click", "button#inc", function(_evt) {
    propose({ add: 1 });
  });
  $root.on("click", "button#decr", function(_evt) {
    propose({ add: -1 });
  });
};

var Main = meiosis.createComponent({
  initialModel: initialModel,
  view: view,
  ready: ready,
  receive: receive
});

var renderer = meiosisVanillaJs.renderer();

meiosis.run(renderer.intoId(document, "app"), Main);
```

You can run this example online [here](http://codepen.io/foxdonut/pen/ezYgNo?editors=1010). You will also find it in the [meiosis-examples](https://github.com/foxdonut/meiosis-examples/tree/master/examples/counter) repository.
