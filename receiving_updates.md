# Receiving Proposals

When you call `propose`, Meiosis calls the `receive` functions of all components with the latest model and the proposal. The function decides how to change the model according to the proposal, and returns the new (or same) model.

Meiosis collects and combines changes made from `receive` functions and merges them into a single root model. There is a default implementation for performing the merge of objects; you can easily replace this with a different implementation. See the [Initial Model](initial_model.md) section for more details.

## Refusing Proposals

In some situations, you may want to *refuse* a proposal. This is more than just returning an unchanged model from the `receive` function. It's also stopping the rest of the chain of functions: other `receive`s, calling the `view` function, re-rendering the view to refresh the UI, and so on.

You can tell Meiosis to refuse a proposal by returning `meiosis.REFUSE_PROPOSAL` from the `receive` function.

An example of this is in the [todomvc example](https://github.com/foxdonut/meiosis-examples/tree/master/examples/todomvc). When the user is editing an existing todo, both pressing Enter and focusing outside of the text field (triggering the `blur` event) save the todo. But pressing Enter also triggers a `blur` event after saving the todo, triggering a duplicate `saveTodo` actions. To guard against this, the `receive` function only accepts `saveTodo` if the todo is being edited. Otherwise, it returns `meiosis.REFUSE_PROPOSAL`.

Another situation where refusing a proposal may be useful is to address a long-running asynchronous action. Say the user has triggered such an action and then decides to cancel it before it has finished. Afterwards, the long-running action finally completes and triggers another proposal. The `receive` can determine that the action was cancelled, and so refuse that proposal.
