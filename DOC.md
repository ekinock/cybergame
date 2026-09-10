# Documentation

## Abstract
Ce projet a été réalisé dans le cadre de ma formation MICSI, à l'école CESI Nantes. \
Il s'intègre dans la démarche de sensibilisation aux thématiques RSE *(Responsabilité Sociale des Entreprises)*.

Le but ici était de créer un support **ludique** de sensibilisation aux enjeux de **cybersécurité** à l'intention des agents du CHUN. \
Ce jeu ne s'adresse pas à des personnes ayant une formation en informatique ; si c'est votre cas, rien ne vous empêche de vous y essayer, mais vous risquez de le trouver ennuyant et de ne pas apprendre grand chose. 

J'ai essayé, via les *4 scénarios*, de couvrir des **menaces plausibles**, mais aussi de créer des **contraintes** similaires à celles que peuvent rencontrer les utilisateurs au quotidien (conseils flous, difficultés d'identifier correctement la menace, ...).

Le but n'étant pas de sanctionner les joueurs, j'ai essayé d'intégrer des aspects *"gamifiants"* (fins alternatives, badges, situations ironiques, ...) ; tous les scénarios se finissent par un **module théorique** rapide. 

## Infrastructure
### Logiciel
Ce jeu a été fait avec Twine, qui est disponible sous 2 formats : 
- [client lourd](https://github.com/klembot/twinejs/releases)
- [version web](https://twinery.org/2/#/)

> [!NOTE]
> Lorsque l'on utilise Twine en version web, les projets sont sauvegardés localement. Je n'ai pas trouvé, à ce jour, de moyen de les synchroniser avec un navigateur sur un autre PC.\
> Pour transférer un projet, il faut soit **"Publish to File"** depuis le projet (fichier .html), soit **"Export As Twee"** (fichier .twee, utilisable par twine uniqument). On peut ensuite, depuis le **Story Bord** du second navigateur, **"Import"** les fichiers.\
> Il n'y aura cependant **pas de mises à jour dynamiques** entre les 2 navigateurs

#### Story Formats
J'utilise comme langage par défaut **SugarCube 2.37.3** pour la gestion du récit.\
Dans chaque slide, j'utilise :
- **JavaScript** : pour la gestions des variables (compteurs & aléatoire) 
- **HTML** : pour la mise en page
- **CSS** : un fichier *style.css*, situé à la racine du projet

#### Modifications post-export
J'ai modifié les récits directement depuis l'application Twine (4 projets **indépendants**).\
Les balises HTML et les références aux images sont insérées directement lors de la rédaction des différentes slides.

> [!NOTE]
> Les classes configurées dans le fichier *style.css* et les images **ne peuvent pas être chargées** lorsque les **tests** sont effectués **depuis Twine** (les chemins correspondants à des ressources plus haut dans le projet).\
> Ces aspects graphiques ne pourront être testées qu'**après export & publication** des fichiers html des scénarios.

##### Variables à modifier
- **title** *(ligne 5)* : titre du document HTML
- **tw-storydata name** : nom de l'histoire Twine - **n'apparaît pas** après publication web
- **name=generateName** : nom qui apparaitra dans le menu à gauche & sur l'onglet *(variable JS)*

## Fonctionnement/Contenu
