# Memo - Programmation orientée objet en PHP

### Classe
C'est un ensemble de variables et de fonctions (attributs et méthodes).
Le nom des classes commence par une majuscule.
```
class Personnage {      // mot-clé "class" suivi du nom de la classe
//déclaration des attributs et méthodes ici
} 
```

### Objet
C'est une <b>instance</b> de la classe à utiliser.
Pour créer un nouvel objet, il faut faire précéder le nom de la classe à <b>instancier</b> du mot-clé ``new``:

```
$perso = new Personnage;
```
Ainsi, ``$perso`` sera un objet de type ``Personnage``. On dit que l'on <b>instancie</b> la classe ``Personnage``, que l'on crée une <b>instance</b> de la classe ``Personnage``.

### Attributs
Il s'agit d'une variable. Il est possible ou non de les initialiser lors de leur déclaration.

```
class Personnage {
private $force = 50;
private $degats;
}
```

### Méthodes
Il s'agit des fonctions utilisées pour une même classe.
Elle est précédée du mot-clé ``function`` et de la visibilité de la méthode. Les types de visibilité des méthodes sont les mêmes que les attributs. Les méthodes n'ont en général pas besoin d'être masquées à l'utilisateur, le plus souvent elles seront en ``public`` (à moins qu'on tienne absolument à ce que l'utilisateur ne puisse pas appeler cette méthode, par exemple s'il s'agit d'une fonction qui simplifie certaines tâches sur l'objet mais qui ne doit pas être appelée n'importe comment).
```
class Personnage
{   
  public function deplacer() // Une méthode qui déplacera le personnage (modifiera sa localisation).
  {

  }
}
```
Pour appeler une méthode d'un objet, il va falloir utiliser un opérateur : il s'agit de l'opérateur ``->``
À gauche de cet opérateur, on place l'objet que l'on veut utiliser. 
À droite de l'opérateur, on spécifie le nom de la méthode que l'on veut invoquer.

```
$perso = new Personnage; 
$perso->parler();
```

La dernière ligne signifie donc « va chercher l'objet ``$perso``, et invoque la méthode ``parler()`` sur cet objet ».

Cet opérateur peut également servir à atteindre un attribut.

- La pseudo-variable ``$this``

Elle permet au sein d'une méthode d'attribuer implicitement un paramètre. Comme on ne peut pas accéder à une méthode ou attibut privé(e) en dehors de la classe, ``$this`` permet de représenter l'objet au sein de la classe et d'obtenir le résultat en dehors:

```
class Personnage
{
  private $experience = 50;

  public function afficherExperience()
  {
    echo $this->experience;
  }
}

$perso = new Personnage;
$perso->afficherExperience();
```
En résumé, ``$this`` est une variable représentant l'objet à partir duquel on a appelé la méthode.


Il est possible de passer un argument à une méthode:

```
// On crée deux personnages
$perso1 = new Personnage;
$perso2 = new Personnage;
    
public function frapper($persoAFrapper)
 {
   $persoAFrapper->_degats += $this->_force;
 }

// Ensuite, on veut que le personnage n°1 frappe le personnage n°2.
$perso1->frapper($perso2);
```

On peut typer la valeur demandée en paramètre, afin d'éviter les erreurs:
```
  public function frapper(Personnage $persoAFrapper)
  {
    // …
  }
}
```

- #### Les méthodes statiques

Les méthodes statiques sont des méthodes qui sont faites pour agir sur une classe et non sur un objet.

Pour déclarer une méthode statique, il faut faire précéder le mot-clé ``function`` du mot-clé ``static`` après le type de visibilité.

````
  public static function parler()
  {
    echo 'Je vais tous vous tuer !';
  }
````

Et dans le code:
````
Personnage::parler();
````

- #### Les attributs statiques

Le principe est le même, c'est-à-dire qu'un attribut statique appartient à la classe et non à un objet. Ainsi, tous les objets auront accès à cet attribut et cet attribut aura la même valeur pour tous les objets.

La déclaration d'un attribut statique se fait en faisant précéder son nom du mot-clé ``static``.

 ```
// Variable statique PRIVÉE.
  private static $texteADire = 'Je vais tous vous tuer !';
```


### Public / Private
Si un attribut ou une méthode est ``public``, alors on pourra y avoir accès depuis n'importe où, depuis l'intérieur de l'objet (dans les méthodes qu'on a créées), comme depuis l'extérieur.
 
S'il est `` private``, il y a quelques restrictions. On aura accès aux attributs et méthodes seulement depuis l'intérieur de la classe, c'est-à-dire que seul le code voulant accéder à un attribut privé ou une méthode privée écrit(e) à l'intérieur de la classe fonctionnera.

```
class Personnage {
private $force;        //On définit les attributs qui ne seront utilisables qu'à l'intérieur de la classe
private $localisation;
}
```

### Accesseurs (ou getters)

C'est une méthode dont le rôle est de renvoyer l'attribut qu'on lui demande.
```
class Personnage
{
  private $degats;
        
  // Ceci est la méthode getDegats() : elle se charge de renvoyer le contenu de l'attribut $degats.
  public function getDegats()
  {
    return $this->degats;
  }
}
```

### Mutateurs (ou setters)

Méthode permettant de modifier un attribut. Ces méthodes sont de la forme ``setNomDeLAttribut()``:

```
class Personnage
{
  private $force;

// Mutateur chargé de modifier l'attribut $force.
  public function setForce($force)
  {
    
    $this->force = $force;
  }
```

### Constructeur

C'est une méthode écrite dans la classe, qui permet d'initialiser les attributs dès la création de l'objet.

Il s'écrit comme ceci: ``__construct`` avec deux underscore au début.

Il est exécuté dès la création de l'objet et par conséquent, aucune valeur ne doit être retournée.
Une classe fonctionne très bien sans constructeur, il n'est en rien obligatoire!

```
public function __construct($force, $degats) // Constructeur demandant 2 paramètres
  {
    echo 'Voici le constructeur !'; // Message s'affichant une fois que tout objet est créé.
    $this->setForce($force); // Initialisation de la force.
    $this->setDegats($degats); // Initialisation des dégâts.
    $this->_experience = 1; // Initialisation de l'expérience à 1.
  }

$perso1 = new Personnage(60, 0); // 60 de force, 0 dégât
$perso2 = new Personnage(100, 10); // 100 de force, 10 dégâts
```

Dans le constructeur, les valeurs sont initialisées en appelant les mutateurs correspondant. En effet, si on assignait directement ces valeurs avec les arguments, le principe d'encapsulation ne serait plus respecté et n'importe quel type de valeur pourrait être assigné !

On ne met jamais la méthode ``__construct`` avec le type de visibilité ``private`` car elle ne pourra jamais être appelée, one ne pourra donc pas instancier notre classe !


### Scope Resolution Operator ``::``

Il est utilisé pour appeler des éléments appartenant à telle classe et non à tel objet. En effet, nous pouvons définir des attributs et méthodes appartenant à la classe : ce sont des éléments statiques.

Parmi les éléments appartenant à la classe, il y a aussi les constantes de classe, sortes d'attributs dont la valeur est constante, c'est-à-dire qu'elle ne change pas.

- Les constantes de classe
Une constante est une sorte d'attribut appartenant à la classe dont la valeur ne change jamais.

Pour déclarer une constante, il faut faire précéder son nom du mot-clé ``const``.

````
class Personnage
{
  // Tous les attributs en privé !
  private $force;
  private $localisation;

  // Déclarations des constantes en rapport avec la force.
  const FORCE_PETITE = 20;
  const FORCE_MOYENNE = 50;
  const FORCE_GRANDE = 80;

  public function __construct()
  {

  }

  public function deplacer()
  {

  }

  public function frapper()
  {

  }

  public function gagnerExperience()
  {

  }
}
````

Pour accéder à une constante, il faut spécifier le nom de la classe, suivi du symbole double deux points, suivi du nom de la constante. 


````
class Personnage
{
  private $force;
  private $localisation;
  private $experience;


  // Déclarations des constantes en rapport avec la force.
  const FORCE_PETITE = 20;
  const FORCE_MOYENNE = 50;
  const FORCE_GRANDE = 80;

  public function __construct($forceInitiale)
  {
    //Assigneation de la valeur d'un attribut uniquement depuis son setter !
    $this->setForce($forceInitiale);
  }

  public function deplacer()
  {

  }

  public function frapper()
  {

  }

  public function gagnerExperience()
  {

  }
  
  public function setForce($force)
  {
    // On vérifie qu'on nous donne bien soit une « FORCE_PETITE », soit une « FORCE_MOYENNE », soit une « FORCE_GRANDE ».
    if (in_array($force, [self::FORCE_PETITE, self::FORCE_MOYENNE, self::FORCE_GRANDE]))
    {
      $this->force = $force;
    }
  }
}
````

Du coup, lors de la création de l'objet:

````
// On envoie une « FORCE_MOYENNE » en guise de force initiale.
$perso = new Personnage(Personnage::FORCE_MOYENNE);
````

A noter que les constantes se notent en majuscules.



### L'hydratation

Quand on parle d'hydratation, c'est qu'on parle d'« objet à hydrater ». Hydrater un objet, c'est tout simplement lui apporter ce dont il a besoin pour fonctionner. En d'autres termes plus précis, hydrater un objet revient à lui fournir des données correspondant à ses attributs pour qu'il assigne les valeurs souhaitées à ces derniers. L'objet aura ainsi des attributs valides et sera en lui-même valide. On dit que l'objet a ainsi été hydraté.

On peut donc écrire une fonction ``hydrate()``:

````
// Un tableau de données doit être passé à la fonction (d'où le préfixe « array »).
  public function hydrate(array $donnees)
  {
    foreach ($donnees as $key => $value)
    {
      // On récupère le nom du setter correspondant à l'attribut.
      $method = 'set'.ucfirst($key);
          
      // Si le setter correspondant existe.
      if (method_exists($this, $method))
      {
        // On appelle le setter.
        $this->$method($value);
      }
    }
  }
````

### Interface

Techniquement, une interface est une classe entièrement abstraite. Son rôle est de décrire un comportement à notre objet.
Une interface se déclare avec le mot-clé ``interface``, suivi du nom de l'interface, suivi d'une paire d'accolades:

```
interface Movable
{
  public function move($dest);
}
```

Exemple: une voiture et un personnage n'ont pas de raison d'hériter d'une même classe, par contre, les deux doivent avoir la possibilité de se déplacer, donc on peut créer une interface représentant ce point commun.  


* Toutes les méthodes présentes dans une interface doivent être publiques.

* Une interface ne peut pas lister de méthodes abstraites ou finales.

* Une interface ne peut pas avoir le même nom qu'une classe et vice-versa.


Il faut ensuite implémenter l'interface à la classe avec le mot-clé ``implements`` (c'est un peu comme faire hériter une classe d'une autre):

```
class Personnage implements Movable
{

}
```

Puis il faut alors obligatoirement implémenter les méthodes de l'interface dans la classe qui utilise l'interface (la méthode peut alors être abstraite ou finale dans la classe).

On peut implémenter plus d'une interface par classe, à condition qu'elles n'aient aucune méthode portant le même nom.

```
interface iA
{
  public function test1();
}

interface iB
{
  public function test2();
}

class A implements iA, iB
{
  // Pour ne générer aucune erreur, il va falloir écrire les méthodes de iA et de iB.
  
  public function test1()
  {
  
  }
  
  public function test2()
  {
  
  }
}
```


* Les constantes d'interface

   Elles fonctionnent exactement comme les constantes de classes. Elles ne peuvent être écrasées par des classes qui implémentent l'interface. 
   
   ```
  interface iInterface
  {
    const MA_CONSTANTE = 'Hello !';
  }
  
  echo iInterface::MA_CONSTANTE; // Affiche Hello !
  
  class MaClasse implements iInterface
  {
  
  }
  
  echo MaClasse::MA_CONSTANTE; // Affiche Hello !
  ```
  
  * Héritage d'interface
  
  Comme pour les classes, on peut faire hériter une interface d'une autre avec le mot-clé ``extands``.
  
  Par contre, on ne peut réécrire ni une méthode ni une constante qui a déjà été listée dans l'interface parente.
  
  
  Contrairement aux classes, les interfaces peuvent hériter de plusieurs interfaces à la fois. Il suffit de séparer leur nom par une virgule.
  
```
interface iA
{
  public function test1();
}

interface iB
{
  public function test2();
}

interface iC extends iA, iB
{
  public function test3();
}
```

Dans cet exemple, si on imagine une classe implémentant iC, celle-ci devra implémenter les trois méthodes ``test1``,``test2`` et ``test3``.


### L'auto-chargement des classes

Pour une question d'organisation, il vaut mieux créer un fichier par classe. Par exemple, nommer le fichier Maclasse.php et on place la classe dedans. Ensuite, il suffit d'inclure le fichier:

```
require 'MaClasse.php'; // J'inclus la classe.

$objet = new MaClasse; // Puis, seulement après, je me sers de ma classe.
```

Puis, pour éviter de les inclure une par une, on utilise l'auto-chargement des classes, c'est-à-dire qu'on crée dans le fichier principal (celui où on crée une instance de notre classe) une ou plusieurs fonctions qui charge(nt) le fichier déclarant la classe:

````
function chargerClasse($classe)
{
  require $classe . '.php'; // On inclut la classe correspondante au paramètre passé.
}

//Puis on va utiliser la fonction ``spl_autoload_registeren`` spécifiant en premier paramètre le nom de la fonction à charger

spl_autoload_register('chargerClasse'); // On enregistre la fonction en autoload pour qu'elle soit appelée dès qu'on instanciera une classe non déclarée.

$perso = new Personnage;

````

### Surcharge (Overriding)

Permet de modifier une méthode d'une classe parent dans une classe enfant.
Par exemple, on peut surcharger la méthode __construct de la classe parent en la réécrivant dans la classe enfant et en rajoutant des instructions.