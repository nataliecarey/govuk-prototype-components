# GOV.UK Prototype Components · [![test](https://github.com/x-govuk/govuk-prototype-components/actions/workflows/test.yml/badge.svg)](https://github.com/x-govuk/govuk-prototype-components/actions/workflows/test.yml)

GOV.UK Prototype Components contains the code you need to use common or experimental components that are not yet in the GOV.UK Design System.

These components are currently experimental and more research is needed to validate them.

| Component | Description |
| - | - |
| [xGovukAutocomplete](https://x-govuk.github.io/govuk-prototype-components/autocomplete/) | Implements the [Accessible autocomplete pattern](https://github.com/alphagov/accessible-autocomplete) to enhance a fixed list of options provided by a `<select>` element. |
| [xGovukMasthead](https://x-govuk.github.io/govuk-prototype-components/masthead/) | Implements the masthead component [used on many GOV.UK product pages](https://github.com/alphagov/product-page-example). |
| [xGovukPrimaryNavigation](https://x-govuk.github.io/govuk-prototype-components/primary-navigation/) | Implements the primary navigation component used on the GOV.UK Design System website. |
| [xGovukRelatedNavigation](https://x-govuk.github.io/govuk-prototype-components/related-navigation/) | Implements [related navigation component](https://components.publishing.service.gov.uk/component-guide/related_navigation) found in the `govuk_publishing_components` gem. |
| [xGovukSubNavigation](https://x-govuk.github.io/govuk-prototype-components/sub-navigation/) | Implements the sub navigation component used on the GOV.UK Design System website. |
| [xGovukSummaryCard](https://x-govuk.github.io/govuk-prototype-components/summary-card/) | Implements a component [proposed for inclusion in the GOV.UK Design System](https://github.com/alphagov/govuk-design-system-backlog/issues/210). |
| [xGovukTaskList](https://x-govuk.github.io/govuk-prototype-components/task-list/) | Implements the [task list page pattern documented on the GOV.UK Design System](https://design-system.service.gov.uk/patterns/task-list-pages/). |

Two JavaScript-only modules are also provided:

| Module | Description |
| - | - |
| [Edge](https://x-govuk.github.io/govuk-prototype-components/edge/) | Define the edges of your prototype for research. |
| [Warn on unsaved changes](https://x-govuk.github.io/govuk-prototype-components/warn-on-unsaved-changes/) | Warn users if they try to leave a page without saving changes to a form. |

> **Note** Prior to v1.0.0, this project included a collection of decorated form components. These can now be found in the [`govuk-decorated-components`](https://github.com/x-govuk/govuk-decorated-components) package.

## Requirements

Node.js v16 or later.

## Installation

> **Note** These components are included by default with the [GOV.UK Prototype Rig](https://x-govuk.github.io/govuk-prototype-rig/).

```shell
npm install govuk-prototype-components --save
```

## Usage with the GOV.UK Prototype Kit

Add the component imports to `app/views/layout.html`, directly after the imports from GOV.UK Frontend:

```njk
{% raw %}{% from "x-govuk/components/autocomplete/macro.njk" import xGovukAutocomplete with context %}
{% from "x-govuk/components/masthead/macro.njk" import xGovukMasthead %}
{% from "x-govuk/components/primary-navigation/macro.njk" import xGovukPrimaryNavigation %}
{% from "x-govuk/components/related-navigation/macro.njk" import xGovukRelatedNavigation %}
{% from "x-govuk/components/sub-navigation/macro.njk" import xGovukSubNavigation %}
{% from "x-govuk/components/summary-card/macro.njk" import xGovukSummaryCard %}
{% from "x-govuk/components/task-list/macro.njk" import xGovukTaskList %}{% endraw %}
```

To initialise those components which use JavaScript, add the following line to `app/assets/javascript/application.js`:

```diff
  window.GOVUKPrototypeKit.documentReady(() => {
    // Add JavaScript here
+   window.GOVUKPrototypeComponents.initAll()
  })
```

## Advanced usage

### CSS

To import all the Sass rules from GOV.UK Prototype Components, add the following to your Sass file:

```scss
@import "node_modules/govuk-prototype-components/x-govuk/all";
```

You can also import Sass rules for an individual component. For example, to import styles for the masthead component, add the following to your Sass file:

```scss
@import "node_modules/govuk-prototype-components/x-govuk/components/masthead/masthead";
```

### JavaScript

To import the JavaScript for the GOV.UK Prototype Components, you can either:

* add the GOV.UK Prototype Components JavaScript file to your HTML
* import the JavaScript using a bundler like [Webpack](https://webpack.js.org/)

#### Add the JavaScript file to your HTML

If you decide to add the JavaScript to your HTML, first either:

* set up your routing so that requests for the JavaScript file are served from `node_modules/govuk-prototype-components/x-govuk/all.js`
* copy the `node_modules/govuk-prototype-components/x-govuk/all.js` file into your application

Then import the JavaScript file before the closing `</body>` tag of your HTML page or page template, and run the `initAll` function to initialise all the components.

```html
<body>
  ...
  <script src="<YOUR-APP>/<YOUR-JS-FILE>.js"></script>
  <script>
    window.GOVUKPrototypeComponents.initAll()
  </script>
</body>
```

#### Import JavaScript using ES modules

If you decide to import using a bundler, use `import` to import all GOV.UK Prototype Components, then run the `initAll` function to initialise them:

```js
import { initAll } from 'govuk-prototype-components'

initAll()
```

You can also import the JavaScript for an individual component. For example, to import the autocomplete component, add the following to your JavaScript file:

```js
import { Autocomplete } from 'govuk-prototype-components'

const myAutocomplete = document.querySelector('#my-autocomplete')
new Autocomplete(myAutocomplete).init()
```

#### Import JavaScript using Common JS

If you’re using a bundler that uses CommonJS (like [Browserify](http://browserify.org/)), use `require`:

```js
const GOVUKPrototypeComponents = require('govuk-prototype-components')

GOVUKPrototypeComponents.initAll()
```

It is not possible to import individual components using CommonJS.
