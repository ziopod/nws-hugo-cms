# Personnaliser un thème avec Hugo

Passons en revue les fonctionnalités essentielles pour personnaliser un thème Hugo.

**En fonction de vos pré-requis**, il est judicieux de choisir un thème adapté. Par exemple, ne vous lancer pas dans la création d'un thème avec peu de connaissances en HTML et CSS.

Vos critère de choix pour un thème, est-que ce thème : 
 - possède un installeur automatique sur Forestry ;
 - couvre le besoin éditorial ;
 - permet une configuration du design (couleurs, layout) ;
 - exploite un framework CSS que je connais ;
 - une technologie CSS que je connais (pré ou post processeur) ;

## Configuration d'un thème

Lorsque vous ajouter un thème à Hugo, il est important de se préoccuper du fichier de configuration `config.toml`. Si votre thème est installé avec un service comme Forestry ou Netlify, un fichier de configuration en accord avec le thème est automatiquement mis en place.

Lors d'un installation manuel, il faudras vous-même préparer le fichier de configuration. 

Certains thème on besoin d'un structure spécifique de données et de certaines informations dans le fichier de configuration pour pouvoir fonctionner correctement. Ces informations sont généralement disponibles avec le code source du thème.

Chaque thème embarque un **exemple de structure de données** dans le répertore `themes/nom-du-theme/exampleSite`. Vous y trouverez un modèle de contenu dans le répertoire `content`, un modèle de données dans le répertoire `data` et un example de configuration dans le fichier `config.tom`.

Certain thèmes poussent loin la configuration, il peuvent permettret par exemple la modification de l'aspect du site (couleurs, fonctionnalités, layout, etc.)

À vous de vous appuyer sur la documentation, et sur les exemples pour configurer correctement votre thème.

## Les données

Hugo permet un grande souplesse pour classer le contenu et les disposer sur les diverses portions d'un site. Les thèmes prennent en charge les mécaniques de bases de Hugo, certains les couvrent de manière exhaustives et d'autres thèes ajoutent leurs propres mécaniques complémentaires.

Nous verrons ici un résumé des mécaniques de bases de Hugo. Pour plus de détails, consulter la documentation sur [la gestion de contenu de Hugo](https://gohugo.io/categories/content-management).

Plus d'informations sur https://gohugo.io/getting-started/directory-structure/

### Le contenu
Le contenu est géré dans le répertoire `content` sous forme de fichier texte Markdown possédant une zone de données appelé "front matter" la zone de données peut être au [format YAML](https://fr.wikipedia.org/wiki/YAML) séparé avec des triples tirets `---` ou au [format TOML](https://fr.wikipedia.org/wiki/TOML) séparé avec des tripes plus `+++`

Exemple au foramt YAML

```
---
title: "Titre méta"
draft: true
---
# Titre de la page
Contenu de la page.
```

Exemple au format TOML :
```
+++
title = "Titre méta"
draft = true
+++
# Titre de la page
Contenu de la page.
```

Les sous répertoires permettent de gérer des [sections de contenu](https://gohugo.io/content-management/sections/) disponible sous forme d'arbre de données ou de [type](https://gohugo.io/content-management/types/). 

Par exemple, un fichier placé dans un repertoire `content/blog`, pourras être seectionné à travers le type `blog` et permettra de sélectionner [les contenus placés dans le même repertoire](https://gohugo.io/content-management/sections/#section-page-variables-and-methods).

**Le [fichier `_index.md`](https://gohugo.io/content-management/organization#index-pages-_indexmd)** à un rôle spécial pour Hugo, il sert à ajouter des données à la page d'index de la section. Par exemple le fichier `content/blog/_index.md` pemettras de générer et de titrer l'url `https://example.com/blog` (la page d'index des articles du blog), d'ajouter un lien pour cette page dans le menu ou d'ajouter du contenu complémentaire à cette page d'index.

### Les archetypes 
Situés dans le repertoire `archetype`, [les archetypes](https://gohugo.io/content-management/archetypes/) sont des modèles pour les fichiers de contenue.

### Les données additionnelles
Situé dans le repertoire `data`, les données sont des fichiers au formats [JSON](https://fr.wikipedia.org/wiki/JavaScript_Object_Notation), YML ou TOML. Il permettent de stocker des données additionnelles au contenu (un bibilographie par exemple).

## La taxonomie
Hugo exploite [un système de taxonomy](https://gohugo.io/content-management/taxonomies/) que l'on peut exploiter pour organiser l'affichage de contenu. 

[Deux taxons sont configuré par défaut](https://gohugo.io/content-management/taxonomies/#default-taxonomies), des catégories (`categories`) et des étiquettes (`tags`).

[Pour associer un contenu à un taxon](https://gohugo.io/content-management/taxonomies/#add-taxonomies-to-content), il suffit de le déclarer dans le front matter de cette manière (ici le tacxn `tags`): 

```
---
title: "Titre méta"
categories: 
 - Exemple
draft: false
---
# Titre de la page
Contenu de la page.
```

## Le menu de navigation
Pour ajouter une page dans un menu de navigation Hugo, il sufit d'ajouter le paramètre `menu` dans le front matter de la page.

Par exemple, pour ajouter la page « À propos » dans la navigation principale `main` d'un thème, le fichier `content/a-propos` doit ressembler à ceci :

```
---
title: À propos
menu: main
---
```

À noter que certains thèmes ont un fonctionnement qu'il leurs sont prope pour générer les menus de navigation.