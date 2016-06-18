# Creating the View

In Meiosis, the `view` function returns a view object that corresponds to the library of your choice. It could be a plain string, JSX, a hyperscript object, and so on.

## Specifying a Renderer

The way you tell Meiosis how you want to create your views is by specifying a *renderer*. Meiosis currently provides renderers for:

- Vanilla JS (String concatenation or template engines such as [Handlebars](http://handlebarsjs.com)
- [React](https://facebook.github.io/react/)
- [Snabbdom](http://github.com/paldepind/snabbdom)
- [Mithril](http://mithril.js.org)

Implementing a renderer for other libraries is easy. Refer to the [as yet unwritten] *Implementing a Renderer* chapter.

To specify the React renderer, you would write:

```javascript
var Meiosis = meiosis.init(meiosisReact.renderer.intoId("app"));
```

Then, you just need a container with the `"app"` id in your HTML page:

```html
<div id="app"></div>
```

Meiosis will render the view into that `div`.

## Creating a `view` Function

Each component that you create can have a `view` function. Meiosis calls it with `(model, actions)` so that you can return the view representation of the model, and call functions on the `actions` object.

The nature of what you return from the `view` function depends on the view library that you chose for your views. Whether you chose React, Snabbdom, Mithril, plain JavaScript, or anything else, you return an object that is compatible with the chosen library.

## Nested components

When you call `Meiosis.createComponent({...})`, the returned component is the view function with the `actions` object already provided. Thus it is a function of the model that you can call from other components.

The [todo-list example](https://github.com/foxdonut/meiosis-examples/tree/master/examples/todo-list) has a `TodoMain` component that uses two other components, `TodoForm` and `TodoList`:

```javascript
import React from "react";
import todoListConfig from "./todoList/main";
import todoFormConfig from "./todoForm/main";

export default function(Meiosis) {
  const createComponent = Meiosis.createComponent;

  const TodoList = createComponent(todoListConfig);
  const TodoForm = createComponent(todoFormConfig);

  const TodoMain = createComponent({
    view: model => (
      <div>
        <div id="tracer" style={{position: "fixed", top: "0px", right: "0px"}}></div>
        <TodoForm {...model}/>
        {TodoList(model)}
      </div>
    )
  });
  Meiosis.run(TodoMain);
}
```

This example demonstrates two ways of calling nested components in JSX. First, as a JSX component: `<TodoForm {...model}/>`. Second, as a function: `{TodoList(model)}`. Notice that while we pass the `model`, there is no need to pass the `actions` object. Meiosis will take care of that. In fact, if each component has configured a specialized `actions` object, they will each get their own version with the functions that they have defined.

Here is another nested component from the [labeled-sliders example](https://github.com/foxdonut/meiosis-examples/blob/master/examples/labeled-sliders/sliderContainer/view.js), written with Snabbdom:

```javascript
import h from "snabbdom/h";

import { Action } from "./actions";

const view = LabeledSlider => (model, actions) => {
  const onAddMeasurement = _evt => actions.sendUpdate(Action.AddMeasurement());
  const onRemoveMeasurement = id => actions.sendUpdate(Action.RemoveMeasurement(id));

  const renderMeasurement = (measurement, index) =>
    h("div", {key: measurement.id, style: {border: "1px solid gray"}, id: measurement.id}, [
      LabeledSlider({measurement, index}),
      h("div", [
        h("button.btn.btn-danger.btn-sm",
          {on: {click: [onRemoveMeasurement, measurement.id]}}, "Remove Measurement")
      ])
    ]);

  // ...
};
```

In this case, `LabeledSlider` is the nested component. Again, notice how it is called like a regular function, passing in the model. The component itself is created outside of the `view` function and passed in as a parameter. This prevents creating the component every time the view is re-rendered; we only need to create the component once.
