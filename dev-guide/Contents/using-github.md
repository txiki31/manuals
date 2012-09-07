# Gestion de configuration des sources

Les développements de Dynacase utilisent git et [github](https://github.com/Anakeen%20github%20pour%20anakeen) pour la gestion de configuration des sources.

## Présentation

Github est, à tout points de vue, un hébergeur de repository git
traditionnel. Il est donc possible de:

-   cloner un repository git
-   puller depuis un repository git
-   pusher vers un repository git
-   etc.

Sa seule différence est qu'en plus de l'hébergement des repos, github
offre une interface web. Cette interface permet de :

-   gérer les autorisations
    -   chaque utilisateur peut être placé dans plusieurs groupes
        (teams)
    -   chaque team est liée à un ensemble de repos avec un de ces
        droits:
        -   pull only
        -   push & pull
        -   push, pull & administrative

-   gérer un workflow de contributions: l'interface simplifie:
    -   le fork
    -   les demandes de pull
    -   la consultation (et la récupération) des commits du réseau et
        des diffs

## Quelques notions

### Notions de github

#### Le repositoy

Le repository est un repository git ordinaire. Il peut soit être

public
  ~ il est alors visible (et clonable) par toute personne allant sur
    github
privé
  ~ il n'est alors visible (et éventuellement clonable) que par les
    membres des teams ayant suffisamment de privilèges

#### le fork

Lorsqu'un utilisateur a la possibilité de voir un repository, il a
directement la possibilité de le forker, via un simple bouton sur
l'interface. Cette action va créer dans son compte un clone du
repository initial.

Cette action est à la base de tout workflow mis en place sur github: une
fois un repository forké, l'utilisateur peut travailler en toute liberté
sur sa copie. Il a ensuite, toujours via un simple bouton sur
l'interface, la possibilité de solliciter les mainteneurs du repository
d'origine pour intégrer ses changements: c'est la [demande de
pull](#demande-de-pull).

#### Le réseau

C'est l'ensemble de tous les repos obtenus par des forks successifs.
C'est à dire que chaque fois qu'un utilisateur forke un repository d'un
reseau, son fork devient membre du réseau.

Si le repository à l'origine du réseau est privé, alors tout le réseau
est privé.

#### La demande de pull

Lorsqu'un utilisateur veut voir ses changements de code intégrés au
repository de départ, il fait une demande de pull. Il va alors préciser
quelle est la branche qu'il propose, et vers quelle branche il propose
ses corrections.

Cette demande de pull va générer une notification chez l'ensemble des
membres ayant le droit de pusher sur le repository concerné. Ils
pourront alors, via l'interface:

1.  Faire une revue:
    -   voir le résumé de ces changements (commits et fichiers impactés)
    -   voir le diff complet
    -   commenter la demande de pull
        -   de façon gobale,
        -   ou directement sur certaines lignes des fichiers impactés

2.  accepter ou refuser les changements

Note: la partie revue peut être itérative: les commentaires permettent
de réelles discussions avec l'ensemble des utilisateurs ayant le droit
de voir le réseau.

### Notions de redmine

#### l'issue

L'issue dans redmine est une entrée du bugtracker. Elle peut être une
anomalie, une évolution ou une amélioration.

#### La feature

Dans le cadre de nos développements, un nouveau tracker sera créé. Ce
tracker sera privé, et permettra d'enregistrer les *features*. Ces
*features* seront des regroupements de 1 à n issues. Les développements
seront faits dans le cadre d'une feature.

## Organisation macroscopique des sources

Il est proposé de créer le découpage suivant:

-   Le repository **Anakeen/dynacase-project**. C'est un repository
    vide, qui contient les submodules suivants:
    -   **Anakeen/dynacase-platform**.
    -   **Anaken/official-modules** C'est un repository vide qui
        contient les submodules suivants :
        -   **Anakeen/dynacase-webdesk**,
        -   **Anakeen/dynacase-dynacase-nu**,
        -   etc.

    -   **Anakeen/third-party-modules** C'est un repository vide qui
        contient les submodules suivants :
        -   **Anakeen/dynacase-extjs**,
        -   **Anakeen/dynacase-fckeditor**,
        -   etc.

    -   **Anakeen/contrib-modules** C'est un repository vide qui
        contient les submodules des contributions telles que celles de
        tony, à condition que ces dernières soient sur github.

## Le workflow proposé pour débuter

### Point de départ

Partons de la situation suivante:

-   [L'*organization*
    Anakeen](https://github.com/organizations/Anakeen/) a un repository
    **Anakeen/dynacase-platform3**.\
     Ce repository est public (Ce qui veut dire que, comme dans le
    modèle actuel, tout le monde peut voir les sources et les cloner,
    travailler dessus dans son coin, et éventuellement proposer des
    corrections de son cru).\
     Il est composé comme suit[^1]:
    -   branches:
        -   master
        -   3.0

    -   tags
        -   <3.0\> --\> pointe vers la dernière version stable 3.0.\*
        -   <3.0.18\>,
        -   <3.0.17\>
        -   ...

-   la *team dynacase 3 - admin* a les droits *push, pull &
    administrative* sur ce repository. Elle est composée de
    -   Eric,
    -   Marc

-   la *team dynacase 3 - workers*[^2] a les droits *pull only* sur ce
    repository. Elle est composée de
    -   Eric,
    -   Marc,
    -   Jerome,
    -   Arnaud,
    -   Clément,
    -   Charles,
    -   Matthieu

Chacun des membres de cette team a un repository, qui est le fork du
repository **Anakeen/dynacase-platform3**

                    ...-o           master
                       / 
                o-...-o             3.0
                |     |
        <3.0.17>      |
               <3.0.18>
                  <3.0>

### Développement

#### Au travail...

Des anomalies et des évolutions ont été qualifiées pour la *prochaine
version*. On crée donc sur le repository **Anakeen/dynacase-platform3**
une branche **next-release-3.0**, à partir de 3.0

                    ...-o           master
                       / 
                o-...-o             3.0
                |     |\
        <3.0.17>      | \
               <3.0.18>  \
                  <3.0>   \
                           o        next-release-3.0

Chacune des issues (ou groupe d'issues) qualifiées pour la *prochaine
version* donnera lieu à la création d'une branche sur le repository du
développeur responsable. Ces branches seront nommées `F-<N° de feature>`
pour un groupe d'issues (une feature).

L'objectif de ces branches est de permettre de garder leur développement
pur. C'est à dire que, une fois les développements correspondant à une
feature terminée, il existera une branche permettant de récupérer
exactement les développements correspondant à ce développement afin de
pouvoir, si nécessaire, les backporter, par exemple. L'objectif des
responsables de F-\#\#\#\# est donc de faire en sorte que les branches
ainsi nommées soient *propres*.

#### Recommandations

Dans le but de respecter cette consigne, il est demandé de travailler
sur d'autres branches, et de faire le nécessaire (rebase, merge,
cherry-picking, etc...) pour que, une fois le développement terminé,
l'historique des branches F-\#\#\#\# soit lisible et compréhensible.

Dans le respect de ces règles, les développeurs sont invités à
travailler *comme il le souhaitent*.\
Ils ont leur repository local, sur leur machine, et leur repository
github, dans le cloud.

#### État des lieux

En prévision de la prochaine release, Éric souhaite voir comment ce qui
est fait pour la F-1234 pourra être intégré. Il se connecte donc à son
compte, sélectionne depuis son dashboard le contexte *anakeen*, puis le
repository du développeur responsable de ce développement. Il se rend
ici sur la liste des branches, d'où il peut simplement faire un diff
entre la branche de son choix[^3], et toute autre branche, que cette
branche soit sur le repository du responsable, mais également avec toute
autre branche du réseau (voir [le tuto sur la vue de comparaison cross
repos](#De-tres-bonnes-pages-d-explications-sur-le-blog-github)).

Évidemment, Éric ne peut pas voir ce que le développeur n'a jamais
pushé...

#### Du coté du développeur (chez F-1234)

Du coté du développeur, le repository ressemble à ceci:

                    ...-o           master
                       / 
                o-...-o             3.0
                |     |\
        <3.0.17>      | \
               <3.0.18>  \
                  <3.0>   \
                           \
                            o       next-release-3.0
                             \
                              o     F-1234

Suivant les [recommandations](#Recommandations), le développeur
travaille sur une autre branche:

                    ...-o           master
                       / 
                o-...-o             3.0
                |     |\
        <3.0.17>      | \
               <3.0.18>  \
                  <3.0>   \
                           \
                            o       next-release-3.0
                             \
                              o     F-1234
                               \
                                o---o-...-o  F-1234-working

Après un certain temps de travail, il estime avoir corrigé son anomalie
(évidemment, il vérifie avec les tests unitaires, et autres tests
automatis[é|able]s qu'il n'a pas introduit de régression. Une fois ces
vérifications effectuées, le développeur veut réintégrer son travail à
**Anakeen/dynacase-platform3**. Cette intégration devra se faire sur la
branche **next-release-3.0**

Afin de s'assurer que son travail est intégrable, le développeur doit
mettre à jour sa branche **next-release-3.0** vis à vis du repository
**Anakeen/dynacase-platform3**, ce qui lui donne par exemple:

                    ...-o                     master
                       / 
                o-...-o                       3.0
                |     |\
        <3.0.17>      | \
               <3.0.18>  \     o              F-1234
                  <3.0>   \   /
                           \ /
                            o---o-...-o       next-release-3.0 (avec d'autres issues déjà intégrées)
                            |\
                   <3.0-beta> \
                               o---o-...-o    F-1234-working

Étant donné que du travail a été fait sur **next-release-3.0** pendant
ce temps, son travail a de fortes chances de ne pas pouvoir être intégré
directement. Il a des ajustements à faire.\
Comme cela a déjà été dit, le but étant toujours de garder F-1234
**propre**

##### Option 1: le rebase

Parmi les nombreuses possibilités qui lui sont offertes, il choisit de
rebaser sa branche **F-1234-working** sur **next-release-3.0**. Pour
plus de propreté, il en profite pour réagencer ses commits afin de créer
la F-1234 propre. Ce qui donne :

                    ...-o                            master
                       / 
                o-...-o                              3.0
                |     |\
        <3.0.17>      | \
               <3.0.18>  \
                  <3.0>   \             o---o-...-o  F-1234
                           \           /
                            o---o-...-o              next-release-3.0 (avec d'autres issues déjà intégrées)

Maintenant que sa branche est au-dessus de next-release-3.0, il peut
demander l'intégration.\
Pour cela, Il se connecte ensuite à son interface github, et fait une
demande de pull pour intégrer sa branche **F-1234** à la branche
**next-release-3.0-integration** de **Anakeen/dynacase-platform3**.

##### Option 2: le merge

Cette fois-ci, il choisit de merger ses changements avec les changements
déjà effectués sur **next-release-3.0**. Il doit d'abord mettre sa
branche **F-1234** au propre, puis effectuer le merge dans une branche
temporaire. Ce qui donne:

                    ...-o           master
                       / 
                o-...-o             3.0
                |     |\
        <3.0.17>      | \
               <3.0.18>  \
                  <3.0>   \
                           \
                            o---o-...-o----   next-release-3.0 (avec d'autres issues déjà intégrées)
                             \             \
                              \             o F-1234-integration
                               \           /
                                o---o-...-o  F-1234

Maintenant que sa branche est au-dessus de next-release-3.0, il peut
demander l'intégration.\
Pour cela, Il se connecte ensuite à son interface github, et fait une
demande de pull pour intégrer sa branche **F-1234-integration** à la
branche **next-release-3.0-integration** de
**Anakeen/dynacase-platform3**.

##### Option 3: l'intégration avec d'autres issues

Ici, afin de diminuer le travail du release manager, il a été demandé
que les issues soient regroupées pour que l'intégration finale soit plus
rapide.\
Ainsi, il a été demandé au développeur de F-1234 de l'intégrer à
F-feature. Dans ce cas, le développeur de F-feature devient une sorte de
*sergent*, un release manager à l'échelle de F-feature.

Le développeur de F-1234 doit lui soumettre sa correction, mais cette
fois-ci de sorte qu'elle soit intégrable avec F-feature. pour dela, il
peut soit rebaser, soit merger, soit utiliser la solution de son choix.

##### Réception de la demande de pull

Le(s) destinataire(s) de la demande de pull reçoit une notification (par
mail, s'il l'a activé, ainsi que via l'interface). Il se connecte à son
compte github, et dans le contexte anakeen, sélectionne *Pull requests*.
Il trouvera ici les différentes demandes du pull.

Il peut alors commenter, voire demander à d'autres développeurs de faire
une relecture de code[^4]. Cette relecture de code se fait dans
l'interface, sans avoir besoin de cloner / puller / fetcher quoi que ce
soit.\
Une fois satisfait (éventuellement après plusieurs refus), le
destinataire merge la demande.

En même temps qu'il merge la demande, le release manager rapatrie
également la branche **F-1234** de **<dev\>/dynacase-platform3** dans la
branche **F-1234** de **Anakeen/dynacase-platform3**. Cela permet
d'envisager:

-   que d'autres développeurs puissent faire les éventuelles corrections
    liées à l'intégration si nécessaire,
-   que la feature fasse référence à l'url de cette branche pour la
    liste des modifications y étant liées.

##### travail à plusieurs sur une issue / un groupe d'issues

Dans le cas où plusieurs personnes doivent travailler ensemble sur une
feature ou une issue, le fonctionnement est le même que dans le cas 3:
un sergent est désigné, responsable du groupe de travail, et il gère une
organisation en dessous de lui, jusqu'au moment où il fait une demande
de pull au release manager.

### Publication d'une nouvelle release

À un moment donné, on décide que plus aucune fonctionnalité ne sera
intégrée à la prochaine release, et on passe à l'intégration de cette
prochaine release.

On crée alors la branche d'intégration de cette release. Étant donné
qu'on sait maintenant exactement ce qu'il y aura dedans, on peut nommer
cette version. 2 cas: soit une nouvelle version, soit une version de
maintenance

#### Cas 1: version de maintenance (3.0.19)

On crée une branche d'intégration: **integration-3.0.19** sur
**Anakeen/dynacase-platform3**. À partir de ce moment, seules les
corrections sont encore acceptables (et devront être pushées sur la
nouvelle branche); tandis que la branche **next-release-3.0** recevra
les développements de la version ultérieure. On obtient:

                o-...-o                   3.0
                |     |\
        <3.0.17>      | \
               <3.0.18>  \
                  <3.0>   \
                           o-...-o        next-release-3.0
                                  \
                                   o      integration-3.0.19
                                   |
                          <3.0-beta>

Au cours des tests d'intégration, **Anakeen/integration-3.0.19** reçoit
les corrections des développeurs ayant pushé dessus selon le même schéma
que précédemment.\
Pendant ce temps, des développements sont en cours pour la version
ultérieure.

Après les tests, et une fois la version réputés stable, on est dans
l'état suivant:

                o-...-o             3.0
                |     |\
        <3.0.17>      | \
               <3.0.18>  \
                  <3.0>   \
                           o-...-o-...-o        next-release-3.0 (càd après 3.0.19)
                                  \
                                   o-...-o      integration-3.0.19 (prête à être publiée)
                                         |
                                <3.0-beta>

à ce moment, on publie:

-   merge de **integration-3.0.19** dans **3.0**, puis dans **master**
    (je finis par me demander à quoi sert master: il ressemble à un
    **current-version**)
-   merge de **integration-3.0.19** dans **next-release-3.0** (pour
    récupérer dans la prochaine version les développements finaux de
    cette version).
-   suppression de **intégration 3.0.19**
-   positionnement des tags

On obtient alors (master a été ignoré pour plus de lisibilité):

                o-...-o---o-...-o---o-...-o                 3.0
                |     |\                  |\
        <3.0.17>      | \          <3.0.19> \
               <3.0.18>  \            <3.0>  \
                          \                   o-...-o       next-release-3.0 (càd après 3.0.19)
                           \
                            o-...-o                         F-feature
                             \
                              o-...-o                       F-1234

#### cas 2: nouvelle version (3.1.0)

Dans ce cas, la démarche est similaire, mais mène au graphe suivant:

                    ...-o-------------------o                 master
                       /                   /
                o-...-o                   /                   3.0
                |     |\                 /
        <3.0.17>      | \               /
               <3.0.18>  \             /
                          \           / 
                           \ <3.1.0> /
                            \      |/
                             o-...-o                          3.1       
                              \     \
                               \     o                        next-release-3.0
                                \
                                 o-...-o                      F-feature
                                  \
                                   o-...-o                    F-1234

On peut y voir qu'une bifurcation entre 3.0 et 3.1 est née. Cela
permettra, par la suite d'arriver à ce graphe:

Dans ce cas, la démarche est similaire, mais mène au graphe suivant
(master, ainsi que les branches I-\* et F-\* a été omis pour plus de
lisibilité):

                              o                               next-release-3.0
                             /              
                o-...-o-o...o                                 3.0
                |     |\    |             
        <3.0.17>      | \   <3.0.19>     
               <3.0.18>  \  <3.0>       
                          \             
                           \ <3.1.0>     <3.1.1>
                            \      |     |
                             o-...-o-...-o                    3.1       
                                          \
                                           o                  next-release-3.1

## Ressources

### Remarques sur la *fork queue* et le *cherry-picking*

La fork queue est décrite
[ici](https://github.com/blog/270-the-fork-queue).

Pour information, la *fork queue* est réellement une interface au
[cherry-picking](http://progit.org/book/ch5-3.html#rebasing_and_cherry_picking_workflows),
avec les avantages et inconvénients que cela peut apporter. Je vous
invite, pour les plus courageux, à lire [ce très bon article sur la fork
queue](http://rjbs.manxome.org/rubric/entry/1755), et surtout ses
commentaires avant de faire un usage intensif de cette fonctionnalité
trop attrayante. Pour le résumer, le cherry-picking, même s'il ne pose
pas de problème technique pour les merges (car, contre toute attente,
git s'en sort très bien avec les conflits liés au cherry-pickig, et qui
en fait n'en sont pas), crée des entrées dupliquées dans l'historique.
Il est, la plupart du temps préférable d'utiliser
`git merge <commit sha-1>` à la place (pour aller plus loin, vous pouvez
lire également [cet article sur les alternatives au
cherry-picking](http://gitready.com/intermediate/2009/03/04/pick-out-individual-commits.html)

### Remarques et discussions sur les repository / branches de travail et
le rebase

Une suggestion que je ferais est la suivante:

-   les branches suivantes doivent **absolument rester stables**:
    -   sur **Anakeen/dynacase-platform3**
        -   Toutes les branches

-   Les branches suivantes peuvent être rebasées à tout moment
    -   sur **developpeur/dynacase3**
        -   Toutes les branches

-   on demande aux développeurs de systématiquement faire des
    `pull --rebase` (cf:
    http://gitready.com/advanced/2009/02/11/pull-with-rebase.html) (cela
    peut être ajouté a .git pour éviter les oublis)
-   ca permet également le cherry-picking sans polluer l'historique.

### De très bonnes pages d'explications sur le blog github
{\#De-tres-bonnes-pages-d-explications-sur-le-blog-github}

-   [Leur wiki d'aide, à parcourir](http://help.github.com/)
-   [Un aperçu des branches, et de leur positionnement
    relatif](https://github.com/blog/611-branch-lists)
-   [vue de
    comparaison](https://github.com/blog/612-introducing-github-compare-view)
-   [vue de comparaison cross
    repos](https://github.com/blog/683-cross-repository-compare-view)
-   [comment filtrer dans gmail les notifications de
    github](https://github.com/blog/695-easily-filter-notifications-by-repository)

### Quelques outils pouvant être utiles

-   Des outils pour simplifier la ligne de commande quand le repository
    est github
    -   https://github.com/defunkt/github-gem\#readme
    -   https://github.com/defunkt/hub\#readme

-   un plugin redmine pour pas devoir tout se cloner ~~à la main~~avec
    cron
    -   http://mentalized.net/journal/2009/08/03/redmine\_plugin\_github\_hook/

[^1]: Ceci est un état statique virtuel, et le repository n'aura en
    réalité jamais été dans cet état précis.

[^2]: Oui, je sais, il va falloir trouver un meilleur nom...

[^3]: Il sera probablement nécessaire de définir des règles de nommage
    pour les branches.

[^4]: Note: Chaque développeur a également eu la possibilité de demander
    une relecture de code sur n'importe lequel de ses commits
