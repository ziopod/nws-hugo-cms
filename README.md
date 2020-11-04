# NWS la JAMstack

## Définition d'une JAMstack
https://jamstack.org/why-jamstack/
La JAMstack est une architecture de design qui met l'accent sur : 
- la sécurité informatique (site servi sans code dynamique) ;
- l'économie de ressources (resources composé à partir de micro-services [SaaS](https://fr.wikipedia.org/wiki/Software_as_a_service)) ;
- la performance (fichier distribué via [CDN](https://jamstack.org/why-jamstack/)) ;
- la facilité de maintenance (le site généré est stable, les modifications de codes n'impacte que la génération, jamais le site en production) ;
- la portabilité (l'essentiel du site étant composé de fichier HTML, il n'est plus nécessaire d'avoir des infrastrucures d'hébergements complexe) ;
- l'éxpérience de conception (en faisant appel à plusieurs petits outils et services, il est simple d'en expérimenter de nouveau et d'en remplacer certains).

## Choix technologiques
Pour cet exercice nous composerons notre liste technique (notre stack) d'outils est de services le plus simple possible à prendre en main.

Les besoins minimum pour géré et publier un site personnel sont :

1. générer le site (n'importe quel générateur statique);
2. héberger le site (n'importe quel herbergeur web).

On peut se contenter d'installer un générateur de site statique localement, produire les fichiers du site, puis de les rendre dispnible en les téléversant sur un serveur web. Cette solution peut être accepatble pour un site personnel, mais est vite limité si le site est conçus par plusieurs personne et doit être alimenté en contenu par des personnes tierces. 

Nous jouteros quelques outils et usages supplémentaires dans le cadre de la conception d'un site professionnel.

Les besoin les plus simples pour gérer un site professionel sont :

1. permettre la collaboration et versionner le site (GIT) ;
2. gérer les données (interface CMS) ;
3. générer le site et déployer le site (service CI/CD) ;
4. hebergement performant (herbergeur CDN).

Dans le cadre de cette exercice nous utiliseros les services suivant :

- versionner et partager le code source : Github ;
- générateur de site statique : [Hugo](https://gohugo.io) ;
- générer et déployer : Netlify ;
- héberger en CDN : Netlify ;
- interface de gestion de contenu (CMS) : Forestry ;

Il est à noter que les données du site sont gérées avec le code source global du site sous forme de fichiers plats composés d'une entête ([frontmatter](https://jekyllrb.com/docs/front-matter/)) au [format YAML](https://fr.wikipedia.org/wiki/YAML) et d'un contenu au [format Markdown](https://fr.wikipedia.org/wiki/Markdown). C'est une pratique simple et qui couvre la plupart des usages pour les site web conventionnel, cette solution est disponible par défaut pour la plupart des générateur de site statique.

Cependant, le générateur de site statiques sont loin de se limiter aux fichier plat, une JAMstack est prévu pour fonctionner avec tout l'écosystème d'internet (via les interfaces API). Il est donc tout à fait possible (et recommmander) de donner de l'ampleur à son projet web en exploitant des sourcces de données provenant de services SaaS spécialisés (comme Stripe, Shopify, Contenful, Algolia, l'écosystème de Google, et à peut près tout les services web qui possédent une interface API).

## Mise en œuvre
Voyons à présent comment mettre en place la stack choisie.

### Installation de Hugo
Pour une installation simple, utiliser le binaire.
https://gohugo.io/getting-started/installing/#binary-cross-platform

### Génération d'un site

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

### Installer un thème
https://themes.gohugo.io/

### Configuration de base
~~~
baseURL = "/"
languageCode = "fr-fr"
title = "My New Hugo Site"
theme = "ananke"
~~~

### Via Forestry

Forestry permet de générer un dépôt Github avec le un installation de Hugo + unn thème le tout déjà configuré.

Les starter de Forestry : https://forestry.io/starters/

Installation de [Hugo + le thème Ananke](https://app.forestry.io/quick-start?repo=forestryio%2fhugo-ananke-forestry&branch=master&engine=hugo&preview=https://res.cloudinary.com/forestry-io/image/fetch/w_400,h_300,c_fill,f_jpg/https://forestry.io/img/starters/ananke.jpg)

Il suffit ensuite d'ajouter votre contenu depsuis Forestry.

### Usage du thème  

Forestry propose un interface graphique qui permet de modifier la plupart des contenu et des paramètres du site.

### Aperçu du site en local

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



### Deploiement sur Netlify

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

### Ressources

 - [générateur de sites statiques](https://jamstack.org/generators) ;
 - [CMS headless](https://jamstack.org/headless-cms) ;
