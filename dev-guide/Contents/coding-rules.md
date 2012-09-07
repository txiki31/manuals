# Règles de codage

## Généralités

### Indentation

L'indentation de structure est de 4 espaces sans tabulation.

### Taille des lignes

Les lignes ne doivent pas excéder 85 caractères et ne doivent pas avoir
d'espaces en fin de ligne. Pas découpé et indenté :

    list($foo, $bar, $baz) = array(Zim::getVal('foo'), Dib::getVal('bar'), Gir::getVal('baz', Gir::DOOM));

Bien découpé et indenté :

    list($foo, $bar, $baz) = array(
        Zim::getVal('foo'),
        Dib::getVal('bar'),
        Gir::getVal('baz', Gir::DOOM)
    );

### Tag PHP

Il faut toujours utiliser <?php ?>.

### Fichiers

Les noms de fichier doivent être écrits en CamelCase, en suivant les
exemples suivants :

    nomDeClasse.php
    actionNomAction.php
    methodNomMethode.php

Les fichiers PHP ne doivent pas avoir d'espace avant ou après les
balises d'ouverture et de fermeture PHP. Le tag de fermeture PHP doit
toujours être sur la dernière ligne du fichier et être précédé par une
ligne vide. Les fichiers PHP doivent être en us-ascii. Les commentaires
devant être en anglais.

### Inclusion de code

L'utilisation de include/require/include\_once n'est pas autorisée, les
classes internes doivent être autoloadées.. Seul require\_once est
accepté lors de l'inclusion de bibliothèque.

### Opérateurs booléens

Les opérateurs booléens OR,AND, NOT sont dépréciés en faveur de ||n &&
et !.

### Les fonctions de traitements de chaînes de caractères

L'utilisation des fonctions strlen, strcpy, str\* sont proscrites.
Utilisation de leur équivalent mb\_strlen, mb\_strcpy, mb\_\*.

### Les constantes

Les seules constantes autorisées sont les constantes de classe.

### Les bibliothèques

Les bibliothèques de fonctions doivent être englobées dans une classe.

## Conventions de nommage

### Généralités

Les noms de classe, de fonctions et de variables trop courts ou trop
long sont déconseillés pour des raisons de lisibilité. Idéalement un nom
devrait être compris entre 3 et 20 caractères (excepté dans le cas des
itérateurs ou un seul caractère et toléré). Tous les mots clefs php
doivent être en minuscules (if, for, class).

### Classe

Les classes doivent avoir un nom parlant. éviter les abréviations
lorsque cela est possible. Les noms de classes doivent toujours
commencer par une majuscule et le reste du nom de la classe est défini
en CamelCase.

    class MaClasse 
    {

    }

### Les fonctions et les méthodes

Les fonctions doivent avoir un nom parlant. éviter les abréviations
lorsque cela est possible. Les noms de fonctions doivent toujours
commencer par une minuscule et le reste du nom de la classe est défini
en CamelCase.

Un nom est composée d'au moins 2 informations utiles :

-   un préfixe (souvent court, le premier mot)
-   un suffixe (souvent long, de plusieurs mots)

Voila les conventions de préfixe utilisés dans Dynacase :

  ----------------------------------------------------------------------
  Préfixe                  Comportement
  ------------------------ ---------------------------------------------
  set                      stocke/enregistre la valeur fourni

  get                      retourne une unique valeur/élément

  is / has                 test si la condition est vrai et retourne le
                           résultat du test

  check                    vérifie que la condition est satisfaite et
                           retourne une exception si ça n'est pas le cas

  list                     retourne une/liste de valeur élément

  \*                       éxecute l'opération demandée
  ----------------------------------------------------------------------

### Les constantes

Les constantes doivent toujours être en majuscules. Les constantes true,
false et null font exception à la règle des majuscules, et doivent
toujours être en minuscules. Les define sont à proscrire, il est
recommandé d'utiliser des constantes de classe.

### Les variables globales

Les variables globales sont fortement déconseillées, lorsqu'elles sont
nécessaires, elles doivent être prefixées par \_ et en majuscule.

## Structures de contrôles

### Parenthèses

Les instructions de contrôle doivent avoir un espace entre le mot clé de
l'instruction et la parenthèse ouvrante, afin de les distinguer des
appels de fonctions.

    <?php
    if ((condition1) || (condition2)) {
        action1;
    } elseif ((condition3) && (condition4)) {
        action2;
    } else {
        defaultaction;
    }
    ?>

    <?php
    switch (condition) {
    case 1:
        action1;
        break;
    case 2:
        action2;
        break;
    default:
        le job par defaut;
        break;
    }
    ?>

### Accolades

Il faut toujours utiliser des accolades, même dans les situations où
elles sont techniquement optionnelles. Leur présence augmente la
lisibilité du code et réduit le risque d'erreur logique lors de l'ajout
de nouvelles lignes de code.

### Opérateur ternaire

Les opérateurs ternaires ne devraient être utilisés que dans les
conditions suivantes:

-   un opérateur ternaire doit être écrit sur une seul ligne de code
-   on ne doit pas imbriquer les opérateurs ternaires
-   les opérateurs ternaires doivent donc être réservé à des tests
    simples et à l'initialisation des variables.

### Priorité des opérateurs

L'utilisation de la seule priorité des opérateurs est déconseillées, il
est recommandé d'utiliser des parenthèses pour augmenter la lisibilité
du code.

    exclus :  if ($x || $y && $z && !$w)
    mettre if (($x || $y) && ($z && (!$w)))

## Classes

### Saut de ligne

Les déclaration de classes ouvrent l'accolade sur une nouvelle ligne.

    <?php
    class FooBar
    {

        //... et le code vient ici

    }
    ?>

### Visibilité

Toutes les fonctions et les membres d'une classe doivent indiquer leur
visibilité. Le mot clef var est donc proscrit. Les attributs de classe
doivent être définis soit en protected soit en private. L'accès en est
limité via des getteurs et des setteurs. L'utilisation des méthodes
magiques **set et**get est découragée.

### Définition

Les attributs de classe doivent être déclarés.

### Valeur par défaut

Toutes les variables de classe doivent être initialisé soit à une valeur
par default, soit à la valeur null.

## Fonctions

### Indentation et argument

La déclaration des fonctions respecte l'indentation du style "K&R".

    <?php
    function connect(&$dsn, $persistent = false)
    {
        if (is_array($dsn)) {
            $dsninfo = &$dsn;
        } else {
            $dsninfo = DB::parseDSN($dsn);
        }

        if (!$dsninfo || !$dsninfo['phptype']) {
            return $this->raiseError();
        }

        return true;
    }
    ?>

### Ordre des arguments

Les arguments possédant des valeurs par défaut vont à la fin de la liste
des arguments.

### Appel de fonction

Les fonctions doivent être appelées sans espace entre le nom de la
fonction, la parenthèse ouvrante, et le premier paramètre ; avec un
espace entre la virgule et chaque paramètre et aucun espace entre le
dernier paramètre, la parenthèse fermante et le point virgule. Voici un
exemple : <?php
$var = foo($bar, $baz, $quux);
?>

Comme montré ci-dessus, il doit y avoir un espace de chaque côté du
signe égal utilisé pour affecter la valeur de retour de la fonction à
une variable.

### Typage des arguments

Les arguments dans les fonctions doivent être typés excepté pour les cas
où ce n'est pas possible (type de base array, string, int etc...).

### Retour de méthode

  ----------------------------------------------------------------------
  Préfixe                  Retour si l'éxécution est conforme
  ------------------------ ---------------------------------------------
  set                      l'objet courant ($this)

  get                      type d'élément indiqué dans le return

  is / has                 booléen

  check                    l'objet courant ($this) si l'assertion est
                           validée

  list                     array

  \*                       l'objet courant ($this)
  ----------------------------------------------------------------------

Une méthode doit toujours retourner le même type de données (pas de
méthode retournant une string et un array suivant que le résultat est
unique ou multiple par exemple).

### Retour d'erreur et exception

Une méthode doit retourner une exception si les contraintes sur les
paramètres d'entrée ne sont pas validées et que cela va entrainer un
dysfonctionnement.

    /**
     * test for example
     *
     * @param int $x must be > 0 and be odd
     * @return float
     */
    public static function mySqrt($x) {
        if ($x < 0) {
            throw new dcp\Exception(sprintf("need to be positive : %d found",$x));
        }
        if ($x%2 == 0) {
            dcp\Context::setError(sprintf(_("need to be odd: %d found"),$x));
            return null;
        }
        return sqrt($x);
    }

Toute méthode ayant annoncé un type de retour non vide doit retourner
"null" si le résultat ne peut être retourné mais que cela ne provoque
pas de dysfonctionnement. De plus un message doit être indiqué (via la
méthode setError) pour expliquer pourquoi le retour n'a pu être fait.

La fonction appelante peut alors utiliser la méthode
getLastErrorMessage() si elle veut voir une éventuelle erreur.

    $c=dcp\MyClass::mySqrt($x) ;
    if ($c === null) {
        $err=dcp\Context::getLastErrorMessage();
    }

## Documentation

### Généralités

Tous les fichiers de code source doivent contenir le bloc de
commentaires d'en-tête : Un bloc de commentaire "page-level" en début de
chaque fichier, et un bloc de commentaires "class-level" juste au dessus
de chaque classe.

### Bloc classe level

    /**
     * Description courte de la classe
     *
     * Description plus détaillée de la classe (si besoin en est)...
     *
     * @brief NomCatégorie
     * @class NomPaquetage
     * @author Equipe de dev <dev@anakeen.com>
     **/

### Bloc function level

    /**
     * Description courte de la fonction
     *
     * Description plus détaillée de la fonction (si besoin en est)...
     *
     * @param type $parameter Description.
     *
     * @return type Description Si la méthode ne retourne pas de valeur, il faut utiliser void comme type.
     * @throws \qualified\Class Description.
     **/

### Bloc var level

    /**
     * Description courte de la variable de classe
     *
     * Description plus détaillée de la variable de classe (si besoin en est)...
     *
     * @var type Description.
     **/

### Variable type

Type de variables qui peuvent être utilisés dans des docBlock :

-   integer Integer type variable (non-floating-point positive or
    negative number).
-   float Float type (point number).
-   boolean Logical type (true or false).
-   string String type (any value in "" or ' ').
-   array Array type.
-   ClasseName Object type : il faut indiquer explicitement le type
    d'objet attendu.
-   resource Resource type (for example, the result of
    mysql\_connect()).
-   callback Used for anonymous functions, or objects that implement
    \_\_invoke(), or array style callbacks.
-   mixed Pseudo type with undefined (or multiple) types.
-   void Pseudo type (i.e. null, a function returns nothing)

### Balises

-   @brief : correspond au package physique (webinst)
-   @class : correspond à l'élément en cours de développement
    dynacasePlatformCore etc... (les noms sont indiqués sur le bug
    tracker)
-   @author :Equipe de dev <dev@anakeen.com>

## Namespace

### Namespace

Le namespace doit être déclaré juste après le tag PHP d'ouverture.

    <?php

    namespace dcp\util;

**Voir le découpage en namespace**

## Gestion des erreurs

### Niveau d'erreur

Le code doit être E\_STRICT compatible. Cela signifie qu'il ne doit pas
produire de warning ou d'erreur quand le niveau de rapport d'erreur de
php est au niveau E\_STRICT.
