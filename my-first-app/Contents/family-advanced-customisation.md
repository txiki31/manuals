# Family advanced customisation

## Introduction

Dans ce tutoriel nous verrons la notion de cycle de vie documentaire et
les hooks qui lui sont associés.\
En effet, un document peut passer par un certains nombres d'état et vous
pouvez influer sur son fonctionnement via des fonctions PHP que vous
pouvez surcharger dans la classe PHP associé à cette famille. Utilisé à
bon escient ce système vous permet de facilement effectuer du code avant
et après un certains nombre d'actions clefs de votre document.

Les méthodes accessibles sont les suivantes :

-   preCreated : appelée avant la création d'un document,
-   postCreated : appelée après la création d'un document,
-   preModified : appelée avant la modification d'un document,
-   postModified : appelée après la modification d'un document,
-   preCopy : appelée avant la copie,
-   postCopy : appelée après la copie,
-   preDelete : appelée avant la suppression,
-   postDelete : appelée après la suppression,
-   preEdition : appelée avant la création du formulaire d'édition,
-   preConsultation : appelée avant la création du formulaire de
    consultation,
-   preExport : appelée avant l'export,
-   postExport : appelée après l'export,
-   preImport : appelée avant l'import,
-   postImport : appelée après l'import,
-   preRefresh : appelée avant la mise à jour,
-   postRefresh : appelée après la mise à jour.

On peut noter que chacune des méthodes préfixée par *pre* peut
interrompre l'action en cours si vous retournez la valeur false et qu'un
message d'erreur peut être envoyé à l'utilisateur en utilisant la
fonction de pile de message CONTEXT:addUserMessage() pour lui indiquer
la cause de refus de la mise à jour.

## Mise en pratique

Nous allons mettre en pratique ceci en calculant automatiquement un lien
entre un domaine de référence et tous les documents qualités qui y font
appel ce lien doit être mis à jour à la consultation de la fiche. Pour
ce faire, nous pourrions agir au preRefresh, cette fonction est appelée
avant la consultation/edition d'un document quelque soit son mode
d'affichage, mais cela serait consommateur en temps de calcul et nous
préférons agir au preConsultation puisque notre contrainte ne porte que
sur la consultation de la fiche.

Nous allons donc ouvrir le fichier PHP associé à la famille *QCO\_TOPIC*
et ajouter le code suivant :

~~~~ {.Php .numberLines}
    <?php
    public function preConsultation(){
        //Cette methode etant heritee nous appelons la methode de la famille mere pour ne pas casser l'heritage
        $return = parent::preConsultation();
        //Nous effectuons ensuite la recherche
        $searchQualityDocs = new SearchDoc("QCO_ABSTRACT_QUALITY");
        $searchQualityDocs->addFilter("QCO_QUAL_TOPIC != %d", $this->getInitId());
        $searchQualityDocs->result('array','initid');
        $result = $searchQualityDocs->search();
        $this->setValue("QCO_TOPREF_QUALITY_DOC", $result);
        return $return;
    }
    ?>
~~~~

Cette méthode sera appelée avant chaque consultation du document et
mettra à jour la liste des éléments associé au document topic.

Nous allons voir un autre exemple, sur un cas d'importation. Il nous
faut en effet à l'import des documents de qualité historique vérifier
qu'un document de qualité ne porte pas déjà le même titre. Si c'est le
cas nous devons refuser l'import et l'indiquer à l'utilisateur.

Nous allons donc ouvrir le fichier PHP associé à la famille
\*QCO\_QUALITY\_ABSTRACT et ajouter le code suivant :

~~~~ {.Php .numberLines}
    <?php
    public function preImport(){
        //Cette methode etant heritee nous appelons la methode de la famille mere pour ne pas casser l'heritage
        $return = parent::preImport();
        //Nous effectuons ensuite la recherche
        $searchOtherDocument = new SearchDoc("QCO_ABSTRACT_QUALITY");
        $searchOtherDocument->addFilter("QCO_TITLE = '%s'",$this->getValue("QCO_TITLE"));
        $nbDocument = $searchOtherDocument->count();
        if ($nbDocument > 0){
            $return = false;
            CONTEXT::addUserMessage(sprintf(_("Unable to import the document %s because another document have the same title"), $this->getValue("QCO_TITLE")));
        }
        return $return;
    }
    ?>
~~~~

Cette fonction sera appelée avant chaque import et le nombre de
documents sera vérifié. Si celui-ci est supérieur à 0 alors nous
retournons false ce qui bloque l'import et nous envoyons un message à
l'utilisateur. Si la notation du message ne vous apparaît pas clair
veuillez vous reporter au tutoriel sur l'internationalisation.

## Conclusion

Vous pouvez comme d'habitude déployer le package. Nous vous conseillons
de tester la fonction d'associations d'un domaine de référence avec un
document de qualité en utilisant un regardant les domaines de référence
fourni en exemple.\
Vous pouvez ensuite tester l'import d'un document qui échouera en
important le fichier XML fournis à cet usage. Si vous ne savez pas
importer de document veuillez vous reporter au tutoriel
