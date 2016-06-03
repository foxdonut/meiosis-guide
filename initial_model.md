# Initial Model

When you create a component, you can set its initial model with the `initialModel` property. Like all properties for `Meiosis.createComponent`, it is optional. If unspecified, an empty object, `{ }` is used as the default.

In applying the *single model* principle, the initial models of all components are merged together into *the* single root model.

By default, models are merged together using [the Object.assign polyfill from Mozilla](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Object/assign#Polyfill). You can replace this with another implementation of your choice:


```javascript
var adapters = {
  render: meiosisReact.renderer.renderIntoId("app"),
  merge: function(target, source) {
    var merged = // implementation goes here...
    return merged;
  }
};
var Meiosis = meiosis.init(adapters);
```

Some possibilities include `Object.assign`, [Ramda's merge function](http://ramdajs.com/0.21.0/docs/#merge), [Lodash's assign function](https://lodash.com/docs#assign), and [this npm clone package](https://www.npmjs.com/package/clone).
