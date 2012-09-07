# Deployment

## Introduction

Nous allons dans ce tutoriel évoquer la problématique du déploiement et
de la construction de paquet Dynacase.

Nous verrons les différents actions de déploiement possible :

-   build : qui permet de construire le paquet
-   build & deploy : qui permet de construire et déployer le paquet sur
    une cible définie.

Nous aborderons les deux scénarios possibles lors d'un déploiement
l'upgrade et l'install.

Et in fine, nous étudierons les mécanisme de pre et post upgrade.

## Mise en pratique

Nous allons tout d'abord construire un paquet Dynacase. Pour ce faire,
vous devez cliquer sur le bouton *Build Dynacase*, l'interface suivante
s'ouvre :

**insérer ici une capture d'écran**

Vous sélectionnez le nom et l'emplacement ou vous voulez construire le
paquet et celui-ci est construit.

Nous allons maintenant nous intéresser au contenu de ce paquet pour ce
faire, vous devez le dezipper, sélectionnez le fichier produit
précédemment et ouvrez le avec votre éditeur de fichier zip préféré.

Vous pouvez voir que le contenu du paquet est similaire à celui de votre
projet à l'exception des fichiers propres à Eclipse. En effet, le paquet
est construit en zippant le projet Dynacase à l'exception des fichiers
ou des pattern de fichiers définis dans le exclude.xml. Ci-dessous vous
pouvez voir le exclude.xml par défaut :

**insérer ici le contenu du exclude par défaut**

Nous allons maintenant voir le contenu du fichier builder.xml. Ce
fichier permet d'indiquer les actions à effectuer lors d'une
installation ou d'une mise à jour. Les actions qui peuvent être déclarés
sont de deux types :

-   des actions tel que définies sur votre application ou dans la
    plateforme sur laquelle vous installez
-   des importations de documents, familles, etc...

Il est à noter que le mode de fonctionnement entre l'installation et la
mise à jour est *différent* sur le point des importations, en effet lors
de l'installation installe tous les éléments définis à l'exception de
ceux exclus et lors de la mise à jour la mise à jour upgrade uniquement
les éléments déclaré comme devant être mis à jour.

Nous allons maintenant voir un exemple de fichier de builder.

**insérer ici le contenu du builder par défaut**

Lors d'une mise à jour, il vous suffit donc de définir dans le fichier
les documents que vous souhaitez mettre à jour. Chaque document
peut-être déclaré soit avec son nom de fichier, soit avec son nom
logique.

Nous allons maintenant voir les pre et post upgrade. Dans votre
application, vous disposez d'un répertoire migration qui vous permet de
définir des scripts qui seront exécuté avant et après une migration.
Pour définir un nouveau script, il vous suffit de sélectionner le menu
*Dynacase* *Script* *Pre migration*, là l'interface suivante vous est
présentée :

**insérer ici une capture d'écran**

et vous demande avant quelle version de l'application le script doit
être lancé et son nom logique. Une fois ce questionnaire votre fichier
est crée et hérite automatiquement de classe preScript.

**insérer ici le d'un script**

## Conclusion

Ce tutoriel a abordé les divers points de mise à jour qui permette de
faire mise à jour et des déploiements. Si vous désirez en savoir plus
sur la gestion des paquets et dynacase control vous pouvez consulter les
tutoriaux suivants....
