# Family : Elementary customisation

## Introduction

Dans ce tutoriel nous allons voir comment ajouter de la logique métier
simple au fonctionnement d'une famille. Nous allons donc découvrir les
points suivants :

-   comment fixer une valeur par défaut :
    -   statique
    -   dynamique

-   comment réaliser un attribut dont la valeur est calculée,
-   comment mettre en place une contrainte sur la valeur d'un attribut,
-   comment mettre en place une aide à la saisie,
-   comment synchroniser la valeur de plusieurs attributs en fonction
    d'un attribut de type relation,
-   comment afficher de manière conditionnelle des attributs.

## Réalisation

Veuillez tout d'abord reprendre le projet initier dans le tutoriel
précédent ou télécharger le projet mis à votre disposition
[ici](http://sldmdksmkdpmskmdskmdksm)

### Valeur par défaut

Il existe dans Dynacase deux types de valeur par défaut :

-   les valeurs par défaut statique qui consiste en une valeur statique
    définie lors de la création de la famille,
-   les valeurs par défaut dynamique qui consiste en une valeur calculée
    (la date du jour, l'utilisateur en cours,...)

Ces deux valeurs sont présentée à l'initialisation du formulaire par
l'utilisateur.

#### Valeur par défaut statique

Nous allons définir la valeur par défaut du booléen indiquant la prise
en compte d'une remarque dans la *fiche de lecture*.

Pour cela, vous devez ouvrir la famille *QCO\_QUALITY* et sélectionner
l'attribut *QCO\_REVIEW\_CHECKED*. Une fois cet attribut sélectionné
vous pouvez voir l'image ci-dessous :\
**insérer ici l'image correspondante**

Cette interface vous permet de saisir les options propres à cet
attribut. Nous nous intéressons ici aux options sous le paragraphe
*Default Value*. C'est ici que sont définies les valeurs par défaut
statique et dynamique d'un attribut. Nous allons sélectionner le champ
valeur par défaut (statical default value) et compléter avec la valeur
suivante "FALSE", en effet nous sommes dans le cas d'un booléen et les
deux seules valeurs par défaut statique acceptés sont "TRUE" et "FALSE".

#### Valeur par défaut dynamique

Nous allons maintenant définir une valeur par défaut dynamique. La
valeur de l'attribut *Validateur* doit avoir par défaut la valeur de
l'utilisateur connecté.\
Pour cela, vous devez sélectionner l'attribut *QCO\_REVIEW\_VALIDATOR*.
Une fois cet attribut sélectionné, vous devez remplir la propriété
*valeur par défaut calculée* avec la valeur suivante
CONTEXT::getCurrentUser()

### Attribut calculé

Un attribut calculé est un attribut dont la valeur est calculée par une
méthode de la classe PHP associée à la famille. Nous allons dans notre
cas calculer une référence automatiquement en à l'aide d'une séquence
qui nous est fournie par la plateforme.\
Pour cela, nous devons commencer par écrire les fonctions
d'initialisation de la séquence et de calcul de celle-ci.

Nous allons commencer par créer et ajouter un élément de type séquence.
Il permet de créer et de gérer un objet interne de Dynacase de gestion
de séquence. Pour le créer vous devez cliquer dans le menu Dynacase sur
ajouter un élément et choisir dans le type autre un élément de type
séquence.\
Un fichier XML de séquence est crée dans le répertoire miscellaneous de
votre projet. Vous devez définir pour cet objet un nom logique et une
valeur d'initialisation (facultative), le nom logique que nous allons
choisir est SEQ\_QCO\_QUALITY.\
Cet objet est entièrement géré par Dynacase et a une interface très
simple, trois fonctions sont accessibles :

-   getCurrentValue() : qui donne la valeur de la séquence
-   increment($int = 1) : permet d'incrémenter la valeur de la séquence,
    la valeur par défaut d'incrément est de 1 mais vous pouvez choisir
    n'importe quel nombre entier,
-   reinit($int=0) : re-initialise la séquence, la valeur par défaut est
    de 0 mais vous pouvez choisir n'importe quel nombre entier

Ensuite, nous allons créer le code qui permet d'utiliser et de tirer
parti de notre nouveau document.

Veuillez ouvrir le fichier PHP associé à la famille qui se nomme
*classQCO\_QUALITY.php*. Nous allons ensuite créer la fonction qui
permet d'incrémenter la séquence lors de la création d'un nouveau
document. Pour ce faire, nous allons au postCreated du document vérifier
que celui-ci vient d'être crée et incrémenter de 1 la séquence.

~~~~ {.Php .numberLines}
    <?php
    public function postCreated(){
        $qualitySequence = new_Doc("SEQ_QCO_QUALITY");
        $currentSequence = $qualitySequence->increment();
        $qualitySequence->save();
        $this->setValue("QCO_SEQUENCE", $currentSequence);
    }
    ?>
~~~~

Nous allons maintenant créer la fonction qui concatène le numéro de
séquence au préfixe de référence

~~~~ {.Php .numberLines}
    <?php
    public function getRefrence(){
        return sprintf("%s %s", $this->getParamValue("QCO_PREFIXE"),$this->getValue("QCO_SEQUENCE"));
    }
    ?>
~~~~

Cette fonction retourne la valeur que vous souhaitez mettre dans la
référence. Vous n'avez plus maintenant qu'à éditer le formulaire de
saisie des attributs en sélectionnant l'attribut *QCO\_REFERENCE* et
dans la propriété *valeur calculée* vous saisissez l'appel à la fonction
*getRefrence* sous la forme *::getReference()*.

### Contrainte sur la valeur d'un attribut

Nous allons maintenant mettre en place une contrainte sur le champ titre
du document qualité. En effet, la spécification indique que le titre
d'un document ne doit pas pouvoir être dédoublé. Pour ce faire, vous
devez ouvrir à nouveau le fichier PHP associé et ajouté la méthode
suivante :

~~~~ {.Php .numberLines}
    <?php
    public function checkUniqueTitle(){
        $searchOtherDocument = new SearchDoc("QCO_QUALITY");
        $searchOtherDocument->addFilter("QCO_TITLE = '%s'",$this->getValue("QCO_TITLE"));
        $nbDocument = $searchOtherDocument->count();
        if ($this->initid === null)
        {
            if ($nbDocument != 0){
                return array("err"=>"There is another document with the same title");
            }
        }
        else
        {
            if ($nbDocument > 1){
                return array("err"=>"There is another document with the same title");
            }
        }
    }
    ?>
~~~~

Dans cette fonction nous effectuons une recherche qui va trouver tous
les documents ayant l'attribut *QCO\_TITLE* avec la même valeur que le
QCO\_TITLE de notre document en cours.\
Ensuite nous effectuons un count sur cette recherche, cette méthode
effectue la recherche mais ne retourne que le nombre de résultat, ce qui
est plus léger que que d'effectuer la recherche.\
Deux cas s'offre à nous, si jamais le document n'a pas encore été crée
(initid à null) alors on doit vérifier qu'aucun document ne porte ce
titre et si le document a déjà été crée qu'il n'existe pas plus d'un
document ayant le même titre (car une fois le document crée il est
inséré en base et la recherche le trouvera).

Il nous reste à relier cette contrainte à l'attribut qui la porte, pour
ce faire vous devez retourner sur la page d'édition des attributs et
ajouter une entrée au tableau de contrainte de l'attribut *QCO\_TITLE*.
Vous cliquez sur add et faite dérouler la liste des fonctions dans
celle-ci vous sélectionnez la fonction *checkUniqueTitle*.

### Une aide à la saisie

Une aide à la saisie est une fonction PHP retournant une liste de valeur
possible pour un attribut. Cela permet entre autre de faire des listes
déroulantes dans les attributs de type relation dont le contenu varie
suivant la valeur d'attribut du document.\
Nous allons mettre en place une aide à la saisie sur l'attribut *Parent*
des *Domaines de référence*. Cette aide ne doit présenter que les
documents dont le parent n'est pas le document en cours.\
Pour ce faire, nous allons ajouter une fonction dans le fichier d'aide à
la saisie. En effet, celles-ci sont dé-contextualisées des familles et
peuvent être appelées par une famille.

Nous allons donc initialiser un fichier d'aide à la saisie, pour ce
faire aller dans le menu Dynacase et cliquer sur ajouter dans le sous
menu *Autre* une *Classe d'aide à la saisie*. Vous devez spécifier le
nom de la classe, nous allons choisir *QCO\_HELPER*. Une fois ces
éléments remplis un fichier PHP est crée et ouvert.

Nous allons écrire le code suivant dans ce fichier.

~~~~ {.Php .numberLines}
    <?php
    public function getPotentialParent($initId, $userInput)
    {
        $searchParent = new SearchDoc("QCO_TOPIC");
        $searchParent->addFilter("QCO_TOPREF_DESC_PARENT != %d", initId)
        $searchParent->addFilter("TITLE  ~* '%s'", $userInput);
        $searchParent->search();
        $potentialParents = array();
        while($currentPotentialParent as $searchParent->nextDoc()){
            $potentialParents[] = array($currentPotentialParent->getTitle(), $currentPotentialParent->initid, $currentPotentialParent->getTitle());
        }
        return $potentialParents;
    }
    ?>
~~~~

Ce code effectue une recherche sur tous les éléments de la famille
*QCO\_TOPIC*, cette recherche est restreinte par deux filtres les
éléments dont le parent n'est pas l'initid passé et les éléments dont le
titre correspond au userInput. Une fois cette recherche effectuée nous
nous contentons de renvoyer dans un tableau les informations suivantes :

-   titre,
-   initid,
-   titre

Nous allons maintenant relier cette fonction à l'attribut qui doit
disposer de l'aide à la saisie. Pour ce faire, vous devez retourner dans
le formulaire de la famille *QCO\_TOPIC* et ouvrir l'attribut
*QCO\_TOPREF\_DESC\_PARENT*.

**Ajouter une capture d'écran**

Vous voyez le champ *Aide à la saisie*, nous allons y ajouter la
référence suivante :\

QCO\_HELPER::getPotentialParent(\#INITID,\#CURRENT\_INPUT):\#CURRENT\_ATTRIBUTE\_VALUE,\#CURRENT\_ATTRIBUTE\_TEXT
ou la notation abrégée : QCO\_HELPER::getPotentialParent(\#INITID,
\#CI):\#CAV,\#CAT

les mots clefs que nous avons utilisés indique les éléments suivants :

-   \#INITID : c'est l'identifiant initial de cette série documentaire
-   \#CURRENT\_INPUT ou \#CI : est la valeur contenue au moment du
    déclenchement de l'aide à la saisie dans le formulaire
-   \#CURRENT\_ATTRIBUTE\_VALUE ou \#CA : indique que la deuxième valeur
    du tableau des valeurs retournées sera stockée en clef dans
    l'attribut concerné par cette aide à la saisie (donc pas affiché à
    l'utilisateur)
-   \#CURRENT\_ATTRIBUTE\_TEXT ou \#CAT : indique que la troisième
    valeur du tableau des valeurs retournées sera affichée en
    consultation et en édition dans l'attribut concerné par cette aide à
    la saisie

Les lecteurs les plus attentifs auront remarqués que nous retournons
trois valeurs dans notre aide à la saisie et que nous n'en déclarons que
deux dans l'utilisation de celle-ci. La première valeur retournée sert
de valeur d'affichage dans la liste déroulante qui est produite lors de
la consultation du résultat de l'aide à la saisie et n'est donc pas
stockée.

### Synchroniser plusieurs attributs en fonction d'un attribut relation

Un besoin couramment exprimé est de synchroniser une série d'attribut en
fonction d'un attribut de type Relation. Pour l'exprimer de manière plus
concrète, nous souhaitons ajouter un attribut de type date synchronisé
avec l'attribut relation portant le père d'un *Domaine de référence* cet
attribut portera toujours la dernière date de modification de l'attribut
père. Pour ce faire, il suffit d'utiliser la fonction adéquat dans
l'attribut calculé.\
Vous devez donc ajouter un attribut date de modification à la suite de
l'attribut *QCO\_TOPREF\_DESC\_PARENT* dans la famille *QCO\_TOPIC*,
nous allons le nommer *QCO\_TOPREF\_DESC\_PARENT\_DATE\_MODIF*.\
**Ajouter une capture d'écran**\
Une fois cet attribut ajouté, veuillez modifier sa propriété *attribut
calculé* pour y ajouter la fonction suivante :\
::synchronizeAttribute(QCO\_TOPREF\_DESC\_PARENT, ldate)\
la fonction synchronizeAttribute sera appelée à chaque consultation de
la famille et synchronisera la valeur de l'attribut avec l'élément de la
relation.

### Comment afficher des attributs de manière conditionnelle

**Ce point reste à définir**

## Conclusion

Vous pouvez maintenant déployer les éléments que nous venons de modifier
et aller vérifier que le comportement est bien conforme à ce que nous
avons prescrits.
