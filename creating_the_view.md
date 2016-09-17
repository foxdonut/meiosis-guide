# Creating the View

In Meiosis, the `view` function returns a view object that corresponds to the library of your choice. It could be a plain string, JSX, a hyperscript object, and so on.

-----

When using reactive template libraries such as [Vue](http://vuejs.org) or [Riot](http://riotjs.com), using the `view` function is not necessary. Indeed, these libraries create components themselves, instead of returning a representation of the component. To create those components, use the `setup` function instead of `view`. We will see the `setup` function in the [next section](setup.md).

-----

## Specifying a Renderer

The way you tell Meiosis how you want to create your views is by specifying a *renderer*. Meiosis currently provides renderers for:

- VanillaJS, [meiosis-vanillajs](https://github.com/foxdonut/meiosis-vanillajs) (String concatenation or template engines such as [Handlebars](http://handlebarsjs.com)
- [React](https://facebook.github.io/react/), [meiosis-react](https://github.com/foxdonut/meiosis-react)
- [Inferno](http://github.com/trueadm/inferno), [meiosis-inferno](https://github.com/foxdonut/meiosis-inferno)
- [Snabbdom](http://github.com/paldepind/snabbdom), [meiosis-snabbdom](https://github.com/foxdonut/meiosis-snabbdom)
- [Mithril](http://mithril.js.org), [meiosis-mithril](https://github.com/foxdonut/meiosis-mithril)
- [Vue](http://vuejs.org), [meiosis-vue](https://github.com/foxdonut/meiosis-vue)
- [Riot](http://riotjs.com), [meiosis-riot](https://github.com/foxdonut/meiosis-riot)

Implementing a renderer for other libraries is easy. Refer to the [Renderers](renderers.md) section.

To specify the React renderer, write:

```javascript
var renderer = meiosisReact.renderer().intoId(document, "app");
```

Then, you just need a container with the `"app"` id in your HTML page:

```html
<div id="app"></div>
```

Meiosis will render the view into that `div`. Of course, you can use a different id. Furthermore, instead of `intoId`, you can also use:

- `intoSelector(document, selector)` for example, `".container"` with `<div class="container"></div>`
- `intoElement(document, element)` where you specify the DOM element directly. In fact, `intoId` and `intoSelector` are merely convenience functions that call `document.getElementById` and `document.querySelector` respectively, and pass the element to `intoElement`.

The VanillaJS, Inferno, Snabbdom, and Mithril renderers work in the same manner. The Vue and Riot renderers work slightly differently. We will see them in the [Setup Function](setup.md) section.

## Creating a `view` Function

Each component that you create can have a `view` function. Meiosis calls it with `(model, propose/actions)` so that you can return the view representation of the model, and call the `propose` function. If you created an `actions` object, that will be passed as a parameter instead. The view can then call functions on it.

The nature of what you return from the `view` function depends on the view library that you chose for your views. Whether you use React, Inferno, Snabbdom, Mithril, plain JavaScript, or anything else, you return an object that is compatible with the chosen library.

## Nested components

When you call `meiosis.createComponent({...})` with a `view` function, the returned component is the view function with `propose` or `actions` already provided. Thus it is a function of the model that you can call from other components.

The [todo-list example](https://github.com/foxdonut/meiosis-examples/tree/master/examples/todo-list) has a component that uses two other components, `todoForm` and `todoList`:

```javascript
import React from "react";

const view = (todoForm, todoList) => model => (
  <div>
    {todoForm(model.store.todo)}
    {todoList(model.store)}
  </div>
);
```

Notice that we can pass a sub-property of the `model` when calling a component function. Also, there is no need to pass the `propose` function or `actions` object. Meiosis will take care of that. In fact, if components have different `actions` objects, they will each get their own instance with the correct functions.

Here is another nested component from the [labeled-sliders example](https://github.com/foxdonut/meiosis-examples/blob/master/examples/labeled-sliders/sliderContainer/view.js), written with Snabbdom:

```javascript
import h from "snabbdom/h";

import { Action } from "./actions";

const view = labeledSlider => (model, propose) => {
  const onAddMeasurement = _evt => propose(Action.AddMeasurement());
  const onRemoveMeasurement = id => propose(Action.RemoveMeasurement(id));

  const renderMeasurement = (measurement, index) =>
    h("div", {key: measurement.id, style: {border: "1px solid gray"}, id: measurement.id}, [
      labeledSlider({measurement, index}),
      h("div", [
        h("button.btn.btn-danger.btn-sm",
          {on: {click: [onRemoveMeasurement, measurement.id]}}, "Remove Measurement")
      ])
    ]);

  // ...
};
```

In this case, `labeledSlider` is the nested component. Again, notice how it is called like a regular function, passing in the model. The component itself is created outside of the `view` function and passed in as a parameter. This prevents creating the component every time the view is re-rendered; we only need to create the component once.
