---
title: 'Web'
---

Voici quelques informations sur les angliscismes usuels utilisés dans le contexte web.

> Ces mots n'ont pas de réel équivalent en français, et nous préférons laisser leur version anglaise dans la documentation pour rester au plus près de l'usage courant.

## Bundler / Packager

Un _bundler_ (ou _packager_) est un outil de développement qui permet à une application web répartie sur plusieurs fichiers sources d'être ramenée à un nombre réduit de fichiers (voir en un unique fichier).

L'étape de _bundling_ est donc une sorte de compilation spécifique au contexte du web. C'est souvent lors de cette étape que l'on transforme notre code source pour l'optimiser pour le navigateur.

Les transformations classiques effectuées lors d'un _bundling_ sont :
- Typescript => Javascript
- JSX => Javascript
- Svelte => Javascript, HTML et CSS
- Minification
- ES20XX => ES6
- Réorganisation des dossiers et fichiers

> Vite ou Rollup sont des exemples de _bundler_.
