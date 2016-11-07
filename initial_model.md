# Initial Model

When you launch Meiosis by calling the `run` function, you can set the initial model of your application with the `initialModel` property. If you do not, Meiosis will automatically use an empty object `{}` as the initial model.

When you create a component, *augment* the initial model with the `initialModel` property. Like all properties for `meiosis.createComponent`, it is optional.

## Using a Single Initial Model

If you have only one `initialModel` property, it becomes the initial single root model. In that case, the property can be specified when calling the `run` function. It can also be passed when calling `createComponent`; in that case, it must be a function that returns the initial model object.

## Using Multiple Initial Models

You can also have multiple components with an `initialModel` property. That can make sense when you have a component that uses properties in the model that are only for its own use. By defining `initialModel` in the component, it is easy to keep together what belongs to that component. If you later decide to remove the component, you'll be removing its `initialModel` along with it and won't leave unused properties in the model.

In applying the *single model* principle, the initial models of all components are merged together into *the* single root model. To achieve this, the `initialModel` property of `createComponent` **must be a function**. Each function receives the model as a parameter. The function should add its properties to the model and return it. Whether you do this with mutation or with immutable objects is up to you.
