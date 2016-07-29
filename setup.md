# The Setup Function

In the [previous section](creating_the_view.md), we saw how to use the `view` function to create the view from the model and return JSX, a virtual DOM object, an HTML string, and so on. For reactive template libraries such as [Vue](http://vuejs.org) and [Riot](http://riotjs.com), however, it makes more sense to create components using the functions provided by those libraries.

In order to use the `propose` function or `actions` object within those components, use the `setup` function. Meiosis will call this function on startup, passing `propose` or `actions`, making it the perfect place to create components.

## Setting Up Vue Components

For example, the Vue todo-list [main component](https://github.com/foxdonut/meiosis-examples/blob/master/examples/todo-list/todoMain/component-vue.js) uses `setup` to create Vue components:

```javascript
const setup = actions => {
  createTodoForm(actions);
  createTodoList(actions);

  Vue.component("todo-main", {
    props: ["store"],
    template: `<div>
      <todo-form :todo="store.todo"></todo-form>
      <todo-list :todos="store.todos" :message="store.message"></todo-list>
    </div>`
  });
};

// createTodoForm:
export default function(actions) {
  Vue.component("todo-form", {
    props: ["todo"],
    template: `
      <form>
        <!-- ... -->
        <div>
          <button v-on:click.prevent="onSave(todo)">Save</button>
          <button v-on:click.prevent="onCancel">Cancel</button>
        </div>
      </form>
    `,
    methods: {
      onSave: actions.saveTodo,
      onCancel: actions.clearForm
    }
  });
}

// similarly for createTodoList...
// ...

// back in the main component:
return createComponent({
  ...,
  setup: setup,
  ...
})
```

## Using the Vue Renderer

Because Vue takes care of refreshing the view when the model changes, the renderer for Vue works differently than the ones for virtual DOM libraries. Instead of giving the renderer a DOM element and root component, you specify the model object and the root property of that model:

```javascript
import { run } from "meiosis";
import { renderer } from "meiosis-vue";
const model = { store: { ... } };
const render = renderer(model, "store")
run(render);
```

Thus for Vue it is recommended to have a single root property in your model.

## Setting Up Riot Components

Riot components are set up in a similar fashion, using calls to `riot.tag`:

```javascript
export default function(actions) {
  riot.tag("todo-form", `
    <form>
      <!-- ... -->
      <div>
        <button class="btn btn-primary btn-xs" onclick="{ onSave }">Save</button>
        <button class="btn btn-danger btn-xs" onclick="{ onCancel }">Cancel</button>
      </div>
    </form>
  `, function() {
    const getTodo = evt => serialize(evt.target.form, { hash: true, empty: true });
    this.onSave = evt => actions.saveTodo(getTodo(evt));
    this.onCancel = actions.clearForm;
  });
}
```

## Using the Riot Renderer

The Riot renderer is only slightly different than the ones for virtual DOM libraries. Instead of calling `renderer()` with no arguments, specify the name of the root tag of the application. Then, call `intoId` as with the other renderers:

```javascript
const todoMain = todoMainComponent();
const renderRoot = run(renderer("todo-main").intoId(document, "app"), todoMain);
```

As with Vue, for Riot it is recommended to have a single root property in your model.
