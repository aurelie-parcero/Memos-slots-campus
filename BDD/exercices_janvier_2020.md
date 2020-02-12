# BDD Etape 4 - Requêtes des données avec MySQL

## Liste des commandes SQL effectuées

Sélection sur une table :
* Lister tous les articles

```
SELECT *

FROM `articles`
```

* Lister les articles publiés depuis le « 01/01/2020 » qui ont une importance
supérieur à 2

```
SELECT *

FROM `articles`

WHERE (date > '2020-01-01')`
```

* Lister les articles visibles aujourd’hui, par date de publication décroissante

```
SELECT *

FROM `articles`

WHERE (finVisibilite >= '2020-01-01')

ORDER BY `date` DESC
```


Sélection sur plusieurs tables:
* Lister les articles avec le nom de leur catégorie

```
SELECT `Article_Titre`, `Categorie_nomCategorie`

FROM `est_categorise`
```


* Lister tous les articles de la catégorie « Loisirs »
```
SELECT `Article_Titre`, `Categorie_nomCategorie`

FROM `est_categorise`

WHERE (Categorie_nomCategorie = Loisirs)
```



* Compter les commentaires publiés par le pseudo « Matéo »
```
SELECT *

FROM `commentaire`

WHERE (Auteur_Pseudo = 'Matéo')
```


* Lister les articles rédigés par le pseudo « Valentine » ou « Matéo » (afficher
l’auteur)

```
SELECT `Auteur_Pseudo`

FROM `article`

WHERE `Auteur_Pseudo` = 'Matéo'

OR `Auteur_Pseudo` = 'Valentine'
```



* Lister les articles visibles aujourd’hui avec le nom de la catégorie et le pseudo de
l’auteur, par date de publication décroissante

```
SELECT `Auteur_Pseudo`, `Categorie_nomCategorie` , `Date`

FROM `article`

INNER JOIN `est_categorise`

ON est_categorise.Article_Titre = article.Titre

WHERE (finVisibilite >= '2020-01-22')

ORDER BY è Date` DESC
```



* Ajouter un article avec comme catégorie « Loisirs » et l’auteur qui a le pseudo «
Matéo »

```
INSERT INTO `article`(`Titre`, `Texte`, `Date, `Importance`, `Auteur_Pseudo`, `finVisibilite`) VALUES ('Mon article', 'blabla', '2020-01-22','4','Matéo','2020-02-01');

INSERT INTO `est_categorise` (`Article_Titre`, `Categorie_nomCategorie`) VALUES ('Mon article', 'Loisirs')
```


      
* Renommer le pseudo « Valentine » par « Val »
Penser à selectionner l'option "CASCADE" dans "vue relationnelle" de la table pour pouvoir mofifier des données qui sont liées à d'autres tables.

```
UPDATE `auteur`

SET `Pseudo` = 'Val'

WHERE (pseudo = 'Valentine')
```  



* Supprimer les commentaires qui n’ont que “Sans avis”

``` 
DELETE FROM `commentaire`

WHERE `Texte` = 'Sans avis'
```

* Supprimer l’auteur avec un pseudo « Matéo »

```
DELETE FROM `auteur`

WHERE `Pseudo` = 'Matéo'
```
