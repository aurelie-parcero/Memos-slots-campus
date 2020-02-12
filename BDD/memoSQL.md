# BDD

## Principales commandes SQL

### SELECT

Permet de sélectionner les champs à afficher:

```
SELECT `nom_du_champ` 
FROM `nom_du_tableau`
```


### FROM

S’utilise en complément à une requête utilisant SELECT.
Permet d'indiquer la table depuis laquelle les données vont être extraites.


### WHERE


S’utilise en complément à une requête utilisant SELECT.
Permet d'exprimer la condition de recherche de données.

```
SELECT `nom_du_champ` 
FROM `nom_du_tableau`
WHERE (`nom_du_champ` > 'condition')
```


### AND / OR


L’opérateur AND permet de s’assurer que la condition1 ET la condition2 sont vrai :

```
SELECT `nom_colonnes`
FROM `nom_table`
WHERE (`condition1`) AND (`condition2`)
```

L’opérateur OR vérifie quant à lui que la condition1 OU la condition2 est vrai :

```
SELECT `nom_colonnes` 
FROM `nom_table`
WHERE (`condition1`) OR (`condition2`)
```

Ces opérateurs peuvent être combinés à l’infini et mélangés. L’exemple ci-dessous filtre les résultats de la table “nom_table” si condition1 ET condition2 OU condition3 est vrai :

```
SELECT `nom_colonnes` 
FROM `nom_table`
WHERE `condition1` AND (`condition2` OR `condition3`)
```

### UPDATE

Permet de modifier des valeurs dans les tables

```
UPDATE `nom_table`
SET `nom_colonne1` = 'value-1', `nom_colonne2` = 'value-2'
WHERE `nom_colonne` = `oldvalue`
```

### DELETE

Permet de supprimer des données

```
DELETE FROM `nom_table` 
WHERE `nom_colonne` = `value_to_delete`
```

### INSERT

Insert des données dans la table choisie

```
INSERT INTO `nom_table` (`nom_colonne1`, `nom_colonne2`, `nom_colonne3`)
VALUES ('value-1', 'value-2', 'value-3')
```

### DATEDIFF()

Permet de déterminer l’intervalle entre 2 dates spécifiées.

```
SELECT DATEDIFF( 'date1', 'date2' );
```

Pour que le résultat soit positif il faut que la date1 soit plus récente que la date2.


### TIMEDIFF()


Permet de calculer la différence entre 2 heures distinctes. Les 2 arguments de la fonction peuvent soit être des heures (TIME) ou des dates avec heure (DATETIME), le résultat sera une heure comprise entre “-838:59:59” et “838:59:59”.

```
SELECT *
FROM `table_journaliere`
WHERE TIMEDIFF(CURTIME(), 'date_ajout') < "00:30"
```


### COUNT()

Permet de compter le nombre d’enregistrement dans une table. Connaître le nombre de lignes dans une table est très pratique dans de nombreux cas, par exemple pour savoir combien d’utilisateurs sont présents dans une table ou pour connaître le nombre de commentaires sur un article.
```
SELECT COUNT(*) FROM table
```
On peut rajouter des conditions:
```
SELECT COUNT(*) FROM utilisateur WHERE nombre_achat > 0
```

**Utilisation de COUNT(DISTINCT colonne)**

L’utilisation de la clause DISTINCT peut permettre de connaître le nombre de villes distinctes sur lesquels les visiteurs sont répartit. La requête serait la suivante :
```
SELECT COUNT(DISTINCT ville) FROM utilisateur
```

### NOT IN

Permet d'exclure des données d'une recherche en effectuant une recherche imbriquée.

```
SELECT `Auteur_Pseudo`
FROM `article`

WHERE `Auteur_Pseudo` NOT IN (SELECT commentaire.Auteur_Pseudo
FROM `commentaire`)  // Liste les auteurs ayant rédigé un article mais pas de commentaire
```