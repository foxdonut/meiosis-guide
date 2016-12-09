# Receiving Proposals

When you call `propose`, Meiosis invokes the `receive` functions of all components with the latest model and the proposal. The function decides how to change the model according to the proposal, and returns the new (or same) model.

Meiosis collects changes made from `receive` functions and keeps a single root model. Each `receive` function should make changes to the model that are independent of the changes made by other `receive` functions. Whether you mutate and return the model, or use immutable objects, is for you to decide.

