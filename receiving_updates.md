# Receiving Updates

When you call `actions.sendUpdate`, Meiosis calls the `receiveUpdate` functions of all components with the latest model and the update that was sent. The function decides how to change the model according to the update, and returns the new (or same) model.

The `receiveUpdate` function of Meiosis components can be used in a similar fashion as a [Redux](http://redux.js.org/) reducer function. However, unlike Redux, whether you should use immutable models, or just mutate the model and return it, is up to you. Meiosis does not impose one approach or the other. Also, the `receiveUpdate` function is analogous to SAM's `model.present`.

Meiosis collects and combines changes made from `receiveUpdate` functions and merges them into a single root model. There is a default implementation for performing the merge of objects; you can easily replace this with a different implementation. See the [Initial Model](initial_model.md) section for more details.

## Refusing Updates

In some situations, you may want to *refuse* an update.
