# The Setup Function

In the [previous section](creating_the_view.md), we saw how to use the `view` function to create the view from the model and return JSX, a virtual DOM object, an HTML string, and so on. For reactive template libraries such as [Vue](http://vuejs.org) and [Riot](http://riotjs.com), however, it makes more sense to create components using the functions provided by those libraries.

In order to use the `propose` function or `actions` object within those components, use the `setup` function. Meiosis will call this function on startup, passing `propose` or `actions`, making it the perfect place to create components.
