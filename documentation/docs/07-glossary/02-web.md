---
title: 'Web'
---

Voici quelques informations sur les angliscismes usuels utilisés dans le contexte web.

Ces mots n'ont pas de réelle traduction en français, ou alors celle-ci n'est que très rarement utilisée. Nous préférons donc laisser leur version anglaise dans la documentation pour rester au plus près de l'usage courant.

> Cette section de glossaire est spécifique à la documentation française de Svelte, et n'existe pas dans la documentation officielle.

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

> Vite et Rollup sont des exemples de _bundler_.

## DOM

Le _Document Object Model_ (_DOM_) est la representation objet d'un document HTML chargé dans le navigateur web. Cette représentation du document permet de le voir comme un groupe structuré de nœuds et d'objets possédant différentes propriétés et méthodes. Il relie les pages web aux scripts, fichiers de styles, ressources externes ou langages de programmation. Il peut être manipulé à l'aide du JavaScript.

## Framework

> Bientôt...

## Keyframe

> Bientôt...

## Lazy loading

> Bientôt...

## Markup

> Bientôt...

## Routing

> Bientôt...

## Sourcemaps

> Bientôt...

## Server-side rendering

Le rendu côté serveur, ou _server-side rendering_ est l'action de générer l'IHM avec tout ou partie des données métiers directement par le serveur. Il est a mettre en opposition avec les pages qui viennent charger la logique dans un premier temps et les données métiers avec des requêtes supplémentaires.

Le rendu côté serveur a pour avantages :

- une exécution plus rapide car nécessitant moins de requêtes
- le fait de pouvoir générer l'entièreté d'une page à la première requête, ce qui permet d'afficher une page même si le contexte JavaScript n'est pas disponible côté client
- bénéficie d'un meilleur référencement SEO (les balises de référencements sont générés côté serveur et disponible pour les outils d'indexation)

SvelteKit mets en place le rendu côté serveur par défaut et peut être désactivé au cas par cas.

## Web component

> Bientôt...

## XSS

> Bientôt...
