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

The function accepts the model as a parameter and returns the view, which displays the counter and buttons to increase and decrease the value.

Now, don't run away screaming *HTML with string concatenation! OH NOES!* You can use whatever you like to create views: virtual DOM libraries such React, Snabbdom, and Mithril, templating engines such as Handlebars, or anything else. We'll switch to React later in this example. The point is, you don't *need* to use any particular library; if creating the HTML from simple string concatenation suits your needs, that is fine with Meiosis.

## Specifying a Renderer

The way you tell Meiosis how you want to create your views is by specifying a *renderer*. Meiosis currently provides renderers for:

- Vanilla JS (String concatenation or template engines such as [Handlebars](http://handlebarsjs.com)
- [React](https://facebook.github.io/react/)
- [Snabbdom](http://github.com/paldepind/snabbdom)
- [Mithril](http://mithril.js.org)

Implementing a renderer for other libraries is easy. Refer to the [as yet unwritten] *Implementing a Renderer* chapter.

Let's specify the Vanilla JS renderer for our counter example:

```javascript
var Meiosis = meiosis.init(meiosisVanillaJs.renderer.intoId("app"));
```

We've initialized Meiosis with the Vanilla JS renderer and told it to render into the element with the `app` id. We just need a container with that id in our HTML page:

```html
<div id="app"></div>
```

Our view will be rendered into that `div`.

## Running Meiosis

Now that we have initialized Meiosis, we can create a component:

```javascript
var Main = Meiosis.createComponent({
  initialModel: initialModel,
  view: view
});
```

The `createComponent` function accepts several properties, all of which are optional. Here, we've indicated the `initialModel` and the `view` function.

The `Main` component that we've created is also the *root*, or *top-level*, component of our application. We need to pass it to `Meiosis.run` to start Meiosis:

```javascript
Meiosis.run(Main);
```

Now, we will see the result of the `view` function being called with the `initialModel`.

## Sending Updates

The view renders, but the buttons don't do anything yet. For them to work, they need to *send updates*. Meiosis provides an `actions` object with a `sendUpdate` function to do exactly that.

Let's use jQuery to attach event handlers to the buttons. Again, note that we'll also look at how we can do this with React.

When creating a component, we can indicate a `ready` function that will be called *once* after the initial view has finished rendering. This is where we attach our event handlers:

```javascript
var ready = function(actions) {
  var $root = $(document.getElementById("app"));

  $root.on("click", "button#inc", function(_evt) {
    actions.sendUpdate({ add: 1 });
  });
  $root.on("click", "button#decr", function(_evt) {
    actions.sendUpdate({ add: -1 });
  });
};
```

Meiosis passes the `actions` object to the ready function. We use its `sendUpdate` function to send updates. In this case, the update requests to add an amount to the counter. We pass the `ready` function to `createComponent`, which is now:

```javascript
var Main = Meiosis.createComponent({
  initialModel: initialModel,
  view: view,
  ready: ready
});
```

Let's finish the example by receiving the updates.

## Receiving Updates

Finally, we need a function to receive updates and decide how to change the model:

```javascript
var receiveUpdate = function(model, update) {
  return { counter: model.counter + update.add };
};
```

Not surprisingly, we use `receiveUpdate` to pass our function to `createComponent`:

```javascript
var Main = Meiosis.createComponent({
  initialModel: initialModel,
  view: view,
  ready: ready,
  receiveUpdate: receiveUpdate
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

var receiveUpdate = function(model, update) {
  return { counter: model.counter + update.add };
};

var ready = function(actions) {
  var $root = $(document.getElementById("app"));

  $root.on("click", "button#inc", function(_evt) {
    actions.sendUpdate({ add: 1 });
  });
  $root.on("click", "button#decr", function(_evt) {
    actions.sendUpdate({ add: -1 });
  });
};

var Meiosis = meiosis.init(meiosisVanillaJs.renderer.intoId("app"));

var Main = Meiosis.createComponent({
  initialModel: initialModel,
  view: view,
  ready: ready,
  receiveUpdate: receiveUpdate
});

Meiosis.run(Main);
```

You can run this example online [here](http://codepen.io/foxdonut/pen/ezYgNo?editors=1010). You will also find it in the [meiosis-examples](https://github.com/foxdonut/meiosis-examples/tree/master/examples/counter) repository.
