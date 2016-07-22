# Installation

You can install Meiosis in a variety of ways:

- using a plain `<script>` tag in your HTML page
- using [Bower](http://bower.io/)
- using [RequireJS](http://requirejs.org)
- using the [Node.js](https://nodejs.org) package manager, [npm](https://www.npmjs.com/)

Let's look at each option in more detail.

## Using a plain `<script>` tag

You can add Meiosis to your HTML page by downloading the JavaScript file from the [Meiosis builds](http://meiosis.js.org/builds) page. Save it to your project, and load it with a `<script src="..."></script>` tag.

You can then access Meiosis using the global variable `meiosis`.

## Using bower

If you have installed [Bower](http://bower.io/), you can add Meiosis to your project using:

```
bower i --save meiosis
```

You can then use Meiosis directly with a `<script>` tag as above.

## Using RequireJS

After downloading Meiosis using one of the methods above, you can also use [RequireJS](http://requirejs.org).

## Using the Node.js package manager

If you have installed [Node.js](https://nodejs.org), you can use `npm` to install Meiosis:

```
npm i --save meiosis
```

You can then load Meiosis using:

```javascript
var meiosis = require("meiosis");
```

If you are using ES6, you can also use:

```javascript
import meiosis from "meiosis";
```

or even:

```javascript
import { createComponent, run } from "meiosis";
```

You are ready to use Meiosis.
