# Redux

Meiosis has some inspiration from [Redux](http://redux.js.org/), by [Dan Abramov](https://github.com/gaearon).

The `receive` function of Meiosis components can be used in a similar fashion as a Redux reducer function. Whether you choose to use immutable models, or to just mutate the model and return it, is up to you. Meiosis does not impose one approach or the other.

Meiosis is also similar to Redux in adhering to the *single source of truth* principle. Meiosis collects and combines changes made from `receive` functions and merges them into a single root model.

Besides not requiring immutable models, Meiosis also differs from Redux in also being more flexible in where side-effects are executed. Again, because the best approach depends on each application, you are free to choose the most suitable for your needs.
