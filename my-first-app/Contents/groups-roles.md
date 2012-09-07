# Groups and role

## Introduction

Nous allons voir dans ce tutoriel deux notions de Dynacase utilisées
dans la gestion des utilisateurs et leurs interactions avec
l'application.\
Les notions sont :

-   les groupes : un groupe est une structure de donnée qui peut stocker
    soit des utilisateurs, soit d'autres groupes (on parle alors de
    sous-groupe). Un groupe ne sert qu'à rassembler des utilisateurs et
    peut-être utilisé comme pointeur lors de l'envoi de mail.
-   les rôles : un rôle est un marqueur qui peut s'appliquer à des
    groupes et/ou des utilisateurs et ils donnent aux utilisateurs
    possédant le rôle (via leurs groupes ou directement) des accès à des
    fonctionnalités particulières soit via les cycle de vie, soit via
    les profils.

## Création des groupes et rôles

### Création des groupes

Nous allons tout d'abord créer les groupes propres à notre application.
Il en existe deux :

-   le groupe général des utilisateurs
-   le groupe département qualité

Pour ce faire, nous allons utiliser le menu *Dynacase*, sélectionner le
sous-menu *Documents Systèmes* et puis l'option *Groupe*.\
Un nom logique vous est alors demandé, vous allez rentrer
*QCO\_GRP\_USER* et valider. L'IHM suivante vous est présentée.

**Capture écran**

Vous allez complété le groupe en indiquant sa traduction par défaut
*COGIP users*.\
Nous allons maintenant créer le deuxième groupe. Je vous laisse suivre
la même procédure en changeant le nom logique par *QCO\_GRP\_QUALITY* et
la traduction en *Quality crowd*.\
Il vous faut maintenant indiquer que le groupe *Quality crowd* est un
sous-groupe de *COGIP users*. Pour cela, vous éditez l'attribut *fathers
groups* de *Quality crowd* et y ajoutée *QCO\_GRP\_USER*.

## Création des rôles

Nous allons maintenant créer les rôles. Il en existe quatre :

-   opérationnel
-   rédacteur
-   valideur
-   responsable qualité

Pour créer un rôle, la démarche est similaire à la création d'un groupe.
Vous allez dans le menu *Dynacase*, sous section *Documents systèmes* et
vous sélectionnez l'option *Rôle*.\
Une fois cette option sélectionnée, on vous demande le nom logique et la
traduction par défaut.

  ------------------------------------------------------------------------
  Nom logique         Traduction
  ------------------- ----------------------------------------------------
  QCO\_ROLE\_OPERA    Operationnal

  QCO\_ROLE\_REDAC    Redactor

  QCO\_ROLE\_VALI     Validator

  QCO\_ROLE\_RESP\_QU Quality manager
  AL                  
  ------------------------------------------------------------------------

# Conclusion

Une fois l'ensemble de vos groupes et rôles crées vous pouvez les
intégrer en cliquant sur le bouton déployer. Vous pouvez retrouver
groupes et rôles dans l'interface de gestion des utilisateurs comme
illustré ci-dessous :

**Capture écran**
