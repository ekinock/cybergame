# Exemple - Ajout d'éléments graphiques

## Passage 1 - Evenement
🚀 ***Début***

```html
<!-- Twine gère nativement les balises html de base :
 - gras / italique / souligné / barré
 - titres de bases (h, h1, h2)
 - identification des paragraphes avec <p> -->

L'utilisateur reçoit un mail <i>bizarre</i> : <!-- italique -->
<img src="/chemin/image.png">

[[ cliquer | PiratageUser]]
[[ ne pas cliquer | PiratageCollegue]]
[[ demander l'avis aux collègues | Conseil]] 
[[ signaler comme suspect | NonPiratage]]
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
<s> Bravo ! </s> <!-- barré -->

Plus d'informations sur l'<a href="http://intranet.intra.chu-nantes.fr/">Intranet</a>
<!-- ajout de lien -->

[[ FIN | Fin]]
```

## Passage 4 - PiratageCollegue
```html
L'utilisateur ne s'est pas fait piraté, mais <u>son collègue, oui</u>. <!-- souligné -->

Plus d'informations sur l'<a href="http://intranet.intra.chu-nantes.fr/">Intranet</a>
<!-- ajout de lien -->

[[ FIN | Fin]]
```

## Passage 5 - NonPiratage
```html
<b>Personne</b> ne s'est fait piraté. <!-- gras -->

Plus d'informations sur l'<a href="http://intranet.intra.chu-nantes.fr/">Intranet</a>
<!-- ajout de lien -->

[[ FIN | Fin]]
```
## Passage 6 - Fin
```html
<!-- En plus des éléments HTML de base, il est possible de rajouter un .css externe
 Ce type de fichier a pour but de définir des paramètres graphiques personnalisés ... -->

<!-- ... comme les titres ... -->
<div class="t1">FIN</div>

<!-- ... les textes de couleurs ... -->
<span class=text-flot>Merci d'avoir participé !</span>

<!-- ... mais aussi le fond de la page, les menus, les polices ... etc. -->
```