# Permissions

## Introduction

Nous allons dans ce tutoriel évoquer la gestion droits applicatifs, des
droits documentaires et droits de workflow de Dynacase. En effet, ces
notions sont naturellements bien distinctes :

-   les droits applicatifs : ces droits s'appliquent aux actions. On
    peut en définir un et l'associer à une ou plusieurs actions pour
    indiquer que seuls les utilisateurs ayant ce droit (ou un rôle
    possédant ce droit) pourront utiliser cette action. Un droit
    applicatif n'est valable que dans le contexte de son application.
-   les droits documentaires : ces droits s'appliquent aux documents.
    Ils sont de deux natures différentes :
    -   les droits de familles : ces droits définissent des actions
        communes à l'ensemble des documents d'une famille (en règle
        général créer),
    -   les droits de documents : ces droits référence au niveau d'un
        document quelles sont les actions disponibles pour ce document.

## Mise en pratique

### Droit applicatif

Nous allons tout d'abord définir un droit applicatif pour notre action
*QCO\_EXPORT\_TOPICS*. Pour ce faire, nous allons dans l'application
*COGIP\_APPLICATION* et nous sélectionnons l'onglet *Applicative
rights*. Vous voyez l'interface suivante :

**Insérer ici capture écran**

Vous ajoutez un droit, en cliquant sur le bouton *Add* et vous rentrez
un nom logique : *RIGHT\_EXPORT*. Vous pouvez voir en dessous le nom
logique généré par Dynacase Studio *COGIP\_APPLICATION\_RIGHT\_EXPORT*,
ce nom est généré de manière automatique pour s'assurer que il existe
bien uniquement pour l'application *COGIP\_APPLICATION*.

Une fois ce droit ajouté, vous devez l'ajouter à votre action. Pour ce
faire, vous devez retourner dans l'onglet *actions* de votre
application, sélectionner l'application qui nous interesse
*QCO\_EXPORT\_TOPICS* et faire dérouler le champ *Right* et sélectionner
le droit *RIGHT\_EXPORT*.

Votre action n'est maintenant accessible qu'aux utilisateurs possédant
le droit d'accès à cette action. Nous allons donc ajouter au profil
applicatif de votre application le droit *RIGHT\_EXPORT* au rôle
*QCO\_ROLE\_RESP\_QUAL*. Pour ce faire, vous allez dans l'onglet *Profil
rights* et là l'IHM suivante vous est proposée :

**Insérer ici capture écran**

Vous ajoutez une ligne dans cette matrice et vous insérer en début de
ligne la référence du rôle *QCO\_ROLE\_RESP\_QUAL* et vous cochez la
case de la colonne *RIGHT\_EXPORT*.

### Profil de famille

Nous allons maintenant créer un profil de famille. Ce document permet
d'indiquer qui a le droit de créer, créer manuellement, ... des
documents d'une famille. Nous allons créer le profil restreignant la
création des documents de qualité aux utilisateurs ayant le rôle
*quality user*. Pour ce faire, veuillez sélectionner dans le menu
*Dynacase* le sous menu *Documents internes* l'option *Profil de
famille*. Un nom logique vous est alors demandé, vous indiquez
*QCO\_FPROFIL\_QUALITY*. Ensuite la famille associée vous est demandée,
vous faites dérouler le menu et sélectionnez *QCO\_QUALITY*.

Un profil de famille est maintenant créé et disposé dans le répertoire
de la famille *QCO\_QUALITY* et l'IHM suivante est affichée.

**Insérer ici capture écran**

Vous pouvez voir la liste des actions disponibles :

-   *créer* : qui permet à un utilisateur de créer un document via du
    code qui est exécuté en son nom
-   *créer directement* : qui permet à un utilisateur de créer un
    fichier via l'IHM.

Vous ajoutez une ligne en spécifiant que le rôle associé à cette ligne
est *QCO\_ROLE\_QUALITY\_USER* et lui donner les droits *créer* et
*créer directement*.\
Il ne vous reste plus qu'à associer votre document de profil de famille
avec la famille. Pour ce faire, veuillez ouvrir la famille et
sélectionner le sous onglet *Proriétés* dans cet onglet vous devez
compléter la valeur de la propriété *Default family profil* avec le nom
logique *QCO\_FPROFIL\_QUALITY*.

### Profil de document

Nous allons créer le profil de document par défaut pour les rapports de
qualité de qualité. Nous allons créer un profil de document restreignant
l'affichage et l'édition aux seuls utilisateurs ayant le rôle *quality
user*. Pour ce faire, veuillez sélectionner dans le menu *Dynacase* le
sous menu *Documents internes* l'option *Profil de document*. Un nom
logique vous est alors demandé, vous indiquez
*QCO\_DOCUMENT\_PROFIL\_QUALITY*. Ensuite la famille associée est
demandée, vous faites dérouler le menu et sélectionnez *QCO\_QUALITY*.

Un profil de document est maintenant créé et disposé dans le répertoire
de la famille *QCO\_QUALITY* et l'IHM suivante est affichée.

**Insérer ici capture écran**

Vous pouvez voir la liste des actions disponibles :

-   *consulter* : qui permet de consulter le document,
-   *éditer* : qui permet d'éditer le document,
-   *envoyer par mail* : qui permet de transmettre par mail le document.

Vous ajoutez une ligne en spécifiant que le rôle associé à cette ligne
est *QCO\_ROLE\_QUALITY\_USER* et lui donner tous les droits.\
Il ne vous reste plus qu'à associer votre document de profil de document
avec la famille. Pour ce faire, veuillez ouvrir la famille et
sélectionner le sous onglet *Proriétés* dans cet onglet vous devez
compléter la valeur de la propriété *Default document profil* avec le
nom logique *QCO\_DOCUMENT\_PROFIL\_QUALITY*.

## Conclusion

Vous pouvez maintenant déployer votre projet et vérifier en utilisant
les différents utilisateurs fournis si les profils s'appliquent bien.
