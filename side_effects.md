# Side Effects

Actions propose values to the `receive` function, which in turn changes the model. Actions can also have side effects: typically, making requests to a server and receiving a response. These side effects happen asynchronously. Where should these be triggered, and how do we handle the response?

## Where To Perform Side Effects

Where to perform side effects is an ongoing debate with different solutions being proposed by different frameworks and libraries. As I said initially about best practices, the answer is "it depends". Use what works best for you. Meiosis is flexible enough to let you do that.

In the [todo-list with server example](https://github.com/foxdonut/meiosis-examples/tree/master/examples/todo-list), the details making server requests are encapsulated in [services](https://github.com/foxdonut/meiosis-examples/blob/master/examples/todo-list/todoMain/services.js). Then, these side effects are performed in the [actions](https://github.com/foxdonut/meiosis-examples/blob/master/examples/todo-list/todoMain/actions.js). Because of the asynchronous nature of those actions, we have the opportunity (if we wish; it is not required) to `propose` something right away, and then `propose` again when we receive the response. The view can display a message to the user ("please wait...") until we get the response.

Doing this is quite straightforward:

```javascript
{
  loadList: () => {
    propose(Action.RequestLoadList());
    services.loadTodos.then(model => propose(Action.LoadedList(model)));
  }
}
```

Notice that there is nothing out of the ordinary here. A first call to `propose` is made. Then we get the `loadTodos` response and make another call to `propose`.

## Performing Initial Actions

Sometimes we need to perform a call to the server on application startup, such as to load data. The [todo-list with server example](https://github.com/foxdonut/meiosis-examples/tree/master/examples/todo-list) does this to load the todos from the server.

Again, this can be accomplished without anything out of the ordinary. Just call the action on startup. In Meiosis, the `ready` function is a good place to do so:

```javascript
createComponent({
  ready: actions => actions.loadList()
});
```

Because the `ready` function gets `propose` or `actions` passed in, you can use them to perform your initial actions.
