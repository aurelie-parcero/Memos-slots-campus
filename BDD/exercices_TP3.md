1. Donner le nom des cinémas lyonnais ayant projeté le ﬁlm ‘Une journée en enfer’ (NB : un cinéma lyonnais est dans une ville commençant par ‘Lyon’). 
```
SELECT DISTINCT `Nom_cinema`, `Ville`
FROM `cinema` 
INNER JOIN `salle`
ON salle.IdC = cinema.IdC
INNER JOIN `seance`
ON seance.IdC = salle.IdC
INNER JOIN `film`
ON film.IdF = seance.IdF
WHERE `Titre` = 'Une journée en enfer'
AND `Ville` like '%Lyon%'
```


2. Donner le titre de ﬁlm qui soit sorti en salle après le 01/01/1980, réalisé par un artiste néaprèsle31/12/1950danslequelajouéunacteurdontlenomderôlecontientlalettre ‘o’ et qui soit projeté dans une salle non climatisée lors d’une séance débutant à 16h30 dans un cinéma de Villeurbanne. 
```
SELECT DISTINCT `Titre`
FROM `cinema` 

INNER JOIN `salle`
ON cinema.IdC = salle.IdC

INNER JOIN `seance`
ON seance.Idc = salle.Idc

INNER JOIN `film`
ON film.IdF = seance.IdF

INNER JOIN `role`
ON role.IdF = film.IdF

INNER JOIN `artiste`
ON artiste.IdA = role.IdA

WHERE `Annee` >= '1980'
AND artiste.Annee_naissance > '1950'
AND role.Nom_Role like '%o%'
AND seance.Heure_debut = '16.30'
AND `Climatise` = 'N'
AND cinema.Ville = 'Villeurbanne'
```

3. Pour chaque ﬁlm, donner le nombre d’acteurs/d’actrices jouant dans ledit ﬁlm. Le résultat aura pour schéma (Film, NbAct) et sera trié par titre selon l’ordre alphabétique. 
```
SELECT titre AS Film, COUNT(idA) AS nbActeurs 
FROM film 
INNER JOIN role 
ON role.idF = film.idF 
GROUP BY film.idF 
ORDER BY Titre ASC
```

4. Donner la capacité moyenne pour chaque cinéma. Le résultat aura pour schéma (NomCinema, CapaMoy). 
```
SELECT cinema.nom_Cinema AS 'Nom-Cinema', AVG(capacite) AS 'CapaMoy'
FROM `salle`
INNER JOIN `cinema`
ON cinema.IdC = salle.IdC
GROUP BY cinema.Nom_cinema
ORDER BY cinema.nom_Cinema
```

5. Donner la capacité totale de chaque cinéma dont on précisera la ville. Le résultat aura pour schéma (NomCinema, Ville, CapaTot) et sera trié par capacité décroissante, puis par nom de ville selon l’ordre alphabétique. 
SELECT cinema.Nom_cinema AS 'NomCinema', cinema.Ville AS 'Ville', SUM(capacite) AS 'CapaTot'
```
FROM `salle`

INNER JOIN `cinema`
ON cinema.IdC = salle.IdC

GROUP BY cinema.Nom_cinema
ORDER BY `capacite` DESC, cinema.Ville ASC
```

6. Donner le nom et le prénom des réalisateurs qui ont déjà dirigé au moins un acteur plus âgé qu’eux. Le résultat aura pour schéma (NomPrenomReal). La solution proposée devra contenir une sous-requête corrélée.
```
SELECT DISTINCT CONCAT(realisateur.nom, ' ',realisateur.Prenom) as NomPrenomReal
FROM `film`
INNER JOIN artiste  realisateur
ON film.IdRealisateur = realisateur.IdA
JOIN role
ON role.IdF = film.IdF
join artiste Acteur
on Acteur.IdA = role.IdA
WHERE realisateur.Annee_naissance > Acteur.Annee_naissance
ORDER by realisateur.Nom DESC
```