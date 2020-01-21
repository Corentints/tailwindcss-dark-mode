# Tailwind CSS Dark Mode

## Installation

```
yarn add tailwindcss-dark-mode --dev
```

Add the plugin to the `plugins` array in your Tailwind configuration.

```javascript
plugins: [
  require('tailwindcss-dark-mode')()
]
```

## Usage

Styles generated by this plugin are only used if the selector is applied to the `<html>` element. How you do that is up to you. `prefers-dark.js` is provided as an option, which is a simple script that enables dark mode based on the user's system theme.

### Available Variants

Variants for dark mode are based on [Tailwind's own variants](https://tailwindcss.com/docs/state-variants/)...

- `dark`
- `dark-hover`
- `dark-focus`
- `dark-active`
- `dark-group-hover`
- `dark-focus-within`

... and are used in the same way.

```html
<div class="bg-white dark:bg-black">
  <p class="text-black dark:text-white">
    My eyes are grateful.

    <a ... class="text-blue-300 hover:text-blue-400 dark:text-blue-700 dark-hover:text-blue-600">
      Learn more
    </a>
  </p>
</div>
```

### Enabling Variants

As with existing variants such as `hover` and `focus`, variants for dark mode must be enabled in your Tailwind configuration for any utilities that need them.

```javascript
variants: {
  backgroundColor: ['dark', 'dark-hover', 'dark-group-hover'],
  borderColor: ['dark', 'dark-focus', 'dark-focus-within'],
  textColor: ['dark', 'dark-hover', 'dark-active']
}
```

### Changing the Selector

By default, `.mode-dark` is used as the selector for dark mode. You can change this by adding the `darkSelector` key to the `theme` section in your Tailwind configuration.

```javascript
  theme: {
    darkSelector: '.mode-dark'
  }
```

Don't forget to also change the selector in `prefers-dark.js` if you are using it.

## PurgeCSS

If you are using PurgeCSS, you should either add the selector to the `whitelist` array...

```javascript
whitelist: ['mode-dark']
```

... or add `prefers-dark.js` to the `content` array.

```javascript
content: [
  '**/*.js',
  './node_modules/tailwindcss-dark-mode/prefers-dark.js',
  './or/your/own/prefers-dark.js'
]
```

Otherwise, PurgeCSS will assume that any classes related to dark mode should be removed, as the selector is only applied when the page is loaded.
