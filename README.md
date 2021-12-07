# tailwindcss-container-query

A plugin that provides CSS Container Queries.

## BEFORE STARTING

This plugin relies on [container-query-polyfill](https://github.com/GoogleChromeLabs/container-query-polyfill). **You must add it to make this plugin work.** We have to rely on polyfills until all browsers have implemented them. [see the support table](https://caniuse.com/css-container-queries)

## Installation

Install the plugin from npm:

```sh
# Using npm
npm install tailwindcss-container-query

# Using Yarn
yarn add tailwindcss-container-query
```

Then add the plugin to your `tailwind.config.js` file:

```js
// tailwind.config.js
module.exports = {
  theme: {
    // ...
  },
  plugins: [
    require('tailwindcss-container-query'),
    // ...
  ],
}
```

## Usage

Container Queries up to 10 are generated by default:

| Class | Query |
| --- | --- |
| `cq-w-4` | `@container (min-width: 64px)` |
| `cq-w-6` | `@container (min-width: 96px)` |
| `cq-w-9` | `@container (min-width: 144px)` |
| `cq-w-16` | `@container (min-width: 256px)` |
| `cq-w-22` | `@container (min-width: 352px)` |
| `cq-h-4` | `@container (min-height: 64px)` |
| `cq-h-6` | `@container (min-height: 96px)` |
| `cq-h-9` | `@container (min-height: 144px)` |
| `cq-h-16` | `@container (min-height: 256px)` |
| `cq-h-22` | `@container (min-height: 352px)` |

Utilities:

| Class | Property |
| --- | --- |
| `container-type-size` | `container-type: size` |
| `container-type-inline-size` | `container-type: inline-size` |
| `container-type-block-size` | `container-type: block-size` |
| `container-type-style` | `container-type: style` |
| `container-type-state` | `container-type: state` |

There are no any `container-name` utilities by default. You should define your own utilities in `tailwind.confij.js`.

## Example Usage

```html
<div class=" h-60 w-60 bg-gray-300 overflow-auto resize container-type-size">
  <h1 class="bg-green-300 cq-w-6:bg-yellow-400">Resize the container and see the background color change</h1>
</div>
```

`.cq-w-6:bg-yellow-400` output:

```css
@container (min-width: 96px) {
  .cq-w-6\:bg-blue-400 {
    --tw-bg-opacity: 1;
    background-color: rgb(96 165 250 / var(--tw-bg-opacity));
  }
}
```

## Using Container Names

```html
<div class=" h-60 w-60 bg-gray-300 overflow-auto resize container-type-size">
  <h1 class="bg-green-300 cq-w-sidebar-6:bg-blue-400">Resize the container and see the background color change</h1>
</div>
```

```js
// tailwind.config.js
module.exports = {
  theme: {
    containerName: {
      sidebar: 'sidebar'
    },
    // ...
  }
}
```

`.cq-w-sidebar-6:bg-blue-400` output:

```css
@container sidebar (min-width: 96px) {
  .cq-w-6\:bg-blue-400 {
    --tw-bg-opacity: 1;
    background-color: rgb(96 165 250 / var(--tw-bg-opacity));
  }
}
```

## Configuration

You can configure which values and variants are generated by this plugin under the `containerQuery`, `containerType` and `containerName` keys in your `tailwind.config.js` file:

```js
// tailwind.config.js
module.exports = {
  theme: {
    // P.S. Container Query thresholds can only be specified using pixels because of the polyfill I recommended.
    containerQuery: {
      xs: '120px',
      sm: '240px',
      md: '360px',
    },
    containerType: {
      size: 'size',
    }
  },
  variants: {
    containerName: ['responsive']
  }
}
```

## TODO

- [ ] Add tests
- [ ] Add demo