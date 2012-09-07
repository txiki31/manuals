# Dynacase : the beginning

## Introduction

Dans ce tutoriel, vous allez avoir un premier contact avec la plateforme
en l'installant via son outil de configuration [Dynacase
Control](http://www.anakeen.com/dynacase-control) et en créant et
installant un premier module Dynacase que vous avez conçu.

L'objectif de ce tutoriel est de mettre en place les éléments suivants :

-   Environnement de test : une machine virtuelle contenant :

    -   ubuntu 10.04 LTS 2
    -   les pré-requis de Dynacase Platform et de Dynacase Studio
    -   Dynacase Studio
    -   Dynacase Platform

-   Environnement de développement :
    -   Eclipse PDT
    -   Dynacase Studio
    -   Eclipse RSE
    -   gTed

Et dans un second temps nous allons initier un projet studio et le
déployer.

## Mise en place des environnements

### Environnement de test

Pré-requis :\
Pour compléter cette étape vous devez télécharger [Virtual
box](http://www.virtualbox.org/) et [Ubuntu Server 10.04
LTS](http://www.ubuntu.com/server/get-ubuntu/download) version 32 bit.
Vous devez aussi avoir des connaissances basiques de logiciel de
virtualisation et de l'utilisation d'une console Linux.

Tout d'abord, vous devez installer Virtual box et initier une nouvelle
machine virtuelle. Si vous ne savez pas installer une virtual box et un
système d'exploitation associé, nous vous conseillons le tutoriel
suivant [Tutoriel installation
virtualbox](http://www.siteduzero.com/tutoriel-3-36484-virtualisez-un-systeme-d-exploitation-avec-virtualbox.html#ss_part_2).

Vous devez ensuite configurer votre machine virtuelle pour permettre à
celle-ci un accès à internet, pour ce faire vous devez sélectionner dans
le menu de configuration de la machine l'option réseau et choisir
d'activer la carte réseau en mode NAT.

Lors de l'installation d'Ubuntu vous laissez les options par défaut et
vous choisissez le login/mot de passe : anakeen/anakeen.

Une fois fois votre machine virtuelle installée et configurée, vous
devez la lancer la machine virtuelle. Celle-ci vous propose de vous
connecter (voir image ci-dessous), vous rentrez alors le login et le mot
de passe (anakeen/anakeen).

Une fois connecté, vous allez télécharger et exécuter le script
d'installation des pré-requis et de Dynacase Control.

~~~~ {.Bash}
wget http://dynacase.org/tuto/script_install_control.sh
chmod 777 ./script_install_control.sh
sudo sh ./script_install_control.sh
~~~~

Un fois exécuté le script a :

-   installé les pré-requis à l'exécution de Dynacase Studio et Dynacase
    Control,
-   téléchargé et installé Dynacase Control.

Votre Dynacase Control est maintenant installé et prêt à fonctionner.
Vous devez maintenant préparer les éléments nécessaires à la création
d'un contexte. Un contexte est un environnement étanche dans lequel est
installer une instance de base de donnée. Pour initialiser le contexte,
vous pouvez utilisez le script fourni à cet effet par Dynacase Control.

~~~~ {.Bash}
wget http://dynacase.org/tuto/context-init.sh
chmod 777 ./context-init.sh
sudo sh ./script_install_control.sh
~~~~

Le script va successivement vous demander :

-   le nom du contexte : vous indiquez qualite-cogip
-   l'emplacement du contexte : /var/www/dynacase/qualite-cogip/
-   le type de base : postgresql
-   nom de la base : vous indiquez bdd-cogip
-   mot de passe de la base : cogip

Une fois ces éléments complétés le script a :

-   créé une base de données vide de type postgresql,
-   crée le répertoire /var/wwww/dynacase/qualite-cogip/,
-   configuré apache2 pour donner l'accès au répertoire avec les
    directives adéquates,
-   téléchargé et installé la plateforme dans le contexte nouvellement
    crée.

Vous pouvez maintenant, vous connecter à votre machine virtuelle via
l'adresse suivante dans un navigateur
http://adresse-ip-de-la-machine/dynacase/qualite-cogip/\
Si vous ne connaissez pas l'IP de votre machine vous devez entrer la
commande suivante :

    # sudo ifconfig

Elle apparaîtra à côté de la mention inet adr.

Votre navigateur vous présente la page suivante :

PAGE DE LOG DYNACASE A AJOUTER

### Environnement de développement

L'environnement de développement de Dynacase est basé soit sur Eclipse
PDT, soit sur Zend Studio. Il est bien sûr possible de développer en
utilisant des outils plus simple (gedit, notepad++, etc) mais cela n'est
pas recommandé car vous n'auriez pas accès à toutes les aides à la
saisie et les contrôles intégrés dans notre plateforme de développement.

Pour installer, la plateforme vous devez :

-   télécharger [Eclipse PDT](http://www.eclipse.org/pdt/downloads/) qui
    correspond à votre plateforme et le dézipper à l'endroit de votre
    choix,
-   lancer eclipse,
-   aller dans le menu helps \> install new software,
-   ajouter le update site : http://dynacase.org/dynacaseStudio/update/,
-   suivre ensuite la procédure d'installation.
-   relancer Eclipse

Il est ensuite conseillé pour faciliter l'interaction avec la machine
virtuelle d'installer les module [Eclipse
RSE](http://www.eclipse.org/tm/) et pour faciliter la traduction le
module [GTED](http://www.gted.org/#Installation). Vous pouvez utiliser
la même méthode décrite ci-dessus.

## Initialisation du projet et premier déploiement

### Initialisation du projet

Vous avez mis en place la base permettant sur Dynacase. Nous allons
maintenant initier le projet et le déployer.

Pour cela, il vous faut :

cliquer sur File, New Project

![Eclipse new project](eclipse_new_project.png)

vous devez devez ensuite sélectionner un projet de type Dynacase :

![Eclipse new project : type de projet](eclipse_new_project_kind.png)

il vous faut indiquer le nom du projet : qualite-cogip cliquer sur
suivant, sélectionner les paramètres du projet :

-   hérite de : familyXplorer
-   version dynacase : 4.0

L'application va créer l'arborescence de base d'un projet Dynacase et
vous le présenter dans Eclipse.

### Premier déploiement

Ce projet est un projet vide mais il est directement intégrable dans la
plateforme et nous donnera accès au fonctionnalité de son module père
familyXplorer.\
Nous allons donc déployer le projet et nous connecter.

Pour déployer le projet, vous devez :

-   cliquer sur le bouton déployer dans la barre d'outil
-   compléter le formulaire qui vous demande d'indiquer l'adresse du
    dynacase control de votre serveur :
    http://adresse-ip-de-la-machine/dynacase-control/
-   cliquer sur déployer

Vous pouvez maintenant vous connecter en utilisant l'url suivante :
http://adresse-ip-de-la-machine/dynacase/qualite-cogip/ et utilisant le
login admin et le mot de passe anakeen.

Insérer ICI une image de familyXplorer

## Conclusion

Vous avez préparé votre environnement pour la suite de cette série de
tutoriaux.\
Il est à noter que vous pouvez télécharger :

-   la machine virtuelle à l'adresse suivante :
    [http://dynacase.org/tuto/VM/tuto1.vmx](http://dynacase.org/tuto/VM/tuto1.vmx)\
-   le projet DynacaseStudio à l'adresse suivante :
    [http://dynacase.org/tuto/projet/tuto1.zip](http://dynacase.org/tuto/projet/tuto1.zip)

