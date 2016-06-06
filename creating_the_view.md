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

When you call `Meiosis.createComponent({...})`, the returned component is the view function with the `actions` object already provided. Thus it is a function of the model that you can call from other components.

## Nested components

Coming soon.
