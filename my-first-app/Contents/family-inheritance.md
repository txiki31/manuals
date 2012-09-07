# Family : Inheritance

## Introduction

Nous allons dans ce tutoriel aborder la notion d’héritage dans les
familles Dynacase. Celle-ci est similaire à celle implémentée dans
PHP.  
On peut donc définir une famille parente : la famille fille
héritera de tous les attributs et paramètres de la famille mère.

Le mécanisme d’héritage de famille de Dynacase est abstrait par le
Dynacase Studio. Il vous suffit donc de déclarer à Dynacase de
quelle famille hérite votre famille et la famille fille présentera
tous les hérités de la famille mère et des familles de la famille
mère, cela vous permet de travailler en connaissance de cause avec
l’ensemble des informations à votre disposition. Dynacase Studio se
charge de créer automatiquement le fichier d’héritage n’indiquant
que les éléments modifiés et les éléments ajoutés, ce qui vous
permet de construire facilement et de manière sûre votre famille
fille.

Nous allons voir dans ce tutoriel, comment :

-   importer une famille dans votre contexte Eclipse,
-   hériter d’une famille,
-   intégrer les familles ajoutées.

## Importation de la famille existante

Vous devez commencer par télécharger le package suivant
[famille fiche qualité abstraite](http://dynacase.org/tuto/family_abstract_quality.dcs).
Ce package contient la définition d’une famille fournie par
Dynacase et ré-exporter par la plateforme. Ce format permet de
partager une famille déjà déployée sur un serveur ou de partager
une définition entre différents programmeur.

Ce fichier s’importe en utilisant le menu Dynacase de votre
application Eclipse. Vous allez donc importer la famille
*abstract quality* (QCO\_QUALITY\_ABSTRACT).

Une fois cette famille importée vous pouvez constater que son
répertoire et ces fichiers ont été ajoutés. Dans ce tutoriel, nous
allons utiliser cette famille comme base pour les développements
des familles :

-   *fiche de qualité*,
-   *fiche de qualité (historique)*.

Si vous ouvrez la vue attributs de cette famille, vous pouvez voir
que celle-ci contient l’ensemble des attributs communs aux familles
*fiche de qualité* et *fiche de qualité (historique)*.

Cette famille contient donc les attributs (non structurant)
suivants :

-   Titre,
-   Description,
-   Référence,
-   Fichier Remarque.

Vous pouvez remarquer que ces attributs représentent l’intégralité
des attributs de la famille *fiche de qualité (historique)*, nous
pourrions donc utiliser cette famille pour représenter la fiche de
qualité historique. Nous allons quand même créer une nouvelle
famille car fonctionnellement ces deux familles n’implémenteront
pas les mêmes éléments.

## Création de la famille fiche de qualité (historique)

Nous allons commencer par créer une nouvelle famille en utilisant
le menu créer une famille de l’application Dynacase. Vous allez
spécifier comme nom logique : QCO\_QUALITY\_HIST, ensuite vous
allez spécifier la famille père qui est bien évidemment
QCO\_QUALITY\_ABSTRACT.

Vous pouvez ensuite ajouter :

-   *Translate notice* : Legacy quality document,
-   *Family Icon* : Vous pouvez utilisez l’icône mise à votre
    disposition.

Vous pouvez ensuite voir que vous héritez de l’ensemble des
attributs placés dans la famille mère de cette famille.

Le contenu de cette famille étant suffisant nous allons pour le
moment le laisser tel quel.

## Création de la famille fiche de qualité

Nous allons commencer par créer une nouvelle famille en utilisant
le menu créer une famille de l’application Dynacase. Vous allez
spécifier comme nom logique : QCO\_QUALITY, ensuite vous allez
spécifier la famille père qui est bien évidemment
QCO\_QUALITY\_ABSTRACT.

Vous pouvez ensuite ajouter :

-   *Translate notice* : Quality document,
-   *Family Icon* : Vous pouvez utilisez l’icône mise à votre
    disposition.

Nous allons maintenant ajouter les attributs manquants pour
compléter cette famille. Pour ce faire, il vous faut aller dans
l’onglet *attributs* du formulaire d’édition et ajouter les
attributs correspondant à la fiche de relecture.

  -----------------------------------------------------------------------
  Nom logique             Type                Sous Type       Options        
  ----------------------- ------------------- ----------- ---------------
  QCO\_REVIEW             SET                 NA          TranslationKey=
                                                              Review         
  
  QCO\_A\_REVIEW          ARRAY               NA          TranslationKey=
                                                              Review         
  
  QCO\_REVIEW\_REMARK     GENERICATTRIBUTE    HTMLTEXT    TranslationKey=
                                                              Remark         
  
  QCO\_REVIEW\_VALIDATOR  GENERICATTRIBUTE    RELATION    TranslationKey=
                                                             Validator      
  
  QCO\_REVIEW\_CHECKED    GENERICATTRIBUTE    BOOLEAN     TranslationKey=
                                                              Checked        
  -----------------------------------------------------------------------

Vous ajoutez ces éléments après le set de contenu de la famille
mère.

Vous pouvez visualiser le XML complet de la famille hérité. Cet XML
contient les instructions permettant à Dynacase de reconstruire la
famille en cours à l’aide de ses familles parents. Il est structuré
de la manière suivante, tous les attributs sont indiqués sans
imbrications avec pour indication de placement le nom de leur
attribut père FATHER et le nom de l’attribut présent avant (BEFORE)
et après lui (AFTER). Attention, toutefois les after et les before
sont donnés par ceux qui sont présent au moment de la construction
de l’arbre, vous pouvez donc voir un décalage avec les attributs
avant et après dans l’arbre finalement construit.

## Déploiement et test

Vous allez maintenant déployer vous deux nouvelles familles en
cliquant sur le bouton déployer dans la barre d’outil.

Une fois votre application déployée vous pouvez consulter les deux
familles que vous venez d’importer.



