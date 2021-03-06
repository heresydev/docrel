# docrel [![Build Status](https://travis-ci.org/svileng/docrel.svg?branch=master)](https://travis-ci.org/svileng/docrel) [![npm version](https://badge.fury.io/js/docrel.svg)](https://badge.fury.io/js/docrel) ![Size](https://img.shields.io/badge/min%2Bgz-%3C%201KB-blue.svg)
> Slightly better document.createElement

`Docrel` is a thin wrapper for `document.createElement` that makes creating elements a bit easier. It also helps clean up your code and avoid repetition. No dependencies, no black magic (see [source](https://github.com/svileng/docrel/blob/master/src/docrel.js)).

Using `document.createElement`:

```js
let el = document.createElement("div")
el.className = "wrapper"

let input = document.createElement("input")
input.setAttribute("type", "text")

let button = document.createElement("button")
button.textContent = "Submit"

if (loading) {
  button.setAttribute("disabled", "disabled")
}

el.appendChild(input)
el.appendChild(button)
```

Using `docrel`:

```js
import {div, input, button} from "docrel"

let el = div({class: "wrapper"}, [
  input({attrs: {type: "text"}}),
  button({textContent: "Submit", attrs: {
    disabled: loading ? "disabled" : null
  }})
])
```

If `loading` returns `null` the attribute won't be set at all.

## Install
```bash
npm install docrel --save
```

## Usage
Using `createElement`, similarly to `document.createElement`:
```js
import {createElement} from "docrel"

let el = createElement("div", {
  id: "el-id",
  class: "class-a class-b",
  textContent: "I'm an HTMLElement!",
  attrs: {
    align: "center",
    "data-attr": 1
  },
  events: {
    click: () => {console.log("click!")}
  }
})
```

```html
<!-- Resulting HTML when el is appended to the DOM -->
<div id="el-id" class="class-a class-b" align="center" data-attr=1>
  I'm an HTMLElement!
</div>
```
Using the `create` function builder (uses `createElement` underneat):
```js
import {create} from "docrel"
const [div] = create("div")

let divOne = div({class: "div-a"})
let divTwo = div({class: "div-b"})
```
Or just importing the html elements directly:
```js
import {div} from "docrel"

let divOne = div({class: "div-a"})
let divTwo = div({class: "div-b"})
```

- The `class` option is a shorthand to `node.className`;
- Keys inside `attrs` are passed to `node.setAttribute`, unless key value is `null` or `undefined`;
- Keys inside `events` are passed to `node.addEventListener`;
- Returns an HTML Element object.

### Nesting / appending children

The `create`/`createElement` function supports a third parameter for appending child elements:

```js
let el = div({class: "wrapper"}, [
  div({class: "another-div"})
])
```

```html
<!-- Resulting HTML when el is appended to the DOM -->
<div class="wrapper">
  <div class="another-div"></div>
</div>
```

## Contributing
Contributions are more than welcome. Please fork the repo and send a PR with a clean, rebased branch containing your changes. Also please make sure tests are passing and update tests if necessary.

To run the project locally, you will need to `npm install` dev dependencies and then use `npm run dev` and `npm test` to transpile ES2015 code and run tests, respectively (Node.js >= 6.0 or latest). See `package.json` for more info.

## Contributors
- [@svileng](https://twitter.com/svileng)
- [@shennan](https://github.com/shennan)

## License
- docrel: [LICENSE](https://github.com/svileng/docrel/blob/master/LICENSE)
