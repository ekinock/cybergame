# Infrastructure logicielle

## Application
Ce jeu a été fait avec Twine, une solution **open source** qui permet de créer des ***fictions interactives*** (aussi appelée *histoires non-linéaires* ou *jeux vidéos textuels*).\
Twine permet d'avoir une **représentation visuelle** de la structure hypertexte, sous la forme de *"slides"* reliées les unes aux autres par des flèches.

![Screenshot de l'interface Twine d'une histoire - On peut foire des carrés, qui représente chacun une "slide", soit une des "pages" de l'histoire (sur laquelle on pourra faire un choix). Ces carrés sont reliés par des flèches, qui représentent les slides qui peuvent apparaître ensuite, selon le choix du joueur. Une des slides est marquée d'une petite fusée, qui représente le début de l'histoire.](../images/doc1.png)

Dans le cadre de se projet, cet outil a été utilisé comme un support pour un **jeu éducatif** qui ressemble dans sa forme à un *livre dont vous êtes le héro* ; on peut cependant en imaginer beaucoup d'autres usages plus *sérieux*, comme l'utiliser pour visualiser des **workflow**, servir de **support à la prise de décision**, ...

Twine, est disponible sous 2 formats : 
- [client lourd](https://github.com/klembot/twinejs/releases)
- [version web](https://twinery.org/2/#/)

> [!WARNING]
> Lorsque l'on utilise la version web, les données sont sauveggardées localement.\
> Il est possible de les transférer en effectuant un export *(voir [Section exploitation](./05-exploitation.md#données))*, mais cette méthode ne permet pas de synchronisation dynamique.


## Architecture
Chaque scénario est **indépendant**, c'est à dire que chacun correspond à une histoire (= un projet Twine) **différent**.\
Cela se matérialise, dans l'architecture globale du projet *(voir [README](../README.md#architecture))*, par le fait que chaque scénario ait **son dossier**, dans lequel est situé un fichier *index.html* (qui correspond au contenu du scénario).\
Ce fichier a été **généré directement par Twine**. 

### Structure des histoires

Chaque histoire est structurée de la manière suivante : 
- **événement** : réception d'un mail, apparition d'un besoin IT urgent, ...
- **choix de la manière de traiter la situation** : en demandant conseil, faisant des recherches, ...
- **traitement de la situation** : réalisation, ou non, de l'action demandée par les pirates
- **apparition des premières conséquences** : à ce moment là, le joueur peut encore essayer de limiter l'impact de l'attaque, mais il est trop tard pour l'empêcher. S'il a fait les bons choix, cette étape sera passée automatiquement
- **fin** : différente selon les choix
- **badges obtenus** : selon ses choix, le joueur peut débloquer différents badges
- **module théorique** : identique pour tous les scénarios. Le but est de donner quelques éléments théoriques pour aider les utilisateurs à s'en sortir mieux la fois suivante. Cette partie **ne dépend pas** des choix effectués

Tous les scénarios sont basés sur **la même trame**, même si des détails peuvent différer (pour maintenir un cohérence dans le récit).

#### Variables
La première slide (ou *"passage"*), appelée ***InitVar***, est invisible pour les joueurs.\
C'est sur celle-ci que sont initialisées les variables (JS). 

![Screenshot de l'interface Twine, centré sur la slide "InitVar" - On peut y voir le nom de la slide (InitVar), en gris clair le début du contenu de la slide (code javascript),ainsi qu'une petite fusée, qui marque la première slide du scénario, ici "InitVar".](../images/doc2.png)

*Contenu de InitVar :*
```javascript
<<set $CAU = 0>>
<<set $AMI = 0>>

<<goto "Première slide du récit">>
```
> [!IMPORTANT]
> Si les variables sont des **compteurs** qui s'implémente en fonction des choix du joueur, il est essentiel de les initialiser au début de chaque session de jeu, sinon les scores pourraient avoir des comportements difficillement prévisibles.

Ici, les variables sont utilisées pour **permettre l'obtention de badges** par le joueur ; c'est un fonctionnalité ludique, mais **secondaire**.\
Il aurait également été possible de concevoir un **système de scoring** par cette intermédiaire, ou des les utiliser pour gérer l'apparition d'**évenements aléatoires**.

## Code
J'utilise comme langage par défaut **SugarCube 2.37.3** pour la gestion du récit.\
Dans chaque slide, j'utilise :
- **JavaScript** : pour la gestions des variables (compteurs & aléatoire) 
- **HTML** : pour la mise en page
- **CSS** : un fichier *style.css*, situé à la racine du projet *(extérieur à Twine)*

### Navigation d'une slide à l'autre




### Gestion des variables
#### Comportements aléatoires


### Graphismes





