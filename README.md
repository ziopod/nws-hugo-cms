# NWS Mise en place du CMS Hugo

Générateur de site statique Hugo : https://gohugo.io

## Installation de Hugo
Pour une installation simple, utiliser le binaire.
https://gohugo.io/getting-started/installing/#binary-cross-platform

## Génération d'un site

Générer avec la commande :
~~~
hugo new site Hello
~~~

Se rendre dans le répertoire du site :
~~~
cd Hello
~~~

Tester le site :
~~~
hugo server
~~~

## Installer un thème
https://themes.gohugo.io/

## Configuration de base
~~~
baseURL = "/"
languageCode = "fr-fr"
title = "My New Hugo Site"
theme = "ananke"
~~~

## Via Forestry

Forestry permet de générer un dépôt Github avec le un installation de Hugo + unn thème le tout déjà configuré.

Les starter de Forestry : https://forestry.io/starters/

Installation de [Hugo + le thème Ananke](https://app.forestry.io/quick-start?repo=forestryio%2fhugo-ananke-forestry&branch=master&engine=hugo&preview=https://res.cloudinary.com/forestry-io/image/fetch/w_400,h_300,c_fill,f_jpg/https://forestry.io/img/starters/ananke.jpg)

Il suffit ensuite d'ajouter votre contenu depsuis Forestry.



