# Counter Example with React

Let's look at the same simple counter example as in [the previous chapter](counter_example_with_jquery.md), this time with React.

You can run this example online [here](http://codepen.io/foxdonut/pen/OXJXmv?editors=1010). You will also find it in the [meiosis-examples](https://github.com/foxdonut/meiosis-examples/tree/master/examples/counter) repository.

## Creating a Model and a View

The model for the counter is the same:

```javascript
var initialModel = { counter: 0 };
```

As you might expect, the view function is different. Since we're using React, we'll use JSX to render the view (although JSX is *not* required to use React; see [JSnoX](https://github.com/af/JSnoX) for example.)

```javascript
var view = function(model, actions) {
  var onInc = function(_evt) {
    actions.sendUpdate({ add: 10 });
  };
  var onDecr = function(_evt) {
    actions.sendUpdate({ add: -10 });
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

This time, the function accepts the model **and** the `actions` object because React makes it easy to bind event handlers to view elements. We call `sendUpdate` in the same way as we did previously. However, because we've attached the event handlers here, we won't be needing a `ready` function.

## Specifying a Renderer

We'll specify the React renderer:

```javascript
var Meiosis = meiosis.init(meiosisReact.renderer.intoId("app"));
```

Remember that we're initializing Meiosis a renderer and telling it to render into the element with the `app` id, which is a `<div>` on our HTML page.

## Running Meiosis

Having initialized Meiosis, we can create the component:

```javascript
var Main = Meiosis.createComponent({
  initialModel: initialModel,
  view: view,
  receiveUpdate: receiveUpdate
});
```

The `initialModel` and `receiveUpdate` functions are the same as the ones we had from the previous chapter. Only the `view` has changed, to use React. Because we are attaching event handlers using React's `onClick` in the view, we don't need a `ready` function. We're ready to run Meiosis:

```javascript
Meiosis.run(Main);
```

Our counter works.

## Try it out

To recap, here is the full code for the example:

```javascript
var initialModel = { counter: 0 };

var view = function(model, actions) {
  var onInc = function(_evt) {
    actions.sendUpdate({ add: 10 });
  };
  var onDecr = function(_evt) {
    actions.sendUpdate({ add: -10 });
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

var receiveUpdate = function(model, update) {
  return { counter: model.counter + update.add };
};

var Main = Meiosis.createComponent({
  initialModel: initialModel,
  view: view,
  receiveUpdate: receiveUpdate
});

Meiosis.run(Main);
```

You can run this example online [here](http://codepen.io/foxdonut/pen/OXJXmv?editors=1010). You will also find it in the [meiosis-examples](https://github.com/foxdonut/meiosis-examples/tree/master/examples/counter) repository.
