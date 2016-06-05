# Receiving Updates

When you call `actions.sendUpdate`, Meiosis calls the `receiveUpdate` functions of all components with the latest model and the update that was sent. The function decides how to change the model according to the update, and returns the new (or same) model.

The `receiveUpdate` function of Meiosis components can be used in a similar fashion as a [Redux](http://redux.js.org/) reducer function. However, unlike Redux, whether you should use immutable models, or just mutate the model and return it, is up to you. Meiosis does not impose one approach or the other. Also, the `receiveUpdate` function is analogous to SAM's `model.present`.

Meiosis collects and combines changes made from `receiveUpdate` functions and merges them into a single root model. There is a default implementation for performing the merge of objects; you can easily replace this with a different implementation. See the [Initial Model](initial_model.md) section for more details.

## Refusing Updates

In some situations, you may want to *refuse* an update. This is more than just returning an unchanged model from the `receiveUpdate` function. It's also stopping the rest of the chain of functions: other `receiveUpdate`s, the `viewModel` and `view`, rendering the view to refresh the UI, and so on.

You can tell Meiosis to refuse an update by returning `meiosis.REFUSE_UPDATE` from the `receiveUpdate` function.

An example of this is in the [todomvc example](https://github.com/foxdonut/meiosis-examples/tree/master/examples/todomvc). When the user is editing an existing todo, both pressing Enter and focusing outside of the text field (triggering the `blur` event) save the todo. But pressing Enter also triggers a `blur` event after saving the todo, triggering a duplicate `saveTodo` update. To guard against this, the `receiveUpdate` function only accepts `saveTodo` if the todo is being edited. Otherwise, it returns `meiosis.REFUSE_UPDATE`.

Another situation where refusing an update may be useful is to address a long-running asynchronous action. Say the user has triggered such an action and then decides to cancel it before it has finished. Afterwards, the long-running action finally completes and triggers another update. The `receiveUpdate` can determine that the action was cancelled, and so refuse that update.
