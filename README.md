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
hugo serve
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
