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

[[ cliquer | RandomFin][ $score += 10 ]]
[[ cliquer et inciter ses collègues à faire pareil | Conseil][ $score += 3 ]] 
[[ ne pas cliquer | RandomFin][ $score += 3 ]]
[[ signaler comme suspect | RandomFin]]
```

## Passage 2 - Conseil
```html
Il commence à se passer des choses étranges.
[[ prévenir la DSN | PiratageUser]]
[[ ne rien faire | PiratageCollegue][ $score += 3 ]]
[[ dissuader les autres de prévenir la DSN | NonPiratage][ $score += 3 ]]
```

## Passage 3 - Redirect
```javascript
/* La variable _p est utilisée pour définir un événement aléatoire */
<<set _p = random(1,100)>>

/* Il y a :
- 30% de chances que les collègues se fassent berner par le mail et recommande au joueur de cliquer
- 70% de chances que les collègues ne se fassent pas berner par le mail et recommande au joueur de ne pas cliquer 

Encore une fois, ces actions ne sont pas visibles par le joueur, et la redirection se fait quasi instantanément. */
<<if _p <= 30>>
		<<set $conseil = 1 >>
        <<goto "ConseilOui">>
	<<else>>
		<<set $conseil = 0 >>
        <<goto "ConseilNon">>
<</if>>

<<if $score <= 1>> 
	<<goto "FinNul">>
/* Si l'utilisateur n'a pas cliqué, il a un % de chance définit plus haut (_user) de s'être fait pirater */
<<elseif $score == 0>>
	<<if _r <= _user>>
		<<goto "FinFaible">>
/* S'il ne s'est pas fait pirater, il y a un % de chance définit plus haut (_ok) que personne d'autre ne se soit fait pirater */
	<<elseif _r >= _ok>>
		<<goto "FinMoyen">>
/* Si l'user ne s'est pas fait pirater, mais que nous ne somme pas non plus dans le cas où personne ne s'est fait pirater, alors c'est que c'est l'un des collègues qui s'est fait avoir */
	<<else>>
		<<goto "FinFort">>
	<</if>>
<</if>>
```



## Passage 3 - FinNul
```html
L'utilisateur a tout bien fait.
Pas de piratage.

Score d'impact : $score
```

## Passage 3 - FinFaible
```html
L'utilisateur a fait quelques erreurs.
Pas de piratage, mais ce n'est pas passé loin.

Score d'impact : $score
```

## Passage 3 - FinMoyen
```html
L'utilisateur a fait plusieurs erreurs.
Il a bien eu piratage, mais les conséquences ont été limitées.

Score d'impact : $score
```

## Passage 3 - FinFort
```html
L'utilisateur a fait de nombreuses erreurs.
Le piratege a mis longtemps a être détecté ; le virus a eu le temps de se répandre, et des nombreuses données ont été volées et/ou corrompues.

Score d'impact : $score
```

   