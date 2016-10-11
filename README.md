# docrel
> Slightly better document.createElement

`Docrel` is a thin wrapper for `document.createElement` that makes creating elements a bit easier. It also helps clean up your code and avoid repetition. No dependencies, no black magic (see source).

Using `document.createElement`:

```js
let select = document.createElement("select")
select.classList.add("class-1", "class-2")

let option = document.createElement("option")
option.setAttribute("value", someVar)
if (someVar === selectedVar) {
  node.setAttribute("selected", "selected")
}
node.textContent = `This is ${anotherVar}`
```

Using `docrel`:

```js
import {createElement} from "docrel"

let select = createElement("select", {classList: ["class-1", "class-2"]})

let option = createElement("option", {
  attrs: {
    value: someVar,
    selected: someVar === selectedVar ? "selected" : null
  },
  textContent: `This is ${anotherVar}`
})
```

If `someVar === selectedVar` returns `null` the attribute won't be set at all.

## Install
```bash
npm install docrel --save
```

## Usage
```js
import {createElement} from "docrel"

let el = createElement("div", {
  textContent: "Text",
  classList: ["array", "of", "classes"],
  attrs: {
    align: "center",
    "data-attr": 1
  },
  events: {
    click: () => {console.log("click!")}
  }
}
```
- Keys inside `attrs` are passed to `node.setAttribute`, unless key value is `null` or `undefined`;
- Keys inside `events` are passed to `node.addEventListener`;
- Returns an HTML Element object.

## Contributing
Contributions are more than welcome. Please fork the repo and send a PR with a clean, rebased branch containing your changes. Also please make sure tests are passing and update tests if necessary.

To run the project locally, you will need to `npm install` dev dependencies and then use `npm run dev` and `npm test` to transpile ES2015 code and run tests, respectively (Node.js >= 6.0 or latest). See `package.json` for more info.

## Contributors
- [@svileng](http://twitter.com/svileng)
