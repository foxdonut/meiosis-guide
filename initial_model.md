# Initial Model

When you create a component, you can set its initial model with the `initialModel` property. Like all properties for `meiosis.createComponent`, it is optional. However, you do need at least one component with an `initialModel` property.

## Using a Single Initial Model

If you have only one component with an `initialModel` property, it becomes the initial single root model. In that case, the property can be the initial model object. It can also be a function that returns the initial model object.

## Using Multiple Initial Models

You can also have multiple components with an `initialModel` property. That can make sense when you have a component that uses properties in the model that are only for its own use. By defining `initialModel` in the component, it is easy to keep together what belongs to that component. If you later decide to remove the component, you'll be removing its `initialModel` along with it and won't leave unused properties in the model.

In applying the *single model* principle, the initial models of all components are merged together into *the* single root model. To achieve this, the `initialModel` property **must be a function** when you have multiple initial models. Each function receives the model as a parameter. The function should add its properties to the model and return it. Whether you do this with mutation or with immutable objects is up to you.

Note that you may use a function for the `initialModel` even when you only have a single initial model.
