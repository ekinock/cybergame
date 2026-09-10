# Exemple - Gestion de l'aléatoire

## Passage 1 - InitVar
🚀 ***Début***
```javascript
<<set  $transfert = 0>>
<<set  $conseil = 0>>
<<set  $clic = 0>>
<<set  $alert = 0>>
<<set  $jour = "">>
/* Toutes les variables sont initialisées à 0 */

/* Une fois fait, le navigateur redirige automatiquement vers la slide "Evenement".
Cette action n'est pas visible pour le joueur */
<<goto "Evenement">>
```

## Passage 2 - Evenement
```text
L'utilisateur reçoit un mail bizarre : 
<img src="/chemin/image.png">

[[ cliquer | RandomFin][ $clic += 1 ]]
[[ demander aux collègues & leur transférer le mail | RandomConseil][ $transfert += 1 ]] 
[[ ne pas cliquer | RandomFin]]
[[ signaler comme suspect | RandomFin][ $alert += 1 ]]
```

## Passage 3 - RandomConseil
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
```

## Passage 4 - ConseilOui
```text
Les collègues conseillent de cliquer.
[[ cliquer | RandomFin][ $clic += 1 ]] 
[[ ne pas cliquer | RandomFin]]
[[ ne pas cliquer + prévenir la DSN | RandomFin][ $alert += 1 ]]
```

## Passage 5 - ConseilNon
```text
Les collègues conseillent de ne pas cliquer.
[[ cliquer | RandomFin][ $clic += 1 ]] 
[[ ne pas cliquer | RandomFin]]
[[ ne pas cliquer + prévenir la DSN | RandomFin][ $alert += 1 ]]
```

## Passage 6 - RandomFin
```javascript
/* Si l'utilisateur a donné l'alerte : découverte de l'attaque dés lundi
Sinon : découverte de l'attaque uniquement le jeudi
(donner l'alerte = réduction de délais de détection) */
<<if $alert == 1>>
	<<set $jour = "lundi" >>
<<elseif $alert == 0>>
	<<set $jour = "jeudi" >>
<</if>> 

/* Deux variables sont utilisées : 
- _user : % de chance que l'utilisateur se soit fait pirater
- _ok : % de chance que personne ne se soit fait pirater (collègues inclus)
Par défaut tout va bien, et les différentes actions vont augmenter les risques que le user ou ses collégues se soient fait pirater.
Les probabilités diffèrent selon si le user a transféré le mail malveillant ou non, et selon si ses collègues se sont également faits duper ou non. */
<<set _cas = $transfert + "-" + $conseil>>
<<switch _cas>>
<<case "1-1">>
	<<set _user = 16>>
	<<set _ok = 76>>
	<<break>>
<<case "1-0">>
	<<set _user = 6>>
	<<set _ok = 66>>
	<<break>>
<<case "0-1">>
	<<set _user = 4>>
	<<set _ok = 44>>
	<<break>>
<<case "0-0">>
	<<set _user = 1>>
	<<set _ok = 11>>
	<<break>>
<<default>>
	<<set _user = 0>>
	<<set _ok = 100>>
	<<break>>
<</switch>>

/* La variable _r va définir l'événement aléatoire */
<<set _r = random(1,100)>>

/* Si l'utilisateur a cliqué, il a 100% de chance de s'être fait pirater */
<<if $clic == 1>> 
	<<goto "PiratageUser">>
/* Si l'utilisateur n'a pas cliqué, il a un % de chance définit plus haut (_user) de s'être fait pirater */
<<elseif $clic == 0>>
	<<if _r <= _user>>
		<<goto "PiratageUser">>
/* S'il ne s'est pas fait pirater, il y a un % de chance définit plus haut (_ok) que personne d'autre ne se soit fait pirater */
	<<elseif _r >= _ok>>
		<<goto "NonPiratage">>
/* Si l'user ne s'est pas fait pirater, mais que nous ne somme pas non plus dans le cas où personne ne s'est fait pirater, alors c'est que c'est l'un des collègues qui s'est fait avoir */
	<<else>>
		<<goto "PiratageCollegue">>
	<</if>>
<</if>>
```


## Passage 7 - PiratageUser
```text
L'utilisateur s'est fait piraté.
L'attaque a été détectée $jour.
```

## Passage 8 - PiratageCollegue
```text
L'utilisateur ne s'est pas fait piraté, mais son collègue, oui.
L'attaque a été détectée $jour.
```

## Passage 9 - NonPiratage
```text
Personne ne s'est fait piraté.
```






   