# Renderers

Meiosis provides renderers for several view libraries. You can use any other view library by implementing a renderer. As you will see, it is not difficult at all.

## The Meiosis-Render Helper

As a base for implementing a renderer, [meiosis-render](https://github.com/foxdonut/meiosis-render) is a helper that provides `intoId` and `intoSelector` by deriving them from `intoElement`. Using meiosis-render is not required, but you might find it convenient.

## The Meiosis-React Renderer

Here is the React renderer:

```javascript
import { ReactElement } from "react";
import { render } from "react-dom";
import { Component, Renderer } from "meiosis";
import { meiosisRender, MeiosisRender, RenderIntoElement } from "meiosis-render";

function intoElement<M, P>(element: Element): Renderer<M, ReactElement<any>, P> {
  return function(model: M, rootComponent: Component<M, ReactElement<any>>): any {
    return render(rootComponent(model), element);
  };
}

function renderer<M, P>(): MeiosisRender<M, ReactElement<any>, P> {
  return meiosisRender<M, ReactElement<any>, P>(intoElement);
}

export { renderer };
```

That might seem complicated because of all the TypeScript generic types. It is probably easier to look at the equivalent JavaScript code:

```javaScript
import { render } from "react-dom";
import { meiosisRender } from "meiosis-render";

const intoElement = element => {
  return function(model, rootComponent) {
    return render(rootComponent(model), element);
  };
};

const renderer = () => meiosisRender(intoElement);

export { renderer };
```

The `intoElement` function takes an element and returns a function that renders the view, given the model and root component. For React, this is done by calling `render` from `react-dom`.

Then, `renderer` is a function that returns the renderer. For convenience, we pass the `intoElement` function to `meiosisRender` and get back `intoElement` along with `intoId` and `intoSelector`.

For other examples, see: [meiosis-mithril](https://github.com/foxdonut/meiosis-mithril), [meiosis-snabbdom](https://github.com/foxdonut/meiosis-snabbdom), [meiosis-vanillajs](https://github.com/foxdonut/meiosis-vanillajs), and
[meiosis-riot](https://github.com/foxdonut/meiosis-riot).

## The Meiosis-Vue Renderer

Since Vue is a reactive template library, its [renderer](https://github.com/foxdonut/meiosis-vue) works differently. We don't re-render a view ourselves. Instead, we use `Vue.set()` to set the model, and Vue automatically takes care of re-rendering the view. The renderer is very simple:

```javascript
import Vue from "vue";

const renderer = (data, key) => model => Vue.set(data, key, JSON.parse(JSON.stringify(model[key])));

export { renderer };
```

From the top-level `data` object and the root `key` property, we return the renderer function. Notice that although that function is given the `model` and `rootComponent` from Meiosis, we only need the `model` here. Refreshing the view is just a matter of calling `Vue.set()` on the data, with the key and the model. Because the model is made observable by Vue, we can't pass it directly. We need to serialize it by stringifying it and parsing it back.

As you can see, implementing a renderer is not difficult. The code just needs to use the view library to re-render the view from the model and root component.
