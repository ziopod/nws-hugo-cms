# NWS la JAMstack

## Définition d'une JAMstack

La [JAMstack](https://jamstack.org/what-is-jamstack) est une architecture de design qui met l'accent sur : 
- la sécurité informatique (site servi sans code dynamique) ;
- l'économie de ressources (resources composé à partir de micro-services [SaaS](https://fr.wikipedia.org/wiki/Software_as_a_service)) ;
- la performance (fichier distribué via [CDN](https://jamstack.org/why-jamstack)) ;
- la facilité de maintenance (le site généré est stable, les modifications de codes n'impacte que la génération, jamais le site en production) ;
- la portabilité (l'essentiel du site étant composé de fichier HTML, il n'est plus nécessaire d'avoir des infrastrucures d'hébergements complexe) ;
- l'éxpérience de conception (en faisant appel à plusieurs petits outils et services, il est simple d'en expérimenter de nouveau et d'en remplacer certains).

Documentation : [Définition d'une JAMstack par NETlify](https://www.netlify.com/jamstack)

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
Voyons à présent comment mettre en place une JAMstack.

Nous allons avoir besoins des services suivants : 
- Versionné et distributer le code source : [Github](github.com/) ;
- Gérer le contenu : [Forestry](forestry.io) ;
- Construire et héberger le site : [Netlify](netlify.com).

Dans un premier temps, il nous faut un compte utilisateur Github, les autres service ce connecterons à travers celui-ci.

## Étape 1 : Mise en place du code source
Pour nous simplifier la tâche, nous allons utliser les ["paquets de démarrage" (starters) de Forestry](https://forestry.io/starters). Celui-ci vas nous guider pour configurer notre JAMstack.

**Rendez-vous sur la page [Starters de Forestry](https://forestry.io/starters)**, nous allons choisir le thème de démarrage Hugo "Ananke", [cliquez sur la flêche, puis sur "Hugo"](https://app.forestry.io/quick-start?repo=forestryio%2fhugo-ananke-forestry&branch=master&engine=hugo&preview=https://res.cloudinary.com/forestry-io/image/fetch/w_400,h_300,c_fill,f_jpg/https://forestry.io/img/starters/ananke.jpg).

Forestry vous invite à **choisir le frounisseur de code source**, nous choisirons "Github", une fenêtre d'authentification de Github s'ouvre, une fois connecté, choissisez un nom pour votre nouveau dépôt, puis **cliquez sur "import site to Forestry"**.

Forestry vous dirige maintenant sur **l'interface d'administration de contenu**. Celle-ci est pré-configuré avec un peu de contenu. D'ici vous pouvez créer / modifier / supprimer des pages et des articles du site et également agir sur le menu de navigation principale du site.

Jetez un œil à votre compte Github, vous devreiez y voir le nouveau dépôt créer par Forestry.

## Étape 2 : Hébergement du site

Nous allons maintenant configurer l'hébergement de notre site sur Netlify.

Connectez-vous sur https://app.netlify.com avec votre compte Github.

Vous arrivez sur votre tableau de bord, **créez un nouveau site** en cliquant sur "New site from Git", choisissez "Github". Sous le nom de votre compte Github sont listé vos projet relié à Netlify, vous ne devriez pas y voir votre projet pour le moment. **Configurez Netlify app sur voetr compte Githug** en cliquant sur "Configure the Netlify app on Github".

Une fenêtre de configuration Github s'ouvre, en bas de la page **rendez-vous à la rubrique "Repository access"**, puis choisissez "Only select repositories" et
dans le menu déroulant, **choisissez le dépôt correspondant à votre projet de site statique** et sauvegardez.

Poursuivez l'installation en selectionner vote dépôt dépuis Netlify. Dans le champ "Build command" saissisez `hugo --minify`, dans le champ "Publish directory" saisissez `public`. Cliquez sur "Deploy".

Votre site est en cours de déploiement, dans le menu "Deploys" observez **l'échec de votre déploiement** : "Production: master@{commit} Failed" (vous pouvez cliquer dessus pour voir le journal de déploiement). Ceci est dû à un soucis de compatibilité entre la version de Hugo du thème et celui de Netlify.

**Pour remédier à ce bug** nous allons ajouter un fichier de [configuration pour Netlify](https://docs.netlify.com/configure-builds/common-configurations). Sur le dépôt Github de votre projet, ajouter un fichier `netlify.toml` dans le quel vous saissisez : 
~~~
[context.production.environment]
HUGO_VERSION = "0.75.1"
~~~

Sur l'onglet "Deploys" de Netlify, observer le déploiement de votre site. Un fois faite, vous devriez obtenir "Prodcution: master@‘commit} published".

Cliquez sur le sous-domaine généré par Netlify (par ex. https://epic-jennings-c38ea0.netlify.app), votre site est en ligne !

En cas de soucis, vérifiez bien vos fichier de configurations.

Documentation sur Hugo et netlify : 
 - [chez Netlify](https://docs.netlify.com/configure-builds/common-configurations/#hugo)
 - [chez Hugo](https://gohugo.io/hosting-and-deployment/hosting-on-netlify)
