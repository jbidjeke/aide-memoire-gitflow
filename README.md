# AIDE MEMOIRE GITFLOW

# Git flow, les features et les mises en prod
 
https://danielkummer.github.io/git-flow-cheatsheet/index.fr_FR.html




## Créer une feature

* git checkout master
* git pull origin master

### Créez toujours votre branche depuis la branche "develop"

* git checkout develop
* git pull origin develop

* git flow feature start MYFEATURE

### Se déplacer sur la branche créée et implémenter

* git checkout feature/MYFEATURE

### A la fin des implémentattions
* git rebase develop

	Gérer le rebase
	
	Le numéro de version devra être mis lors de la release

* git log

	Vérifier que vos modifications sont bien en premier

* git status

	Vérifier que vous êtes bien sur la branche feature/MYFEATURE

* git push origin feature/MYFEATURE

si Git proteste, force:

* git push -f origin feature/MYFEATURE

* git flow feature finish MYFEATURE

Cette commande supprime la branche et vous remet sur la branche develop




## Démarrer la release de mise en production

* git checkout develop
* git pull origin develop

* git checkout master
* git pull origin master

Le numéro de release dépend du projet

* git flow release start  v<numero de version incrémenté>

Modifier le fichier contenant la version
* git add <fichiers modifiés> 
* git commit
 
Si Vous avez une branche de travail (MYFEATURE)
* git checkout MYFEATURE 
* git rebase develop 

Revenez sur la release
* git checkout v<numero de version incrémenté>
* git merge MYFEATURE

* git flow release finish 'v<numero de version incrémenté>'

* git push origin develop

* git checkout master
* git pull origin master

* git merge develop

* git push origin master --tags

Si Git râle, lancer la commande suivante:

* git push  -f origin master --tags

* Déployer sur les serveurs de production




### Créer un hotfix

Exactement le même processus, sauf que c'est démarré de **master**

* git checkout develop
* git pull origin develop

* git checkout master
* git pull origin master

	Le nom de la hotfix est le numéro de version incrémenté

* git flow hotfix start MYHOTFIX
 
    exemple :
        git flow hotfix start v4.8.32


Après correction 
* git add <fichiers modifiés>
* git commit

	
* git flow hotfix finish MYHOTFIX	

Message
```txt
Summary of actions:
- Hotfix branch 'hotfix/v4.7.9' has been merged into 'master'
- The hotfix was tagged 'v4.7.9'
- Hotfix tag 'v4.7.9' has been back-merged into 'develop'
- Hotfix branch 'hotfix/v4.7.9' has been locally deleted
- You are now on branch 'develop'

```

* git push origin develop
* git checkout master
* git push origin master

* git status
* git log

	pour vérifier que vos modifications sont bien en premier
  
  
  
 

### Serveurs de production

	git pull origin master
	git log
		Pour vérifier que tout est ok
