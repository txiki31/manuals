# Starting up the project

## Contexte

Vous êtes employé dans le service informatique de la COGIP, une grande
entreprise d'agroalimentaire. Récemment, la COGIP a acheté la COGEM et
la fusion entre les deux sociétés est en cours.\
Le département qualité de la COGIP récemment fusionné avec celui de la
COGEM a décidé de mettre en place un nouveau système de gestion des
fiches qualité. Pour ce faire, le département souhaite utiliser un outil
pour lui permettre de :

-   sécuriser ses processus d'édition documentaire
-   augmenter sa productivité

Après une étude des progiciels existants aucun ne semblent satisfaisant.
La DSI vous demande donc de réaliser un logiciel pour le département
qualité.

Une première phase d'analyse des besoins, vous a permis de remonter les
éléments suivants :

-   nécessité de gérer un système de relecture et de validation des
    documents au sein du département qualité, qui permet de :
    -   indiquer le document applicable en cours,
    -   gérer un système de fiche de relecture,
    -   apporte une vue synthétique de l'historique de relecture d'un
        document,

-   gestion d'un référentiel de domaine d'application, qui permet de :
    -   gérer une imbrication en domaine, sous domaine,
    -   permet pour un domaine donné de connaître tous les documents
        qualités

-   le système doit être fonctionnel pour dans trois mois et évolutifs
    certains besoins ne sont pas encore matures
-   le système doit être accessible depuis les locaux de la COGIP, ceux
    de la COGEM et depuis internet pour les employés qui télé-travaille.

Fort de ces premiers éléments, vous faites un tour d'horizon des
solutions existantes et plusieurs choix s'offrent à vous, soit :

-   développer en partant de zéro : la solution est tentante l'outil
    sera adapté au besoin et vous maîtrisez la chaine de production mais
    le délais semble trop court,
-   utiliser un framework : là encore la solution semble tentante mais
    la charge de développement semble toujours trop importante,
-   utiliser Dynacase Platform : la solution semble idéal, en effet vos
    pré-requis rentrent tout à fait dans le genre de projet à adresser
    avec cet outil.

Vous décidez donc d'utiliser Dynacase Platform et de mener le projet les
outils de développement associés à la plateforme.

Votre première étape sur le projet est l'analyse du besoin utilisateurs.
Étant donné que vous n'êtes pas encore à l'aise avec les concepts et la
platform de développement, vous avez commandé quelques jours de
consulting à [Anakeen](http://www.anakeen.com "Anakeen").

Le consultant Anakeen organise avec vous les ateliers fonctionnels et
vous fourni une spécification détaillée de l'ensemble des éléments à
intégrer dans le projet. Vous allez utiliser cette spécification tout au
long du projet. Celle-ci est accessible à l'emplacement suivant
[spécification fonctionnelle détaillée](http://adressedelaspec.com).

Nous allons dans ce tutoriel dérouler les différentes étapes de la
réalisation du projet en considérant que l'étape d'analyse du besoin a
été faite avec les membres du département qualité.

\*[DSI] : Direction des Systèmes d'Informations
