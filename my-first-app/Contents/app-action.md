# Application et Action

## Introduction

Nous allons maintenant voir deux concepts essentiels de Dynacase :

-   Applications : une application permet de grouper des actions, que ça
    soit dans le cadre du développement d'une petite bibliothèque
    d'action Dynacase ou pour créer une IHM complexe comme
    familyXplorer,
-   Actions : une action est une classe qui permet d'effectuer des
    opérations, elle peut être appelée aussi en CLI que en WEB et peut
    être soumise à une ACL qui restreint ses conditions d'utilisations.

Nous allons dans ce tutoriel mettre en place une application en héritant
de *familyXplorer*. FamilyXplorer est une des applications de base de
Dynacase Platform, elle permet de travailler avec une ensemble de
famille. Nous allons aussi mettre en place une action que nous allons

## Mise en pratique

Nous allons tout d'abord créer l'application pour ce faire vous devez
cliquer sur le menu Dynacase et sélectionner l'option créer une
application. Il vous est demandé le nom logique de votre application,
nous utilisons *COGIP\_APPLICATION*.\
Une nouvelle application vierge est crée. Nous allons tout d'abord
indiquer l'application mère via l'action *inherit*. Le menu déroulant
affiche la liste des applications fourni par défaut et la liste de vos
applications, vous sélectionnez l'application familyXplorer.\
Vous avez donc l'ensemble des paramètres provenant de familyXplorer,
nous allons juste modifier la liste des familles chargés par défaut dans
familyXplorer pour y ajouter vous nouvelles familles. Il faut pour cela
modifier la valeur du paramètre *Default family* pour y ajouter les
éléments suivants : "QCO\_QUALITY,QCO\_HISTORY\_QUALITY,QCO\_TOPIC".

Nous allons passé à la suite de notre tutoriel en créant une nouvelle
action, celle-ci permettra de faire un export de l'ensemble des TOPIC
crée sous la forme d'un fichier CSV.\
Pour ce faire, nous allons :

-   aller dans l'onglet *actions* de notre nouvelle application,
-   cliquer sur le bouton *add* pour ajouter une nouvelle action,
-   donner le nom logique de la nouvelle action *QCO\_EXPORT\_TOPICS*,
-   vous devez ensuite indiquer la classe contenant la logique de
    l'action

Le fichier contenant le squelette de la classe PHP contenant le code de
l'action a été créé automatiquement lors de l'initialisation de votre
action. Vous pouvez l'ouvrir en vous rendant dans le répertoire
contenant votre action
(/application/COGIP\_APPLICATION/actions/QCO\_EXPORT\_TOPICS.php).

Ce fichier contient une classe héritant de la classe *Action*, vous
devez éditer la méthode exécute pour y ajouter votre code. Le code que
nous allons ajouter est le suivant :

~~~~ {.Php}
    <?php
    public function execute(){
        //Cette methode etant heritee nous appelons la methode de la famille mere pour ne pas casser l'heritage
        $return = parent::execute();
        //Nous effectuons ensuite la recherche
        $searchTopic = new SearchDoc("QCO_TOPIC");
        $searchTopic->search();
        $arrayTopic = array();
        while($currentTopic = $searchTopic->nextDoc()){
            $arrayTopic[] = array('name'=>$currentTopic->getTitle());
        }
        $this->getTemplate()->addKey("TOPICS", $arrayTopic);
    }
    ?>
~~~~

Il nous reste maintenant à définir le template dans lequel cette action
produira son résultat. En effet, il y a une séparation forte entre les
données et l'affichage celui-ci se faisant systématiquement par un
système de templating.\
Nous allons donc créer un nouveau fichier de template, pour cela le plus
simple consiste à créer le template directement dans le formulaire
d'action en utilisant une fois notre action sélectionnée le bouton
*ajouter un template*. Un nom logique vous est demander nous allons
indiquer *QCO\_TEMPLATE\_TOPICS\_CSV*.

**Insérer ici le code du template**

## Conclusion

Nous disposons maintenant de tous nos éléments et nous allons pouvoir
procéder à l'installation et au test de nos nouveau composants. Comme il
est de coutume à la fin de nos tutoriau, vous allez maintenant déployer
votre paquet en utilisant le bouton idoine dans la barre des tâche.\
Une fois votre application déployée connecté vous et voyez dans le menu
déroulant des applications apparaître votre nouvelle application, si
vous consultez celle-ci vous pouvez voir le résultat suivant : **insérer
ici une capture d'écran** et si vous exécutez l'URL suivante **insérer
ici l'URL** vous obtenez une sortie en CSV de l'ensemble des titres de
*Domaine de référence* mis en forme par notre template.
