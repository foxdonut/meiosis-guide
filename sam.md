# The SAM Pattern

Meiosis is an implementation of the [the SAM pattern](http://sam.js.org), by [Jean-Jacques Dubray](http://www.ebpml.org/about). The nomenclature is slightly different, but the ideas are the same. You can use Meiosis as a library to support your code in using the SAM pattern.

In SAM, the View is a function of the data given to it by the State. When an action is triggered, it *presents* data to the Model. The Model decides whether to accept or refuse what is presented to it, and how to change the model accordingly.

This should sound familiar because Meiosis works in essentially the same way. Calling `propose` is the equivalent of presenting data to the Model. The `receive` function is analogous to SAM's `model.present`. The State object in SAM contains functions to indicate the current state according to the model. You can use the `state` function for the same purpose with Meiosis. Finally the `nextAction` function works in the same manner as SAM's `nap()` (next-action predicate) function.

## Rocket Launcher Example

One of the examples for the SAM pattern is the [Rocket Launcher](https://bitbucket.org/snippets/jdubray/9dgKp/sam-sample). You will find the same example implemented with Meiosis in the [meiosis-examples repository](https://github.com/foxdonut/meiosis-examples/tree/v0.9.0/examples/rocket-launcher) and [online on CodePen](http://codepen.io/foxdonut/pen/pbJRrK?editors=1010), also [with React](http://codepen.io/foxdonut/pen/PzqOGG?editors=1010), and [with Snabbdom](http://codepen.io/foxdonut/pen/rLVRPR?editors=1010).
