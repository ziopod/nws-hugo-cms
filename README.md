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

Nous ajouterons quelques outils et usages supplémentaires dans le cadre de la conception d'un site professionnel.

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

Gardez à l'esprit que tout ces services proposent **une offre gratuite limité**. Cela est suffisant pour de petits sites, mais peut vous **imposer à passer sur une offre payante** dans le cas d'un usage professionnel plus intensif. N'hésiter pas à **consulter les grilles de tarifs** afin de vous renseigner sur les limites de chaque offre (à titre d'exemple Netlify facture ses services de build à la "consommation", ce qui provoque parfois des "factures surprise" quand on abuse trop des mises à jour du site (l'offre gratuite étant limité à 300 builds/mois)).

### Étape 1 : Mise en place du code source
Pour nous simplifier la tâche, nous allons utliser les ["paquets de démarrage" (starters) de Forestry](https://forestry.io/starters). Celui-ci vas nous guider pour configurer notre JAMstack.

**Rendez-vous sur la page [Starters de Forestry](https://forestry.io/starters)**, nous allons choisir le thème de démarrage Hugo "Ananke", [cliquez sur la flêche, puis sur "Hugo"](https://app.forestry.io/quick-start?repo=forestryio%2fhugo-ananke-forestry&branch=master&engine=hugo&preview=https://res.cloudinary.com/forestry-io/image/fetch/w_400,h_300,c_fill,f_jpg/https://forestry.io/img/starters/ananke.jpg).

Forestry vous invite à **choisir le fournisseur de code source**, nous choisirons "Github", une fenêtre d'authentification de Github s'ouvre, une fois connecté, choissisez un nom pour votre nouveau dépôt, puis **cliquez sur "import site to Forestry"**.

Forestry vous dirige maintenant sur **l'interface d'administration de contenu**. Celle-ci est pré-configuré avec un peu de contenu. D'ici vous pouvez créer / modifier / supprimer des pages et des articles du site et également agir sur le menu de navigation principale du site.

Jetez un œil à votre compte Github, vous devreiez y voir le nouveau dépôt créer par Forestry.

### Étape 2 : Hébergement du site

Nous allons maintenant configurer l'hébergement de notre site sur Netlify.

Connectez-vous sur https://app.netlify.com avec votre compte Github.

Vous arrivez sur votre tableau de bord, **créez un nouveau site** en cliquant sur "New site from Git", choisissez "Github". Sous le nom de votre compte Github sont listé vos projet relié à Netlify, vous ne devriez pas y voir votre projet pour le moment. **Configurez Netlify app sur votre compte Github** en cliquant sur "Configure the Netlify app on Github".

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

Documentation sur le fonctionement de Hugo avec netlify : 
 - [chez Netlify](https://docs.netlify.com/configure-builds/common-configurations/#hugo)
 - [chez Hugo](https://gohugo.io/hosting-and-deployment/hosting-on-netlify)

### Configuation du thème

Le fichier `config.yml` vous permet de configurer certains détails de votre site. Notamment : 

La configuration de **l'adresse de base du site** peut poser problème pour l'accès à certaines ressources du site tant que le nom de domaine n'est pas définitif. Pour éviter tout problème, passons cette adresse en chemin relatif : 
~~~
baseURL: "/"
~~~

**La langue du site**, indiquez que le contennu éditoriale de votre site est en français :
~~~
languageCode: "fr-fr"
~~~

Consultez le site officiel [plus d'informations sur la configuration de Hugo](https://gohugo.io/getting-started/configuration/).


### Serveur local

Pour afficher votre site en local, il sufit de récupérer avec un `git clone` ou via Github Desktop.

Via le terminal, placer le pointeur du terminal dans le repertoire de votre projet :

~~~
cd chemin/vers/votre/projet
~~~

Puis de lancer le serverur local de Hugo :
~~~
hugo server
~~~

N'oublier de préfixer la commande `hugo` avec le chemin vers votre binaire si vous utilisez le binaire de Hugo (par exemple `../hugo server` sur Macosx et Linux ou `..\hugo` sur Windows).

Ouvrez votre novigateur web à l'adresse indiqué dans le terminal (http://localhost:1313 par défaut).

## Personnalisation du thème

Il est tout à fait possible de personnalié un thème. En premier lieu il faut explorer la conception du thème afin de personnaliser le thème sans dégrader ses performances, cela permet également de mieux comprendre la conception d'un thème Hugo.

### Exploration du thème

Le thème que nos avons via Forestry est configuré sous forme de [module Hugo](https://gohugo.io/hugo-modules). Pour retrouver les sources d'origine du thème, il faut explorer le fichier de configuration `config.yml` (notez que les fichier de configuration sont parfois au format `toml`). À la 5ème linge nous voyons le code suivant : 
~~~
module:
  imports:
    - path: github.com/theNewDynamic/gohugo-theme-ananke
~~~

La valeur de `path` est le chemin des sources du thème, il suffit de le copier / cller dans la barre d'adresse d'un navigateur web pour consulter les source.

Le thème est docummenté (fichier `README.md`), cette documentation nous indique comment personnalisé utiliser et personnalisé le thème.

Nous voyons qu'il possible de [modifier la typo principale et la couleur de fond](https://github.com/theNewDynamic/gohugo-theme-ananke#update-font-or-body-classes).

Dans le fichier `config.yml`, personalisons `body_classes` en choisissant une typo et une couler compatible avec le thème : 
~~~
params:
  body_classes: baskerville bg-moon-gray
~~~

Observez le résultat sur votre serveur local.

### Modifier des fichiers de template

Hugo utilise un mécanisme de [priorité de template](https://gohugo.io/templates/lookup-order) (le Lookup Order) qui permet de sur-classer certains fichiers.

De cette manière, il est possible de remplacer n'importe quel fichier du thème par ces propres fichiers.

Modifions la page d'accueil par exemple, sur le dépôt du thème Ananke, elle se trouve dans repertoire `layouts/index.html`. Pour pouvoir la remplacer par notre page d'accueil personnaliser, nous allons créer le même ficher avec le même chemin. Hugo remplacera ainsi le fichier d'index du thème par le notre.

Dans votre repertoire local, créez le fichier `layout/index.html`, copier le code source du fichier `layouts/index.html` du thème Ananke et collez le dans votre propre fichier `index.html`.

À noter que la documentaion d'Ananke nous indique que le thème utilise le framework CSS [Tachyons](http://tachyons.io)

À la ligne 2 du fichier, modifiez cette portion de code comme ceci : 
~~~
<article class="cf ph3 ph5-l pv3 pv4-l f4 center measure-wide lh-copy mid-gray">   
  <div class="fl w-100 w-two-thirds-ns pa2">
    {{ .Content }}
  </div>
  <div class="fl w-100 w-third-ns pa2">  
    <h3>Bloc personnalisé</h3>
    <p>Hello</p>
  </div>
</article>
~~~

Nous avons supprimé la classe `tc-l` de la balise `article`, [d'après la documentation de Tachyons](http://tachyons.io/docs/typography/text-align/), `tc` est pour appliquer la propriété CSS `text-align: center`, le `-l` est pour indiquer que ce règlage ne [s'applique que sur les écrans larges](https://github.com/tachyons-css/tachyons/blob/master/src/_text-align.css).

Le balises `div` aditionnelles nous permmettent de créer deux colonnes avec [le système de grille de Tachyons](http://tachyons.io/docs/layout/grid/), une en deux tiers avec la classe `two-thirds` et une autre de 1 tier avec la classe `third`. Le suffixe `-ns` indique le réglage ne s'applique ras pas sur les petits écrans (ns = Not Small).

Note : Il est parfois nécessaire de redémarrer votre serveur local pour afficher les modification de votre thème, pour cela, faites le raccourcis `ctrl + c` dans votre terminal pour arrêter le serveur local, puis de nouveau `hugo server` pour le relancer. 

### Personnaliser le CSS

Il est possible d'ajouter son propre CSS : https://github.com/theNewDynamic/gohugo-theme-ananke#custom-css

## Objectifs

Les objectifs suivants seront évalués : 
 - [ ] installation complète fonctionnelle (Forestry, Github, Netlify) ;
 - [ ] fournir un lien vers le site généré par Netlify
   À indiquer dans la description du projet Github
 - [ ] Ajouter un bloc de texte personnalisé ;
 - [ ] ~~Ajouter une navigation de pied de page personnalisé~~ ;
 - [ ] Ajouter un logo personnalisé ;
 - [ ] ~~Rendre le bloc personnalisé éditable~~ ;
 - [ ] Ajouter un contenu original (l'image de couverture et le contenu par défaut de Ananke ne doit pas apparaître)
 - [ ] Éventuellement, personnalisé la fonte et la couleur du site via la configuration du thème.
 - [ ] Prendre soin des informations SEO (points SEO : Titre & description dela page, texte alternatif sur les images, titrage et inter-titrage de l'article, mettre en valeur des termes avec de l'italique, du gras et des liens).
