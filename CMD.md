# Commandes Git

## A installer 
si besoin
```bash
sudo dnf install git 
sudo dnf install gh
```

## Pour se loguer
### Identification
Pour les commits & tout

```bash
git config --global user.name "nom/pseudo"
git config --global user.email "ton@mail.com"
git config --global --list     # pour vérifier
```
- name : le nom/pseudo que tu veux que j'utilise **pour te créditer**. A noter que ça sera *visible dans l'historique des commit*, donc potentiellement des gens du CHU/de mon école pourront le voir apparaitre s'uls veulent fouiller un peu
- mail : idem ; ce n'est pas obligé d'être le mail lié à ton compte github, mais c'est celui qui apparaitra. **Tu peux mettre un alias** si t'as pas envie que ça traine

### Authentification
```bash
gh auth login 
# ça va te lancer un truc pour t'authentifier en graphique via HTTPS
```

```bash
? What account do you want to log into?
> GitHub.com

? What is your preferred protocol for Git operations?
> HTTPS

? Authenticate Git with your GitHub credentials?
> Yes

? How would you like to authenticate GitHub CLI?
> Login with a web browser
```
et là tu renseigne tes identifiants github normaux


## Récupérer le projet

### La première fois
```bash
cd ~/Documents
git clone https://github.com/ekinock/cybergame.git
cd ./cybergame
git switch dev-wui
git pull
```

### Mettre à jour 
```bash
cd ~/Documents/cybergame
git status
git switch dev-wui
git pull origin dev-wui
```

### Pousser les modifs locales
```bash
git add .
git commit -m "message"  # c'est obligé sinon github fait chier
git push
```

