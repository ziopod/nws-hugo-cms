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

## Usage du thème  

Forestry propose un interface graphique qui permet de modifier la plupart des contenu et des paramètres du site.

## Aperçu du site en local

Synchroniser le repertoire Github du projet localement avec Githu Desktop ou en ligne de commande via le terminal.

Via le terminale, se rendre dans le repertoire du projet : 
~~~
cd ~/chemin/vers/le/projet
~~~

Lancer le serveur local :
~~~
hugo server
~~~

Après chaque modification de contenu dans Forestry, synchroniser le contenu local avec Githu Desktop ou en ligne de commande avec `git pull`.



## Deploiement sur Netlify

En préalable, spécifier un fichier de configuration pour Netlify sur votre projet.

En fonction du thème il est peut-être necessaire de précisier la version de Hugo à utiliser.
Dans ce cas, ajouter le fichier `netlify.toml` avec la configuration indiqué par le thème.

Pour le thème Ananke le contenu suivant : 

~~~
[context.production.environment]
HUGO_VERSION = "0.75.1"
HUGO_ENV = "production"
HUGO_ENABLEGITINFO = "true"
~~~

Documentation : [Netlify & Hugo configuration courante](https://docs.netlify.com/configure-builds/common-configurations/#hugo)

1. Se connecter à Netlify
2. Créer un nouveau site (depuis Netlify)
3. Selectionner le dépôt Github correspondant au projet, puis valider.

Paramètre à préciser sur le projet Netlify (deplay settings) : 
 - Build command : `hugo --minify`
 - Publish Directory : `public`

Netlify construit (build) le site statique et genère une URL.

Exemple de projet : 
Depôt Github : https://github.com/ziopod/hugo-ananke-forestry-netlify
Site sur hébergé sur Netlify : https://festive-dijkstra-b6cf85.netlify.app/
