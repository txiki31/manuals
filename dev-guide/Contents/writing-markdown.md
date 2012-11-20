# documentation

## Introduction

Ce document aborde les points suivants :

* Les règles de rédaction;
* Le glossaire;
* L'organisation du travail et les outils de production;
* La syntaxe markdown;
* Des annexes

## Les règles de rédaction

Pour l'instant les règles identifiées sont :

* Il faut utiliser, autant que possible, le présent de vérité générale, car il exprime qu'un fait est vrai dans sa globalité quelque soit le contexte,
* Il faut éviter d'utiliser les pronoms : je, tu, nous <class ="fixme CBO"> Eric, Yannick ? Expliquer ce choix</a>,

## Le glossaire

Consultation
:   Exprime la modalité permettant uniquement de consulter un document

Modification
:   Exprime la modalité d'édition/modification d'un document

Lignée documentaire
:   C'est l'ensemble des révisions d'un document

module
:   Un module Dynacase contient la définition et l'ensemble des éléments nécessaires au fonctionnement de zéro, une ou plusieurs applications. Elle contient la définition et l'ensemble des éléments nécessaires (cycle de vie, profil, ….) à l'utilisation de zéro, une ou plusieurs familles.

application
:   Une application Dynacase permet de couvrir une fonctionnalité spécifique au système documentaire (exemple: gestion des utilisateurs, administration des contrôle qualité). Une application utilise souvent une ou plusieurs familles de document afin de réaliser leurs fonctions. Une application Dynacase est composée de une à plusieurs actions. Une application possède généralement une interface principale qui permet d'accéder à l'ensemble des actions nécessaires à l'application. Une application est accessible directement par une url directe et est considéré comme autonome vis-à-vis d'autre application.

action
:   Une action Dynacase réalise une fonction d'une application. Cette action reçoit des paramètres, réalise un traitement et retourne le résultat de ce traitement. L'action Dynacase est composée de deux parties : le traitement et la représentation du résultat du traitement. Chacune de ses deux parties est optionnelle mais il en faut au moins une des deux. Le traitement est réalisé à l'aide d'une fonction PHP qui utilise des fonctions de l'API Dynacase. La représentation est réalisée à l'aide d'un template (appelé aussi layout). Ce template permet de réaliser des sorties HTML avec des parties dynamiques.

interface
:   L'interface Dynacase est la représentation d'une action.

template, layout
:   Le template est le modèle de représentation. Ce modèle est généralement du HTML avec des parties dynamiques qui sont construite dans le traitement de l'action. Ce modèle peut aussi être n'importe de n'importe quel type ascii tel que csv ou xml.  Le seul modèle binaire possible est le format openDocumentText. Ce type de modèle permet d'avoir des représentations utilisables pour des besoins d'impressions. Ces modèles sont utilisés pour les représentations des actions et aussi pour les vues de documents.

zone
:   Une zone Dynacase est une action qui ne peut pas être appelée directement depuis l'interface principale. Une zone peut être considéré comme un fragment d'action. Sa représentation est souvent un fragment HTML (le contenu d'une DIV ou d'une TABLE). La zone est réutilisable dans différentes représentations d'actions. Elle permet de réutiliser des fragments d'interfaces dans les différentes interfaces de haut niveau. Une zone peut elle aussi faire référence à d'autres zones. On peut ainsi assembler des interfaces avec des niveaux différents réutilisable.

document
:   Le document Dynacase contient un ensemble structuré d'informations. Il peut être associé à un cycle de vie et porte ses propres paramètres de sécurité d'accès. Un document est toujours associé à une famille de document.

attribut
:   Un attribut de document défini un type syntaxique (texte, nombre, date, …) ainsi que son emplacement dans la structure d'information du document.

famille
:   La famille permet de donner une unité à un ensemble de document de même type sémantique (compte-rendu, facture, client, …). La famille défini la structure de l'information qui sera commune à l'ensemble des documents de cette famille. Cette structure est composée d'attributs du document. Elle défini aussi les règles de sécurités d'accès et l'accès au cycle de vie.

vues
:   Une vue de document désigne un représentation de celui-ci. Cette vue est généralement associé à un template qui lui confère un aspect particulier. Une permet aussi masquer ou de démasquer un ou plusieurs attributs du documents.

cycle de vie
:   Le cycle de vie définit l'ensemble des activités à réaliser, les états et transitions possibles du documents. Un cycle peut être associé à un document; dans ce cas le document est soumis aux contrôles imposé par le cycle. à chaque changement d'état, l'ancien état du document est conservé afin de tracer et de pouvoir voir les informations des états précédents.

profil
:   Le profil d'un document décrit une matrice de droits. Les droits les plus usuel sont 'voir','modifier', 'supprimer'. Pour chacun des ces droits, le profil défini quels groupes d'utilisateurs ou quels utilisateurs en particulier ont cette habilitation. Les droits des groupes sont propagés automatiquement sur les membres de groupes et des éventuels sous-groupes.Le même profil peut être partagé par plusieurs documents. Cela permet de modifier plus facilement les accès à un ensembles de document de même niveau de sécurité. Généralement, un même profil est partagé par les documents d'une même famille.

## La syntaxe markdown

Nous allons maintenant voir différents points basiques de la syntaxe
pandoc-markdown.

### Paragraphe

Un paragraphe est une ou plusieurs lignes de textes suivi de un ou plusieurs saut de ligne. Si vous avez besoin d'un saut de ligne au milieu d'un paragraphe deux syntaxes sont possibles : deux espaces ou \\ suivi d'un saut de ligne.

### Titre et sous titre

Les titres sont présentés de la manière suivante :

    # Titre 1
    ## Titre 2
    ### Titre 3

### Emphase

Il est possible de mettre en évidence du texte de manière différentes.

L'emphase en utilisant la syntaxe suivante :

    *Ceci mérite votre attention*

L'emphase importante en utilisant la syntaxe suivante :

    **Ceci est important**

NB : l'emphase simple est souvent rendu avec un texte en *italique*,
l'emphase importante avec un texte en **gras**.

### Rayer

Il est possible de rayer un texte avec la syntaxe suivante :

    ~~je suis rayé~~

### Caractère d'échappement

Le caractère d'échappement est le \\. Les caractères pouvant être
échappés sont les suivants :

    \`*_{}[]()>#+-.!

### Bloc de citation

Un bloc de citation ce défini de la manière suivante :

    > Au commencement, Dieu créa les cieux et la terre. 
    > La terre était informe et vide: il y avait des ténèbres à la surface de l'abîme, et l'esprit de Dieu se mouvait au-dessus des eaux. 
    > Dieu dit: Que la lumière soit! Et la lumière fut. 
    > Dieu vit que la lumière était bonne; et Dieu sépara la lumière d'avec les ténèbres. 
    > Dieu appela la lumière jour, et il appela les ténèbres nuit. Ainsi, il y eut un soir, et il y eut un matin: ce fut le premier jour. 
    > Dieu dit: Qu'il y ait une étendue entre les eaux, et qu'elle sépare les eaux d'avec les eaux. 

### Bloc de code

Un bloc de code peut-être défini de deux manières :

-   soit en ajoutant une tabulation devant chaque ligne de code
-   soit de la manière suivante (une ligne de 3 ou plus \~) :

<!-- end of list -->

    ~~~
    if (a > 3) {
        moveShip(5 * gravity, DOWN);
    }
    ~~~

Vous pouvez aussi ajouter le langage (ce qui active la coloration
syntaxique):

    ~~~~~~~~~~~~~~~~{.php }
    if (a > 3) {
      moveShip(5 * gravity, DOWN);
    }
    ~~~~~~~~~~~~~~~~

et si votre code contient des tildes, vous pouvez utiliser la syntaxe
suivante :

    ~~~~~~~~~~~~~~~~
    ~~~~~~~~~~
    if (a > 3) {
      moveShip(5 * gravity, DOWN);
    }
    ~~~~~~~~~~
    ~~~~~~~~~~~~~~~~

### Liste à puce

Les liste à puce peuvent être définies de plusieurs manières :

-   liste non ordonnée (on peut aussi utiliser (+, -)) :

    * ceci est le premier élément
    * ceci est le second élément

-   liste non ordonnée avec une sous liste :

    * fruits
        + apples
            - macintosh
            - red delicious
        + pears
        + peaches
    * vegetables
        + brocolli
        + chard

Il faut ajouter autant de tabulation que de sous niveau de liste qu'on
souhaite obtenir.

-   liste ordonnée :

    1.  one
    2.  two
    3.  three

NB : pandoc ne prête attention qu'au premier élément de la liste et si
on écrit

    1.  one
    *  two
    +  three

On obtient le même résultat que dans l'exemple précédent.

NB : Pour terminer une liste et pouvoir mettre un morceau de code
présenté par une tabulation vous devez utiliser la syntaxe suivante :

    -   item one
    -   item two

        <!-- end of list -->

        { my code block }

### Tableau

Il existe deux 3 de tableau.

1.  le tableau simple une seule ligne: ce type ne permet pas les cases
    fusionnées et l'écriture sur plusieurs lignes des cases mais est
    plus simple à rédiger

<!-- end of list -->

      Right     Left     Center     Default
    -------     ------ ----------   -------
         12     12        12            12
        123     123       123          123
          1     1          1             1

    Table:  Demonstration of simple table syntax.

Vous pouvez noter que l'alignement des élément au sein du tableau est
indiqué par l'entête du tableau avec les règles suivantes :

-   si le texte d'en tête est collé au dernier tiret de la ligne de
    définition des colonnes : le texte est aligné à droite
-   si le texte d'en tête est collé au premier tiret de la ligne de
    définition des colonnes : le texte est aligné à gauche
-   si le texte d'en tête est collé au à aucun des tirets de la ligne de
    définition des colonnes : le texte est aligné à centré
-   si le texte d'en tête est collé au au premier et au dernier tiret de
    la ligne de définition des colonnes : le texte est aligné avec
    l'alignement par défaut (le plus souvent à droite)

Un titre peut être fourni de manière optionnelle. Pour ce faire, il faut
commencer le paragraphe suivant le tableau soit par :

-   Table:
-   :

<!-- end of list -->

2.  le tableau simple en plusieurs lignes: ce type ne permet pas les
    cases fusionnées mais permet l'écriture sur plusieurs lignes des
    cases

<!-- end of list -->

~~~~
-------------------------------------------------------------
     Centered   Default           Right Left
      Header    Aligned         Aligned Aligned
    ----------- ------- --------------- -------------------------
       First    row                12.0 Example of a row that
                                        spans multiple lines.
    
      Second    row                 5.0 Here's another one. Note
                                        the blank line between
                                        rows.
    -------------------------------------------------------------
Table: Here's the caption. It, too, may span
multiple lines.
~~~~

Le principe est similaire au précédent mais avec l'ajout de deux lignes
de *-* pour indiquer le début et la fin du tableau.

<!-- end of list -->

3.  le tableau: ce type ne permet pas les cases fusionnées mais est plus
    difficile à réaliser

<!-- end of list -->

~~~~
+---------------+---------------+--------------------+
| Fruit         | Price         | Advantages         |
+===============+===============+====================+
| Bananas       | $1.34         | - built-in wrapper |
|               |               | - bright color     |
+---------------+---------------+--------------------+
| Oranges       | $2.10         | - cures scurvy     |
|               |               | - tasty            |
+---------------+---------------+--------------------+
~~~~

### Les hyperliens

Pour ajouter un hyperlien, vous devez utiliser une des syntaxes
suivantes :

-   les liens automatiques :

<!-- end of list -->

    <http://google.com>
    <sam@green.eggs.ham>

-   les liens inline :

<!-- end of list -->

    This is an [inline link](/url), and here's [one with a title](http://fsf.org "click here for a good time!").

### Les images

Pour ajouter une image.

    ![This is the caption](/url/of/image.png)

Ce paragraphe n'est qu'un résumé des principaux éléments de la syntaxe
pandoc, vous pouvez retrouver l'ensemble plus détaillé à l'adresse
suivante :

<http://johnmacfarlane.net/pandoc/README.html>

## Annexes

### Le choix de markdown

Lors des choix pour la réalisation de la documentation, nous voulions un moyen de produire de la documentation qui combine les différents points suivants :

-   La rédaction est facilitée de rédaction par la syntaxe;
-   La mise en page est simplifiée;
-   Le format permet de réaliser la documentation en composant un ensemble d'éléments unitaires facilement identifiables;
-   possibilité d'établir un diff entre deux versions d'un élément de documentation;
-   et que le document soit lisible tel quel sans traitement particulier par quelqu'un ne connaissant pas la syntaxe.

Nous avons étudié les différents moyen de production à notre disposition et retenu markdown car il est :

> Markdown est un langage de balisage léger créé par John Gruber et
> Aaron Swartz. Le but de la syntaxe Markdown est d'offrir une syntaxe
> facile à lire et à écrire. C'est-à-dire qu'un document formaté selon
> Markdown devrait pouvoir être publié comme tel, en texte, sans donner
> l’impression qu’il a été marqué par des balises ou des instructions de
> formatage. Bien que la syntaxe Markdown ait été influencée par
> plusieurs filtres de conversion de texte vers HTML existants —
> incluant Setext, atx, Textile, reStructuredText, Grutatext et EtText —
> la source d’inspiration principale de la syntaxe Markdown est le
> format du courrier électronique en mode texte.

dixit wikipedia.

