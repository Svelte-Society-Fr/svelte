---
title: 'API de web component'
---

Les composants Svelte peuvent également être compilés en [web components (ou "custom elements")](/docs/web#web-component) en utilisant l'option `customElement: true`. Il est recommandé de spécifier un nom de balise pour le composant en utilisant la balise [`<svelte:options>`](/docs/special-elements#svelte-options) et l'attribut `customElement`.

```svelte
<svelte:options customElement="my-element" />

<!-- en Svelte 3, faire plutôt ceci :
<svelte:options tag="my-element" />
-->

<script>
	export let name = 'tout le monde';
</script>

<h1>Bonjour {name} !</h1>
<slot />
```

Vous pouvez ignorer le nom de balise pour tout composant imbriqué que vous ne voulez pas exposer et les utiliser plutôt comme des composants Svelte normaux. Il sera toujours possible de nommer ce composant au moment de son instanciation si besoin, en utilisant la <span class="vo">[props](/docs/sveltejs#props)</span> statique `element` qui contient le constructeur de <span class="vo">[web component](/docs/web#web-component)</span> et qui est disponible lorsque l'option de compilateur `customElement` est à `true`.

```js
// @noErrors
import MyElement from './MyElement.svelte';

customElements.define('my-element', MyElement.element);
// en Svelte 3, faire plutôt ceci :
// customElements.define('my-element', MyElement);
```

Une fois qu'un <span class="vo">[web component](/docs/web#web-component)</span> a été défini, il peut être utilisé comme un élément du <span class="vo">[DOM](/docs/web#dom)</span> classique :

```js
document.body.innerHTML = `
	<my-element>
		<p>Ceci est du contenu enfant</p>
	</my-element>
`;
```

Par défaut, les <span class="vo">[web components](/docs/web#web-component)</span> sont compilés avec l'option `accessors: true`, qui indique que n'importe quelle [props](/docs/basic-markup#attributs-et-props) sera exposée comme propriété de l'élément <span class="vo">[DOM](/docs/web#dom)</span> (et sera traitée comme un attribut modifiable lorsque ce sera possible).

Pour empêcher ce comportement, vous pouvez ajouter l'option `accessors={false}` à la balise `<svelte:options>`.

```js
// @noErrors
const el = document.querySelector('my-element');

// affiche la valeur courante de la propriété 'name'
console.log(el.name);

// met à jour une nouvelle valeur, mettant à jour le shadow DOM
el.name = 'everybody';
```

## Options de composant

Lorsque vous construisez un <span class="vo">[web component](/docs/web#web-component)</span>, vous pouvez définir plusieurs aspects en utilisant l'attribut `customElement` de `<svelte:options>` en tant qu'objet, et ce depuis Svelte 4. Cet objet comprend un champ `tag` requis pour définir le nom du composant, un champ `shadow` optionnel dont la valeur peut être `"none"` pour ignorer la création du [noeud fantôme racine](/docs/javascript#shadow-dom) (notez que les styles ne seront alors plus encapsulés, et que ne pourrez plus utiliser de <span class="vo">[slot](/docs/sveltejs#slot)</span>), et un champ `props` optionnel, qui a lui-même les champs suivants :

- `attribute: string`: Pour mettre à jour une <span class="vo">[props](/docs/sveltejs#props)</span> d'un <span class="vo">[web component](/docs/web#web-component)</span>, vous avez deux alternatives : soit affecter la props sur la référence de l'élément comme illustré juste au-dessus ou utiliser un attribut HTML. Pour cette dernière, le nom par défaut de l'attribut est le nom de la props en minuscules. Vous pouvez modifier ceci avec `attribute: "<nom que vous voulez>"`
- `reflect: boolean`: Par défaut, les <span class="vo">[props](/docs/sveltejs#props)</span> mises à jour ne sont pas reflétées dans le <span class="vo">[DOM](/docs/web#dom)</span>. Pour activer ce comportement, utiliser `reflect: true`.
- `type: 'String' | 'Boolean' | 'Number' | 'Array' | 'Object'`: Si vous convertissez une valeur d'attribut en valeur de <span class="vo">[props](/docs/sveltejs#props)</span> pour la refléter dans le <span class="vo">[DOM](/docs/web#dom)</span>, la valeur de la props est supposée de type `String` par défaut. Ce n'est pas toujours correct. Par exemple, pour un nombre, vous pouvez utiliser `type: "Number"`

```svelte
<svelte:options
	customElement={{
		tag: 'custom-element',
		shadow: 'none',
		props: {
			name: { reflect: true, type: 'Number', attribute: 'element-index' }
		}
	}}
/>

<script>
	export let elementIndex;
</script>

...
```

## Limitations

Les <span class="vo">[web components](/docs/web#web-component)</span> sont un bon moyen de <span class="vo">[packager](/docs/web#bundler-packager)</span> des composants pour une utilisation dans une application développée dans une autre technologie que Svelte, puisqu'ils fonctionneront avec du HTML et JavaScript natifs mais aussi avec [la plupart des frameworks](https://custom-elements-everywhere.com/). Il y a cependant des différences importantes à connaître :

- Le style est _encapsulé_, plutôt que simplement <span class="vo">[scopé](/docs/development#scope)</span>. Cela signifie que tout style défini en dehors du composant (par exemple, celui défini dans un fichier `global.css` et celui défini avec `:global(...)`) ne s'appliquera pas au <span class="vo">[web component](/docs/web#web-component)</span>
- Plutôt que d'être extrait dans un fichier `.css` séparé, le style est <span class="vo">[inliné](/docs/javascript#inline)</span> directement en tant que `string` JavaScript
- Les <span class="vo">[web components](/docs/web#web-component)</span> ne sont généralement pas faits pour être rendus côté serveur, puisque le <span class="vo">[DOM fantôme](/docs/javascript#shadow-dom)</span> est invisible tant que le code JavaScript n'est pas chargé
- En Svelte, les éléments <span class="vo">[slottés](/docs/sveltejs#slot)</span> sont rendus de manière <span class="vo">[lazy](/docs/web#lazy-loading)</span>. Dans le <span class="vo">[DOM](/docs/web#dom)</span>, le rendu est "impatient". En d'autres termes, le composant sera toujours créé même si l'élément `<slot>` est à l'intérieur d'un bloc `{#if ...}`. De la même manière, inclure un `<slot>` dans un bloc `{#each ...}` ne rendra pas l'enfant plusieurs fois
- La directive `let:` n'a aucun effet, car les <span class="vo">[web components](/docs/web#web-component)</span> n'ont aucun moyen de passer de la donnée au composant parent qui fournit le <span class="vo">[slot](/docs/sveltejs#slot)</span>
* Des <span class="vo">[polyfills](/docs/javascript#polyfill)</span> sont nécessaires pour supporter de vieux navigateurs

Lorsqu'un <span class="vo">[web component](/docs/web#web-component)</span> écrit avec Svelte est créé ou mise à jour, le <span class="vo">[DOM fantôme](/docs/javascript#shadow-dom)</span> reflète la valeur dans le rendu suivant, et non immédiatement. Ainsi, les mises à jour peuvent être groupées, et les déplacements <span class="vo">[DOM](/docs/web#dom)</span> qui détachent temporairement (mais de manière synchrone) les éléments du DOM ne déclenchent pas le démontage du composant sous-jacent.
