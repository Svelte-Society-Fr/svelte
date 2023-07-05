---
title: 'svelte/register'
---

> Cette <span class="vo">API</span> a été retirée à partir de Svelte 4. La méthode `require` a été dépréciée car les versions actuelles de Node comprennent directement le format ESM. Utilisez un <span class="vo">bundler</span> comme Vite ou le <span class="vo">framework full-stack</span> [SvelteKit](https://kit.svelte.dev) à la place pour créer des modules Javascript à partir de composants Svelte.

Pour faire un rendu des composants Svelte avec Node.js sans étape de compilation, utilisez `require('svelte/register')`.Vous pourrez alors utiliser la syntaxe `require` pour importe tout fichier ayant l'extension `.svelte`.

```js
// @noErrors
require('svelte/register');

const App = require('./App.svelte').default;

// ...

const { html, css, head } = App.render({ answer: 42 });
```

> Le `.default` est nécessaire car Svelte convertit à partir de modules Javascript natifs en modules CommonJS reconnus par Node. Notez que si vos composants importent des modules Javascript, ils n'arriveront pas à les charger dans un environnement Node et vous devrez utilisez un <span class="vo">bundler</span> à la place.

Pour passer des options de compilation, ou pour utiliser des extensions de fichier personnalisées, appelez la méthode `register` comme une fonction :

```js
// @noErrors
require('svelte/register')({
	extensions: ['.customextension'], // defaults to ['.html', '.svelte']
	preserveComments: true
});
```
