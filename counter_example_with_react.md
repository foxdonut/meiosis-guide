# Counter Example with React

Let's look at the same simple counter example as in [the previous section](counter_example_with_jquery.md), this time with React.

You can run this example online [here](http://codepen.io/foxdonut/pen/OXJXmv?editors=1010). You will also find it in the [meiosis-examples](https://github.com/foxdonut/meiosis-examples/tree/v0.9.0/examples/counter) repository.

## Creating a Model and a View

The model for the counter is the same:

```javascript
var initialModel = { counter: 0 };
```

As you might expect, the view function is different. Since we're using React, we'll use JSX to render the view. JSX is *not* required to use React; one example of an alternative is [JSnoX](https://github.com/af/JSnoX).

```javascript
var view = function(model, propose) {
  var onInc = function(_evt) {
    propose({ add: 2 });
  };
  var onDecr = function(_evt) {
    propose({ add: -2 });
  };
  return (
    <div>
      <div><span>Counter: {model.counter}</span></div>
      <div>
        <button onClick={onInc}>+</button>
        <button onClick={onDecr}>-</button>
      </div>
    </div>
  );
};
```

This time, the function accepts the model *and* the `propose` function. React makes it easy to bind event handlers to view elements. We call `propose` in the same way. Because we've attached the event handlers here, we won't be needing a `ready` function.

## Specifying the Renderer

We'll specify the React renderer:

```javascript
var renderer = meiosisReact.renderer();
```

## Creating the Component

We can now create the component:

```javascript
var Main = meiosis.createComponent({
  view: view,
  receive: receive
});
```

The `initialModel` and `receive` functions are the same as the ones we had from the previous example. The `view` has changed to use React. Because we are attaching event handlers using React's `onClick` in the view, we don't need a `ready` function.

## Running Meiosis

We're ready to run Meiosis:

```javascript
meiosis.run({
  renderer: renderer.intoId(document, "app"),
  initialModel: initialModel,
  rootComponent: Main
});
```

Our counter now works with React.

## Try it out

To recap, here is the full code for the example:

```javascript
var initialModel = { counter: 0 };

var view = function(model, propose) {
  var onInc = function(_evt) {
    propose({ add: 10 });
  };
  var onDecr = function(_evt) {
    propose({ add: -10 });
  };
  return (
    <div>
      <div><span>Counter: {model.counter}</span></div>
      <div>
        <button onClick={onInc}>+</button>
        <button onClick={onDecr}>-</button>
      </div>
    </div>
  );
};

var receive = function(model, proposal) {
  return { counter: model.counter + proposal.add };
};

var renderer = meiosisReact.renderer();

var Main = meiosis.createComponent({
  view: view,
  receive: receive
});

meiosis.run({
  renderer: renderer.intoId(document, "app"),
  initialModel: initialModel,
  rootComponent: Main
});
```

You can run this example online [here](http://codepen.io/foxdonut/pen/OXJXmv?editors=1010). You will also find it in the [meiosis-examples](https://github.com/foxdonut/meiosis-examples/tree/v0.9.0/examples/counter) repository.
