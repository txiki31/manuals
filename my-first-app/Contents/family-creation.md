# Family : The creation

## Introduction

La famille est une des notions de base de Dynacase. Elle est
comparable à la notion de classe en conception orienté objet. C'est
à dire qu'une famille est une structure de donnée indiquant :

-   les types d'information stockés dans la famille,
-   la structure sémantique des informations de la familles
    (groupement d'élément d'informations unitaire),
-   les propriétés de la famille (cycle de vie, représentation,
    etc)

Une famille est composée de :

-   les propriétés : elles donnent des informations sur le
    comportement de la famille et ses relations avec les autres
    éléments de la plateforme
-   attribut : les attributs sont de deux natures :
    -   les attributs structurants : ils ne portent pas d'information
        mais indique que les attributs qu'ils englobent appartiennent au
        même bloc sémantique ou qu'ils sont colonnes d'un tableau,
    -   les attributs informatifs : ils indiquent la structure de
        l'information qui va être stockée dans la famille (texte, date,
        numérique, ...)

-   paramètre : les paramètres sont de même nature que les
    attributs mais ils sont valables au sein de tous les éléments d'une
    même famille avec la même valeurs. Ils sont généralement utilisés
    pour paramétrer des comportements ()envoi de mail à un groupe
    donné, ...) toute en laissant la possibilité aux administrateur de
    la plateforme de modifier le paramétrage.

La famille produit des *Documents*. Si on reprend notre métaphore
qui assimile les familles à des classes, les documents sont des
objets. C'est à dire qu'ils sont l'unité qui contient l'information
dans la structure est décrite dans la famille.

Si on prend pour exemple la famille *Domaine de référence*. La
famille est un élément déclaratif qui décrit un
*Domaine de référence*, elle indique que celui-ci doit contenir un
titre, une description, etc. Tandis que le document est lui le
domaine de référence *Chimie organique* qui a pour titre
*Chimie organique* et qui contient le descriptif de la chimie
organique.

## Construction de la famille

Nous allons dans cette première partie construire notre première
famille. Nous allons commencer par la famille la plus simple de
notre cahier des charges : la famille *Domaine de référence*.

Pour ce faire, je vous propose de reprendre le projet que nous
avons initié lors du tutoriel précédent, si vous ne l'avez pas vous
pouvez le trouver sur notre
[site](http://www.dynacase.org/tuto/projet/tuto3.zip).  
Une fois le projet chargé dans Eclipse et la perspective Dynacase
ouverte, vous pouvez créer votre famille.

Pour cela, vous devez :

1.  Allez dans le menu Dynacase et sélectionner l'option "new
    Family"
2.  remplir le formulaire de création de la famille, vous devez
    indiquer le nom logique de la famille. Ce nom est utilisé en
    interne pour référencer la famille, il doit donc respecter la
    convention suivante : être compris entre 1 et 63 caractères
    alphanumériques et \_ excepté pour le premier qui doit être
    numérique. Une bonne pratique mise en place sur la plupart des
    projets dynacase consiste a préfixer le nom des familles par un
    trigramme correspondant à leur module de création de notre cas QCO
    (pour QualitéCOgip), le nom de notre famille sera donc
    QCO\_TOPIC\_REFERENCE.

Une fois le nom logique indiqué, la famille est crée. Une famille
est toujours contenues dans son répertoire de référence, lui même
dans le répertoire families. Son répertoire de référence porte le
nom logique de la famille. Nous allons examiner le contenu de ce
répertoire, il contient :

-   un fichier QCO\_TOPIC\_REFERENCE\_STRUCTURE.xml, ce fichier
    contient la structure de la famille est peut-être édité à l'aide
    d'une vue particulière qui permet de guider le développeur, nous
    verrons dans la suite de ce tutoriel le fonctionnement de cet
    élément
-   un fichier classQCO\_TOPIC\_REFERENCE.php, ce fichier contient
    la classe php de la famille qui permet de paramétrer son
    comportement, nous verrons son utilité dans le tutoriel
    **[insérer une référence]**.
-   **REPRENDRE LA DOC DE MAT pour voir ce qui est initialisé par défaut**

Nous allons maintenant paramétrer la famille, en utilisant
l'interface de configuration prévue à cette effet, pour ce faire
ouvrer le document QCO\_TOPIC\_REFERENCE\_STRUCTURE.xml.

### Édition des propriétés de la famille

Nous allons commencer par configurer les propriétés de la famille,
vous pouvez voir que par défaut l'interface de paramétrage affiche
le formulaire suivant :  
**INSERER UNE CAPTURE D ECRAN**

Nous allons parcourir et compléter le formulaire :

-   *Name* : le premier élément est le nom logique de la famille
    qui n'est pas modifiable, il est fourni à titre indicatif
-   *Version* : la version de la famille, cette propriété est
    utilisée lors de la mise à jour. Il vous permet de vous assurer que
    vous ne mettez pas à jour une famille avec une version antérieure
    de celle-ci. Nous allons le laisser à sa valeur par défaut 0.1
-   *Translate notice* : Cette notice permet d'aider à la
    traduction, elle doit indiquer en anglais une traduction possible
    pour aider les différents traducteurs. Elle est utilisée en
    fallback si aucune notice de traduction est définie, il est
    conseillé de le remplir uniquement avec des caractère ASCII et en
    anglais. Pour plus d'information, veuillez consulter le tutoriel
    sur l'internationalisation **insérer une référence**. Nous ajoutons
    la notice avec *Topic*,
-   *Family Icon* : Icône de la famille, cette icône est affiché
    pour représenter la famille et les documents de celle-ci. Vous
    pouvez à cet emplacement ajouter l'icône mise à votre disposition
    [icône](http://www.dynacase.org/tuto/icone/qco_topic_reference.png),
-   *Parent Family* : Cet élément porte la référence à la famille
    parent dont hérite la famille en cours. Pour plus d'information sur
    l'héritage, consulter le tutoriel sur l'héritage
    **insérer référence**. Nous le laissons vide.
-   *Document Root Dir* : Cet élément porte la référence du dossier
    racine dans lequel seront contenu les documents. Pour plus
    d'information sur les dossiers, consulter **insérer référence**.
    Nous le laissons vide.
-   *Auto revision* : indique si une révision du document est
    ajoutée à chaque modification de celui-ci. Nous le laissons à sa
    valeur par défaut "Non auto révisable".
-   *Class file* : Cet élément est pré-rempli avec le nom du
    fichier contenant la classe PHP générée par l'application et ne
    peut pas être modifié,
-   *Title function* : Cet élément référence une méthode utilisée
    pour calculer le titre des documents de cette famille. Par défaut,
    il est rempli avec la méthode getTitle qui crée un titre sous la
    forme NOM\_LOGIQUE\_FAMILLE\_refuniquedocument. Vous pouvez
    modifier cette élément soit en :
    -   modifiant le contenu de l'appel à la fonction sous la forme
        :chaine au format sprintf, liste des valeurs
    -   appelant votre propre fonction définie dans la classe de la
        famille

-   *Version function* : Cet élément permet de calculer le numéro
    de version d'une famille, soit en utilisant la fonction complétée
    par défaut getVersion qui augmente de 1 la version à chaque
    nouvelle révision, soit en appelant votre propre méthode définie
    dans la classe de la famille
-   *Profil* : Cet élément référence un document profil de famille.
    Ce document permet d'indiquer qui peut créer, créer manuellement,
    etc des documents de cette famille
-   *View Control* : Cet élément référence un Contrôle de vue. Ce
    document permet d'indiquer quelle représentation est associée à un
    document en fonction de différents paramètres. Pour plus
    d'information, veuillez consulter le tutoriel sur les
    représentation **insérer une référence**.
-   *Document default profil* : Cet élément référence un document
    de profil de document. Ce profil est associé par défaut au nouveau
    document de la famille et permet d'indiquer qui peut voir,
    modifier, supprimer,etc les documents.
-   *Workflow* : Cet élément référence un document de workflow. Ce
    workflow sera associé aux documents de la famille. Pour plus
    d'information sur les cycles de vie, consulter le tutoriel sur
    l'héritage **insérer référence**. Nous le laissons vide.

Vous avez donc complété les propriétés de la famille.

### Éditions des attributs de la familles

Nous allons ensuite spécifier les attributs de la famille. Pour ce
faire, veuillez cliquer sur l'onglet attributs du formulaire de
saisie.

Pour ajouter des éléments, il faut suivre la procédure suivante :

1.  Cliquer sur le bouton "Add" et sélectionner un type d'attribut
    à ajouter,
2.  Indiquer le nom de l'attribut, celui-ci doit être écrit en
    caractère alphanumérique, majuscule et peut utiliser le caractère
    \_.
3.  une fois votre attribut ajouté, vous pouvez le déplacer dans
    l'arbre représentant l'arborescence des attributs pour modifier son
    emplacement.

Nous allons maintenant mettre en place les différents attributs
indiqués dans la spécification, veuillez ajouter les éléments
suivants:

  -----------------------------------------------------------------------
  Nom logique                 Type                Sous Type   Options
  --------------------------- ------------------- ----------- -----------
  QCO\_TOPREF\_DESCRIPTION    SET                 NA          Translation
                                                              Key=Descrip
                                                              tion
  
  QCO\_TOPREF\_DESC\_NAME     GENERICATTRIBUTE    TEXT        Translation
                                                              Key=Name
  
  QCO\_TOPREF\_DESC\_DESCRIPT GENERICATTRIBUTE    HTMLTEXT    Translation
  ION                                                         Key=Descrip
                                                              tion
  
  QCO\_TOPREF\_DESC\_PARENT   GENERICATTRIBUTE    RELATION    Translation
                                                              Key=Parent
                                                              Topic
  
  QCO\_TOPREF\_F\_CHILD\_TOPI SET                 NA          Translation
  C                                                           Key=Childre
                                                              n
                                                              Topic
  
  QCO\_TOPREF\_A\_CHILD\_TOPI ARRAY               NA          Translation
  C                                                           Key=Sub
                                                              Topics
  
  QCO\_TOPREF\_CHILD\_TOPIC   GENERICATTRIBUTE    RELATION    Translation
                                                              Key=Name
  -----------------------------------------------------------------------

Vous obtenez l'arbre suivant :

**INSERER ICI UNE IMAGE du résultat**

### Déploiement

Avant le déploiement, nous allons référencer la famille dans
l'application familyXplorer.
**Demander à quelqu'un (Eric) comment on fait**

Nous allons maintenant déployer cette famille. Pour cela veuillez
cliquer sur le bouton déployer dans le menu dynacase (si votre
action déployée n'est pas configurée, veuillez vous référer au
tutoriel).  
La procédure de déploiement ouvre la fenêtre de déploiement et
affiche un compte rendu une fois le déploiement terminé.

**INSERER ICI UNE IMAGE du résultat**

## Conclusion

Votre famille est maintenant déployée sur votre serveur de test.
Nous allons maintenant faire un tour de celle-ci.

Veuillez vous connecter sur votre environnement de test et aller
dans l'application familyXplorer.

Vous pouvez voir par défaut que votre nouvelle famille est présente
dans le menu de gauche avec son icône.

**Insérer ici une image de family explorer**

Nous allons maintenant créer un document de cette famille et le
visualiser en édition et en consultation.

Pour ce faire, veuillez suivre les instructions suivantes :

1.  Cliquer sur le bouton représentant la famille,
2.  Sélectionner l'option créer un document,
    **INSERER ICI UNE IMAGE DE L'INTERFACE DE CREATION**,
3.  Vous remplissez ensuite les différents éléments du formulaire,
4.  Vous cliquez sur sauver

Vous venez de créer votre premier document, vous pouvez remarquer
que :

-   son nom a été généré automatiquement avec la valeur par défaut,
    soit QCO\_TOPIC\_REFERENCE\_xxxx où xxxx est le numéro
    d'identifiant unique du document,
-   l'application n'étant pas traduite les libellés restent sous la
    forme de leur TranslationKey.

Vous savez maintenant construire une famille simple et la déployer.
Dans le prochain tutoriel nous aborderons l'héritage.



