---
title: 'JavaScript'
---

Voici quelques informations sur les angliscismes usuels utilisés dans le contexte de JavaScript.

> Ces mots n'ont pas de réel équivalent en français, et nous préférons laisser leur version anglaise dans la documentation pour rester au plus près de l'usage courant.

## Event listener

Un _event listener_ est une fonction conçue pour être exécutée lorsqu'un événement est déclenché.

On peut utiliser un _event listener_ pour **changer la couleur d'un bouton** (fonction) lorsqu'on **clique** dessus.

```html
<!-- HTML standard -->
<button onclick="() => console.log('Click !')">
	Clic
</button>
```

```ts
// JavaScript vanille
const element = document.createElement('button');

element.onclick = () => console.log('Click !')
// ou
element.addEventListener('click', () => console.log('Click !'))
```

```svelte
 <!-- Svelte -->
<button on:click={() => console.log('Click !')}>
	Clic
</button>
```

Plus d'infos sur les _event listeners_ sur [le site de MDN](https://developer.mozilla.org/fr/docs/Web/API/EventTarget/addEventListener).

## Truthy / Falsy

### Falsy

Une valeur est dite _falsy_ si celle-ci peut être interprétée comme équivalente (et non pas égale) à `false`.

Les valeurs _falsy_ sont:
- `false`
- `0`
- `-0`
- `0n` (`0` en BigInt)
- `""` (chaîne de caractère vide)
- `null`
- `undefined`
- `NaN`
- `document.all`

Si une valeur est `falsy`, alors sa double négation renvoie la valeur `false`.

```ts
!!0 // false
!!null // false
!!undefined // false

// ...
```

Plus d'infos sur les valeurs _falsy_ sur [le site de MDN](https://developer.mozilla.org/en-US/docs/Glossary/Falsy) (en anglais).

### Truthy

Une valeur est dite _truthy_ si celle-ci n'est pas <span class="vo">[falsy](/docs/javascript#truthy-falsy-falsy)</span>. Toutes les valeurs qui ne sont pas celles listées juste au-dessus sont donc _truthy_.

Si une valeur est `falsy`, alors sa double négation renvoie la valeur `false`.

```ts
!!1 // true
!!{} // true
!!'dsds' // true

// ...
```

Plus d'infos sur les valeurs _truthy_ sur [le site de MDN](https://developer.mozilla.org/fr/docs/Glossary/Truthy).
