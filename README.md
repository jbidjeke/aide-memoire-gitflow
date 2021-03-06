# AIDE MEMOIRE GIT FLOW

# Git flow, les features et les mises en prod
 
https://danielkummer.github.io/git-flow-cheatsheet/index.fr_FR.html




## Créer une feature

* git checkout master
* git pull origin master

### Créer toujours votre branche depuis la branche "develop"

* git checkout develop
* git pull origin develop

* git flow feature start MYFEATURE

cas pratique :
git flow feature start voicematch-S11 

Message
```txt
Switched to a new branch 'feature/voicematch-S11'

Summary of actions:
- A new branch 'feature/voicematch-S11' was created, based on 'develop'
- You are now on branch 'feature/voicematch-S11'

Now, start committing on your feature. When done, use:

     git flow feature finish voicematch-S11
```

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

### Le numéro de release dépend du projet

* git flow release start  v<numero de version incrémenté>

### Modifier les fichiers ainsi que la version
* git add <fichiers modifiés> 
* git commit
 
####  Merger la branche de travail, s'il existe, sur la release
* git checkout MYFEATURE 
* git rebase develop 

* git checkout v<numero de version incrémenté>
* git merge MYFEATURE

* git flow release finish 'v<numero de version incrémenté>'
* git push origin develop

* git checkout master
* git push origin master

### Si Git râle, lancer la commande suivante:

* git push  -f origin master --tags





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
* git status
* git log
	pour vérifier que vos modifications sont bien en premier
* git push origin master




  
  
  
 

### Serveurs de production

*git pull origin master
*git log
	Pour vérifier que tout est ok
