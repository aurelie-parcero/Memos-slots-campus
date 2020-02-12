#Memo - Programmation orientée objet en PHP

###Classe
C'est un ensemble de variables et de fonctions (attributs et méthodes).
Le nom des classes commence par une majuscule. Il s'agit de la notation PEAR, il est fortement conseillé de la respecter!.
```
class Personnage {      // mot-clé "class" suivi du nom de la classe
//déclaration des attributs et méthodes ici
} 
```

###Objet
C'est une <b>instance</b> de la classe à utiliser.
Pour créer un nouvel objet, il faut faire précéder le nom de la classe à <b>instancier</b> du mot-clé ``new``:

```
$perso = new Personnage;
```
Ainsi, ``$perso`` sera un objet de type ``Personnage``. On dit que l'on <b>instancie</b> la classe ``Personnage``, que l'on crée une <b>instance</b> de la classe ``Personnage``.

###Attributs
Il s'agit d'une variable. Il est possible ou non de les initialiser lors de leur déclaration.
Ils sont toujours(?) privés (alors que la méthode pourra être privée ou publique), c'est ce qu'on appelle <b>l'encapsulation</b>.
```
class Personnage {
private $_force = 50;
private $_degats;
}
```
La valeur donnée par défaut doit être une expression scalaire statique. Par conséquent, leur valeur ne peut par exemple pas être issue d'un appel à une fonction ( ``private $_attribut = strlen('azerty')`` ) ou d'une variable, superglobale ou non ( ``private $_attribut = $_SERVER['REQUEST_URI']`` ).


###Méthodes
Il s'agit des fonctions utilisées pour une même classe.
Elle est précédée du mot-clé ``function`` et de la visibilité de la méthode. Les types de visibilité des méthodes sont les mêmes que les attributs. Les méthodes n'ont en général pas besoin d'être masquées à l'utilisateur, le plus souvent elles seront en ``public`` (à moins qu'on tienne absolument à ce que l'utilisateur ne puisse pas appeler cette méthode, par exemple s'il s'agit d'une fonction qui simplifie certaines tâches sur l'objet mais qui ne doit pas être appelée n'importe comment).
```
class Personnage
{
  private $_force;        
  private $_localisation; 
        
  public function deplacer() // Une méthode qui déplacera le personnage (modifiera sa localisation).
  {

  }
}
```
Pour appeler une méthode d'un objet, il va falloir utiliser un opérateur : il s'agit de l'opérateur ``->`` (une flèche composée d'un tiret suivi d'un chevron fermant).
À gauche de cet opérateur, on place l'objet que l'on veut utiliser. 
À droite de l'opérateur, on spécifie le nom de la méthode que l'on veut invoquer.

```
class Personnage {
private $_force;
private $_localisation;

// Nous déclarons une méthode dont le seul but est d'afficher un texte.
public fonction parler() {

echo 'Je suis un personnage!';
    }
}
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
  private $_experience = 50;

  public function afficherExperience()
  {
    echo $this->_experience;
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

Pour s'assurer que l'on passe bien en paramètre un objet et éviter ainsi les erreurs, il suffit de préciser dans les parenthèses le nom de la classe:

```
class Personnage
{
  //...

  public function frapper(Personnage $persoAFrapper)
  {
    // …
  }
}
```
Grâce à ça, on est sûrs que la méthode ``frapper()`` ne sera exécutée que si le paramètre passé est de type ``Personnage``, sinon PHP interrompt tout le script. On peut donc appeler les méthodes de l'objet sans crainte qu'un autre type de variable soit passé en paramètre.


- ####Les méthodes statiques

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

- ####Les attributs statiques

Le principe est le même, c'est-à-dire qu'un attribut statique appartient à la classe et non à un objet. Ainsi, tous les objets auront accès à cet attribut et cet attribut aura la même valeur pour tous les objets.

La déclaration d'un attribut statique se fait en faisant précéder son nom du mot-clé ``static``.

 ```
// Variable statique PRIVÉE.
  private static $_texteADire = 'Je vais tous vous tuer !';
```


###Public / Private
Si un attribut ou une méthode est ``public``, alors on pourra y avoir accès depuis n'importe où, depuis l'intérieur de l'objet (dans les méthodes qu'on a créées), comme depuis l'extérieur.
 
S'il est `` private``, il y a quelques restrictions. On aura accès aux attributs et méthodes seulement depuis l'intérieur de la classe, c'est-à-dire que seul le code voulant accéder à un attribut privé ou une méthode privée écrit(e) à l'intérieur de la classe fonctionnera.

```
class Personnage {
private $_force;        //On définit les attributs qui ne seront utilisables qu'à l'intérieur de la classe
private $_localisation;
}
```
Les attributs respectent la notation PEAR, qui dit que chaque nom d'élément privé (attributs ou méthodes) doit être précédé d'un underscore.

###Accesseurs (ou getters)

C'est une méthode dont le rôle est de renvoyer l'attribut qu'on lui demande. Par convention, ces méthodes portent le même nom que l'attribut dont elles renvoient la valeur.
```
class Personnage
{
  private $_force;
  private $_experience;
  private $_degats;
        
  // Ceci est la méthode degats() : elle se charge de renvoyer le contenu de l'attribut $_degats.
  public function degats()
  {
    return $this->_degats;
  }
        
  // Ceci est la méthode force() : elle se charge de renvoyer le contenu de l'attribut $_force.
  public function force()
  {
    return $this->_force;
  }
        
  // Ceci est la méthode experience() : elle se charge de renvoyer le contenu de l'attribut $_experience.
  public function experience()
  {
    return $this->_experience;
  }
}
```

###Mutateurs (ou setters)

Méthode permettant de modifier un attribut. Ces méthodes sont de la forme ``setNomDeLAttribut()``:

```
// Mutateur chargé de modifier l'attribut $_force.
  public function setForce($force)
  {
    if (!is_int($force)) // S'il ne s'agit pas d'un nombre entier.
    {
      trigger_error('La force d\'un personnage doit être un nombre entier', E_USER_WARNING);
      return;
    }
    
    if ($force > 100) // On vérifie bien qu'on ne souhaite pas assigner une valeur supérieure à 100.
    {
      trigger_error('La force d\'un personnage ne peut dépasser 100', E_USER_WARNING);
      return;
    }
    
    $this->_force = $force;
  }
  
  // Mutateur chargé de modifier l'attribut $_experience.
  public function setExperience($experience)
  {
    if (!is_int($experience)) // S'il ne s'agit pas d'un nombre entier.
    {
      trigger_error('L\'expérience d\'un personnage doit être un nombre entier', E_USER_WARNING);
      return;
    }
    
    if ($experience > 100) // On vérifie bien qu'on ne souhaite pas assigner une valeur supérieure à 100.
    {
      trigger_error('L\'expérience d\'un personnage ne peut dépasser 100', E_USER_WARNING);
      return;
    }
    
    $this->_experience = $experience;
  }
```

###Constructeur

C'est une méthode écrite dans la classe, qui d'initialiser les attributs dès la création de l'objet.

Il s'écrit comme ceci: ``__construct`` avec deux underscore au début.

Comme son nom l'indique, le constructeur sert à construire l'objet. Il est exécuté dès la création de l'objet et par conséquent, aucune valeur ne doit être retournée.
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

###Scope Resolution Operator (opérateur de résolution de portée) "::"

Il est utilisé pour appeler des éléments appartenant à telle classe et non à tel objet. En effet, nous pouvons définir des attributs et méthodes appartenant à la classe : ce sont des éléments statiques.

Parmi les éléments appartenant à la classe, il y a aussi les constantes de classe, sortes d'attributs dont la valeur est constante, c'est-à-dire qu'elle ne change pas.

- Les constantes de classe
Une constante est une sorte d'attribut appartenant à la classe dont la valeur ne change jamais.

Pour déclarer une constante, il faut faire précéder son nom du mot-clé ``const``.

````
class Personnage
{
  // Tous les attributs en privé !
  private $_force;
  private $_localisation;
  private $_experience;
  private $_degats;


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
  private $_force;
  private $_localisation;
  private $_experience;
  private $_degats;


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
      $this->_force = $force;
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



###L'hydratation
L'hydratation est un point essentiel dans le domaine de la POO, notamment lorsqu'on utilise des objets représentant des données stockées. 

Quand on vous parle d'hydratation, c'est qu'on parle d'« objet à hydrater ». Hydrater un objet, c'est tout simplement lui apporter ce dont il a besoin pour fonctionner. En d'autres termes plus précis, hydrater un objet revient à lui fournir des données correspondant à ses attributs pour qu'il assigne les valeurs souhaitées à ces derniers. L'objet aura ainsi des attributs valides et sera en lui-même valide. On dit que l'objet a ainsi été hydraté.

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

## Résumé "opérateurs"

L'opérateur « -> » permet d'accéder à un élément de tel objet

L'opérateur « :: » permet d'accéder à un élément de telle classe.


##Bonnes pratiques
###L'auto-chargement des classes

Pour une question d'organisation, il vaut mieux créer un fichier par classe. Par exemple, nommer le fichier Maclasse.php et on place la classe dedans. Ensuite, il suffit d'inclure le fichier:

````
require 'MaClasse.php'; // J'inclus la classe.

$objet = new MaClasse; // Puis, seulement après, je me sers de ma classe.
````

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

