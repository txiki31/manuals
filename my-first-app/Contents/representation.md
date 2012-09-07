# Representation control and parametrage

## Introduction

Nous allons voir dans ce tutoriel la notion de représentation. Une
représentation est un fichier de configuration décrivant la mise en
forme d'un document Dynacase, il est obligatoirement associé à une
famille et se base sur l;a structure de la famille pour exister.\
La composition des données de la structure d'une famille et d'une
représentation est appelée une vue.

## Création d'une représentation pour un document qualité à l'état
applicable

Dans le tutoriel précédent, nous avons utilisé un document de
représentation nous allons maintenant le créer. Pour ce faire, vous
allez comme vous en avez l'habitude dans le menu *Dynacase* section
*Documents systèmes* et vous sélectionnez le document de type
*Représentation*.\
Comme toujours un nom logique vous est demandé :
*QCO\_REPRESENTATION\_APPLICABLE* et la famille associée à ce document
là vous faite dérouler le menu et sélectionnez *QCO\_QUALITY*.\
Le studio crée le document de représentation et le place directement
dans le répertoire de la famille et vous ouvre l'IHM suivante.

**insérer capture d'écran**

Une fois dans cette IHM, vous retrouvez une présentation en arbre
similaire à celle de la structure et des propriétés. Vous allez dans
l'onglet *éléments*, nous verrons la partie propriétés par ailleurs.\
L'arbre qui vous est présenté vous permet de définir les options de
représentation des différents attributs de la famille, vous sélectionnez
l'attribut *QCO\_REVIEW* et vous sélectionnez sa propriétés d'affichage
de manière à la passer à *HIDDEN*, ce qui vous permet de le rendre
cacher ainsi que ses sous éléments.\
Vous avez déjà pu dans le tutoriel précédent vous rendre compte de
l'effet qu'à cette représentation sur les documents applicables : elle
cache toutes la partie de discussion lorsqu'un élément est applicable.

Il existe une multitude d'options de représentation mais celle-ci ne
permette que des modifications mineurs des IHM produites, si vous
désirez entièrement redéfinir une IHM il vous faut utiliser la notion de
template ce que nous verrons dans le tutoriel suivant.

## Conclusion

Vous pouvez maintenant déployer votre application. Et constater que
votre représentation fonctionne bien comme dans le tutoriel précédent.
