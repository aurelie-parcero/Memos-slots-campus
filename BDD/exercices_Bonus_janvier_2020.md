Bonus 1 :
* Lister les articles (avec leur catégorie) indiquant « Sport » dans le titre

```
SELECT `Titre`, `Categorie_nomCategorie`

FROM `article`

INNER JOIN `est_categorise`

ON est_categorise.Article_Titre = article.Titre

WHERE `Titre` like '%sport%'`
```

* Lister les articles (avec leur catégorie) indiquant « Sport » dans le titre et «
Biathlon » dans le texte

```
SELECT `Titre`, `Categorie_nomCategorie`

FROM `article`

INNER JOIN `est_categorise`

ON est_categorise.Article_Titre = article.Titre

WHERE `Titre` like '%sport%'

AND `Texte` like '%Biathlon%'
```

* Lister les articles ayant « Bravo » dans le commentaire

```
SELECT `Titre`, `commentaire.Texte`

FROM `article` 

INNER JOIN `commentaire`

ON commentaire.Article_Titre = article.Titre

WHERE commentaire.Texte like '%Bravo%'
```

* Lister les articles publiés aujourd’hui et ayant « Bravo » dans le commentaire,
compléter l’affichage avec les 20 premiers caractères du commentaire

```
 SELECT `Titre`, article.Auteur_Pseudo, LEFT(commentaire.Texte, 20)

FROM `article` 

INNER JOIN `commentaire`

ON commentaire.Article_Titre = article.Titre

WHERE article.Date = '2020.01.23'

AND commentaire.Texte like '%Bravo%'
```

* Lister les articles rédigés par « Matéo » avec un commentaire ajouté par « Matéo
»
```
SELECT `Titre`, article.Auteur_Pseudo, commentaire.Auteur_Pseudo, commentaire.Texte

FROM `article` 

INNER JOIN `commentaire`

ON commentaire.Article_Titre = article.Titre

WHERE commentaire.Auteur_Pseudo = 'Matéo'

AND article.Auteur_pseudo = 'Matéo'
```

* Lister les articles avec un commentaire de plus de 20 caractères, compléter
l’affichage avec les commentaires

```
SELECT `Titre`, article.Auteur_Pseudo, commentaire.Texte

FROM `article`

INNER JOIN `commentaire`

ON commentaire.Article_Titre = article.Titre

WHERE LENGTH (commentaire.Texte) > 20`
```


Bonus 2 :
* Lister les articles ayant un commentaire dans les 2 heures suivant leur
publication

```
SELECT `Titre`, article.Date, commentaire.Date`

FROM `article`

INNER JOIN `commentaire`

ON commentaire.Article_Titre = article.Titre

WHERE DATEDIFF(article.Date, commentaire.Date) = 0

AND TIMEDIFF(article.Date, commentaire.Date) < '02:00'`
```

* Lister le titre des articles et le nombre de commentaires de chacun d’entre eux

```
SELECT article.Titre, COUNT(*)

FROM `commentaire`

INNER JOIN `article`

ON article.Titre = commentaire.Article_Titre

GROUP BY commentaire.Article_Titre
```


* Lister les articles qui n’ont pas de commentaire

```
SELECT `Titre`
FROM `article` 

WHERE article.Titre NOT IN (SELECT DISTINCT commentaire.Article_Titre
FROM `commentaire`)
```

* Lister les auteurs qui ont rédigé des articles mais pas de commentaire

```
SELECT `Auteur_Pseudo`
FROM `article`

WHERE `Auteur_Pseudo` NOT IN (SELECT commentaire.Auteur_Pseudo
FROM `commentaire`)
```