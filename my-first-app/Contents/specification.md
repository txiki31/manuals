# Spécification détaillée

## Introduction

Ce document est issu du recueil des besoins utilisateurs du département
qualité de la COGIP. Il présentera les points suivants :

-   ensemble des groupes utilisateurs à implémenter,
-   structure des familles à implémenter,
-   structure et paramétrage du cycle de vie à implémenter.

Chacun de ces points est explicité dans un chapitre dédié.

## Groupes et rôles

Les groupes utilisateurs se calquent sur la structure existante au sein
de la COGIP et permettent de regrouper les utilisateurs par section,
sous-section. Tandis que les rôles permettent de définir un ensemble
d'utilisateur ayant des droits et des actions spécifiques à remplir dans
le cadre de l'application.

#### Groupes

Les groupes utilisateurs identifiés en séances sont les suivants :

-   utilisateurs COGIP : ce groupe contient tous les utilisateurs de
    l'application,
-   département qualité : ce groupe contient les membres du département
    qualité.

### Les rôles

Les différents rôles sont :

-   opérationnels :
    -   éditer des fiches de domaine de référence
    -   consulter les fiches qualité applicables

-   rédacteur de fiche qualité, qui peut :
    -   créer des fiches qualité
    -   être responsable d'une fiche qualité
    -   éditer une fiche qualité dont il est responsable

-   validateur de fiche qualité, qui peut :
    -   être responsable d'une fiche qualité
    -   éditer la partie remarque d'une fiche qualité en validation dont
        il est responsable

-   responsable qualité, qui peut :
    -   passer une fiche à l'état applicable
    -   gérer le cycle de validation

## Familles

La notion de famille est un élément fondamental de Dynacase. En effet,
une famille décrit la structure des éléments métiers manipulés dans
l'application que l'on appellera par la suite document.\
Une famille contient deux types d'informations :

-   des propriétés : son nom logique, son profilage...
-   son contenu informationnel : celui-ci se décline en deux notions :
    -   les attributs : ce sont les types d'information que l'on peut
        intégrer dans un document (typiquement une date, un titre...),
    -   les paramètres : ce sont des types d'information dont la valeur
        est valable pour l'ensemble des documents d'une famille. On les
        utilise généralement pour des éléments de fonctionnement, par
        exemple à quel groupe doit être envoyé le mail de confirmation
        du passage d'une fiche à l'état applicable.

Nous allons dans la suite de ce chapitre détailler les familles qui ont
été identifié en précisant leur implémentation. Les attributs
constituant la famille seront détaillés dans des sous chapitres et sous
la forme de tableau

### Domaine de référence

#### Introduction

Le domaine de référence doit permettre de :

-   stocker un nom de domaine
-   stocker un tableau de sous domaine de ce domaine (calculé
    automatiquement)
-   indiquer un domaine parent

#### Attributs

##### Frame : Description

  --------------------------------------------------------------------------
  Nom              Type         Commentaire
  ---------------- ------------ --------------------------------------------
  Nom              Text         Cet élément est obligatoire pour pouvoir
                                sauvegarder le document

  Description      HTML text    

  Parent           Relation     La liste des éléments présentés ne
                                comprend:\
                                - ni les documents ayant pour parent le
                                document en cours\
                                - ni le document en cours
  --------------------------------------------------------------------------

##### Array : Sous domaines

Cet array est stocké dans une frame de même nom. Son contenu est calculé
automatiquement, il n'est donc pas éditable.

  Nom              Type         Commentaire
  ---------------- ------------ --------------------------------------------
  Nom              Relation     Cet élément est calculé automatiquement

#### Paramètres

NA

#### Droits et autres actions

Tous les membres du groupe "utilisateurs COGIP" peuvent créer un domaine
de référence.\
L'ensemble des liens entre les domaines de références pourront être
exportés sous la forme d'un graphique.

### Fiche qualité

##### Introduction

La fiche de qualité doit :

-   avoir une référence unique,
-   avoir un rédacteur et un validateur responsable,
-   stocker fichier contenant la fichier fiche de qualité,
-   contenir sa fiche de remarque

Le titre d'un document fiche de qualité est calculé avec la formule
suivante reference\_titre

#### Attributs

##### Frame : Description

Cette frame est comprise dans une tab Description.

  --------------------------------------------------------------------------
  Nom              Type         Commentaire
  ---------------- ------------ --------------------------------------------
  Titre            Texte        Obligatoire pour sauvegarder et deux fiches
                                ne peuvent pas avoir le même titre

  Description      Texte long   

  Référence        Nombre       Non éditable et calculé automatiquement
  --------------------------------------------------------------------------

##### Frame : Contenu

Cette frame est comprise dans une tab Contenu.

  Nom              Type        Commentaire
  ---------------- ----------- -------------------------------------------
  Fichier Remarque Fichier     Obligatoire pour sauvegarder

##### Array : fiche de relecture

Cet array est compris dans une frame ayant le même nom qui est elle même
inclus dans une tab Fiche de relecture.

  --------------------------------------------------------------------------
  Nom              Type         Commentaire
  ---------------- ------------ --------------------------------------------
  Remarque         HTML texte   Contenu de la remarque

  Validateur       Relation     Nom du validateur ayant effectué la remarque

  Pris en compte   Énuméré      Valeur nul par défaut, vrai, faux \
                                Indique si la remarque a été prise en compte
  --------------------------------------------------------------------------

#### Paramètres

NA

#### Droits et autres actions

Seul les membres du groupe "Rédacteur" peuvent créer des fiches
qualités.

### Fiche qualité (historique)

##### Introduction

Cette famille est une fiche de qualité permettant de stocker les fiches
qualités existants avant la mise en place de l'application. Elle est
donc plus simple que la fiche de qualité vue précédemment car
l'historique de relecture n'est pas importé.

#### Attributs

##### Frame : Description

Cette frame est comprise dans une tab Description.

  --------------------------------------------------------------------------
  Nom              Type         Commentaire
  ---------------- ------------ --------------------------------------------
  Titre            Texte        Obligatoire pour sauvegarder et deux fiches
                                ne peuvent pas avoir le même titre

  Description      Texte long   

  Référence        Nombre       Non éditable et calculé automatiquement
  --------------------------------------------------------------------------

##### Frame : Contenu

Cette frame est comprise dans une tab Contenu.

  Nom              Type        Commentaire
  ---------------- ----------- -------------------------------------------
  Fichier Remarque Fichier     Obligatoire pour sauvegarder

#### Paramètres

NA

#### Droits et autres actions

Personne ne peut créer des fiches qualité.

## Cycle de vie

Le cycle de vie est un élément à part qui s'applique à une ou des
familles et qui permet de définir un cycle d'action qui s'applique aux
documents de la familles.

### Introduction

Il a été décidé que les documents du type domaine de référence et du
type fiche qualité (historique) n'auraient pas de cycle de vie.\
Le travail de définition a donc porté sur le cycle de vie de la famille
fiche de qualité.

### Description du cycle de vie

![Schéma du cycle de vie](./cycle_de_vie.png "Schéma du cycle de vie")

Il est à noter que durant tout le cycle de vie, les points suivants sont
toujours valables :

-   les administrateurs peuvent voir/éditer/supprimer n'importe quel
    documents,
-   les groupes validateur, rédacteur et responsable qualité peuvent
    voir tous les documents.

#### A1 : Rédaction

Cette activité permet au créateur de la fiche de qualité d'éditer
celle-ci jusqu'à qu'il considère qu'elle est suffisamment mature pour un
premier cycle de relecture (uniquement sur la partie Description). A ce
moment, il passera celle-ci à l'activité validation par le biais de la
transition "Passage en validation". Durant cette activité, seul
l'utilisateur ayant crée la fiche peut voir/éditer celle-ci.

#### T1 : Passage en validation

Cette transition permet au créateur d'indiquer que sa fiche est prête
pour la relecture. Il doit sélectionner le validateur est responsable de
la relecture. Un mail est envoyé au validateur.

#### A2 : Validation

Cet activité permet au validateur en charge du document d'éditer
uniquement une partie de la partie fiche de relecture du document
(ajouter une ligne dans le tableau et éditer la colonne remarque). Une
fois que le validateur a complété l'ensemble de ses remarques, il peut
soit :

-   utiliser la transition "retour au brouillon", s'il estime que des
    précisions doivent être apportées,
-   utiliser la transition "passage en approbation", s'il estime que le
    document est prêt à être applicable.

Seul le validateur peut éditer le document lors de cette transition.

#### T2 : Retour au brouillon

Cette transition permet au validateur de la fiche d'indiquer que
celle-ci doit être retravaillée. Un mail est envoyé au créateur de la
fiche pour lui notifier qu'il doit la reprendre. De plus, un timer est
attaché à la fiche pour indiquer que si celle-ci est toujours à l'état
"Brouillon" trois semaines après cette transition, le créateur de la
fiche est re-notifié avec en copie le groupe "Responsable qualité".

#### T3 : Passage en approbation

Cette transition permet au validateur d'indiquer que la fiche est prête
à être validée par le responsable qualité. Celui-ci reçoit un mail pour
lui notifier qu'il doit relire la fiche.

#### A3 : Approbation

Cette activité permet au responsable qualité de vérifier le travail
effectué sur la fiche. Personne ne peut éditer le fiche durant cette
activité. Une fois qu'il a relu le document, le responsable qualité peut
:

-   utiliser la transition "retour au brouillon", s'il estime que des
    précisions doivent être apportées,
-   utiliser la transition "passage en applicable", s'il estime que le
    document est applicable.

#### T4 : Retour au brouillon

Cette transition permet au responsable qualité de la fiche d'indiquer
que celle-ci doit être retravaillée. Celui-ci doit motiver sont renvoi
en qualité à l'aide d'un champ texte qui est présenté lors de la
transition. Un mail est envoyé au créateur de la fiche pour lui notifier
qu'il doit la reprendre. De plus, un timer est attaché à la fiche pour
indiquer que si celle-ci est toujours à l'état "Brouillon" trois
semaines après cette transition, le créateur de la fiche est re-notifié
avec en copie le groupe "Responsable qualité".

#### T5 : Passage en applicable

Cette transition permet au responsable qualité d'indiquer que la fiche
est applicable. Un mail est envoyé au rédacteur et au validateur pour
les notifier.

#### A4 : Diffusion

Cette activité indique que la fiche est applicable. La partie
"Description" est consultable pour l'ensemble des membres du groupe
"utilisateurs COGIP", l'intégralité de la fiche est consultable par les
membres des groupes "rédacteur qualité", "validateur qualité" et
"responsable qualité". Les membres du groupe "responsable qualité"
peuvent décider de passer la fiche en "Non applicable" en utilisant la
transition "Non applicable". Il est à noter que cette activité est
associée à un état. C'est à dire que le passage dans l'activité
diffusion passe automatiquement le document à l'état applicable, ce qui
permet de tracer ce document et de retrouver toutes les version d'un
document applicable.

#### T6 : Passage en révision

Cette transition est automatique et à lieu suivant une périodicité qui
est définie dans la fiche qualité (typiquement 6 mois). Lors de cette
transition le document passe à l'activité rédaction, c'est à dire que le
document applicable reste le seul consultable mais qu'une nouvelle
version du document est initialisée pour d'éventuelle modifications. Le
créateur de la fiche reçoit un mail pour lui indiquer qu'il doit étudier
à nouveau cette fiche.

#### T7 : Abandon

Cette transition permet au responsable qualité ou au rédacteur de la
fiche qualité de déclarer la fiche comme abandonnée. Un mail est envoyé
au groupe responsable qualité, au rédacteur et au validateur de la fiche
qualité.

#### E3 : Abandonné.

Cet état est un état final aucune activité ne s'y applique. Une fois le
document dans cet état, il ne peut plus changer d'état et n'est plus
éditable. Seul les membres des groupes "rédacteur qualité", "validateur
qualité" et "responsable qualité" peuvent le consulter.
