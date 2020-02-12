# GIT-memo

## COMMANDES GIT

Utilisation du terminal GitBash.

Commandes de base de la console:

* ### pwd

affiche le répertoire courant.

* ### cd
permet de changer de répertoire.

* ### ls
permet de lister un répertoire.

* ### ls -l
Permet un affichage détaillé du répertoire (permissions d'accès, le nombre de liens physiques, le nom du propriétaire et du groupe, la taille en octets, et l'horodatage)

* ### cat <nom du fichier>
Permet d'afficher le contenu du fichier.

* ### mv        
Déplacer ou renommer un fichier, un repository...

* ### rm        
Remove files from the working tree and from the index

* ### Git init
Permet de créer un nouveau dépôt Git.

* ### Git add       
Ajouter un fichier dans le répertoire local de l'index.

* ### Git commit
Permet de valider les modifications apportées au HEAD.

* ### Git push
Envoie les modifications locales apportées à la branche principale associée
   
* ### Git status
Affiche la liste des fichiers modifiés ainsi que les fichiers qui doivent encore être ajoutés ou validés. 

* ### Git checkout
Peut être utilisé pour créer des branches ou pour basculer entre elles. Egalement pour revenir à un commit antérieur.
   Pour créer une branche: git checkout -b <nom-branche>
   Pour passer d’une branche à une autre: git checkout <nom-branche>
   Pour revenir à un commit: git checkout <nom du commit>

* ### Git remote
Permet à un utilisateur de se connecter à un dépôt distant.

   Répertorier les dépôts distants actuellement configurés: git remote –v
   Connecter le dépôt local à un serveur distant: git remote add origin <93.188.160.58>
   
* ### Git pull
Pour fusionner toutes les modifications présentes sur le dépôt distant dans le répertoire de travail local.

* ### Git tag
Le marquage est utilisé pour marquer des commits spécifiques avec des poignées simples. 
Marque le commit sur lequel on se trouve.
Ou: git tag <nom du tag> <insert-commitID-here>?

* ### Git log
Génère le log d’une branche = affiche tout les commits de la branche.

* ### Git branch
Répertorie toutes les branches présentes dans le dépôt.
    Pour supprimer une branche: git branch -d <nom branche>


## ISSUES

* Si l'issue à traiter semble correct, créer en local les fichiers à rajouter. Il faut les push (add+commit+push) sur une nouvelle branche (créer une nouvelle branche puis checkout pour se déplacer vers la branche).
* Sur GitHub, aller sur l'issue et "Compare request"
* Pour résoudre l'issue, dans le commentaire: "fixes #IDissue"
* Merge les branches puis supprimer la dernière branche vide.
* L'issue est cloturée!



* ### Editeur de texte GitBash
Pour insérer du texte: i (comme insertion)
Pour sortir de l'insertion de texte: echap
Pour sortir en enregistrant: :x