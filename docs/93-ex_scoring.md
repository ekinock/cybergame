# Exemple - Gestion des compteurs

## Passage 1 - InitVar
🚀 ***Début***
```javascript
<<set  $score = 0>>
/* Le score est initialisé à 0 */

/* Une fois fait, le navigateur redirige automatiquement vers la slide "Evenement".
Cette action n'est pas visible pour le joueur */
<<goto "Evenement">>
```

## Passage 2 - Evenement
```text
L'utilisateur reçoit un mail bizarre : 
<img src="/chemin/image.png">

[[ cliquer | Alerte][ $score += 2 ]]
[[ cliquer et inciter ses collègues à faire pareil | Alerte][ $score += 4 ]] 
[[ ne pas cliquer | Alerte][ $score += 1 ]]
[[ signaler comme suspect | Alerte]]
```

## Passage 3 - Alerte
```html
Il commence à se passer des choses suspectes.
[[ prévenir la DSN | Redirect]]
[[ ne rien faire | Redirect][ $score += 2 ]]
[[ dissuader les autres de prévenir la DSN | Redirect][ $score += 4 ]]
```

## Passage 4 - Redirect
```javascript

/* Le score sanctionne les mauvaises décisions ; plus il est haut, plus l'attaque aura été délétère pour le CHU.
La fin qu'aura le joueur dépendra de la hauteur de son score.

Cette redirection est également invisible pour le joueur. */

<<if $score <= 1>> 
	<<goto "FinNul">>
<<elseif ($score > 1 && $score <= 3)>>
	<<goto "FinFaible">>
<<elseif ($score > 3 && $score <= 5)>>
	<<goto "FinMoyen">>
<<else>>
	<<goto "FinFort">>
<</if>>
```

## Passage 5 - FinNul
```html
L'utilisateur a tout bien fait.
Pas de piratage.

Score d'impact : $score
```

## Passage 6 - FinFaible
```html
L'utilisateur a fait quelques erreurs.
Pas de piratage, mais ce n'est pas passé loin.

Score d'impact : $score
```

## Passage 7 - FinMoyen
```html
L'utilisateur a fait plusieurs erreurs.
Il a bien eu un piratage, mais les conséquences ont été limitées.

Score d'impact : $score
```

## Passage 8 - FinFort
```html
L'utilisateur a fait de nombreuses erreurs.
Le piratage a mis longtemps à être détecté ; le virus a eu le temps de se répandre, et de nombreuses données ont été volées et/ou corrompues.

Score d'impact : $score
```