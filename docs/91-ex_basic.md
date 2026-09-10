# Exemple - Utilisation basique

## Passage 1 - Evenement
🚀 ***Début***

```html
L'utilisateur reçoit un mail bizarre : 
<!-- Insertion d'une image -->
<img src="/chemin/image.png">

[[ cliquer | PiratageUser]]
[[ ne pas cliquer | PiratageCollegue]]
[[ demander l'avis aux collègues | Conseil]] 
[[ signaler comme suspect | NonPiratage]]
<!-- Les différents choix s'affichent sous forme de liste au joueur
 Selon ce sur quoi il clique, il sera redirigé vers le bon passage 
 Le nom du passage cible est indiqué après le "|" -->
```
## Passage 2 - Conseil
```html
Les collègues conseillent de cliquer.
[[ cliquer | PiratageUser]]
[[ ne pas cliquer | PiratageCollegue]]
[[ signaler comme suspect & sensibiliser les collègues | NonPiratage]]
```

## Passage 3 - PiratageUser
```html
L'utilisateur s'est fait piraté.
```

## Passage 4 - PiratageCollegue
```html
L'utilisateur ne s'est pas fait piraté, mais son collègue, oui.
```

## Passage 5 - NonPiratage
```html
Personne ne s'est fait piraté.
```
