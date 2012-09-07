# Workflow : Parametrage

## Introduction

Nous allons maintenant paramétrer le cycle de vie que nous avons défini
précédemment. Nous allons introduire les éléments suivants :

-   le profil de cycle de vie : ce type d'élément permet de paramétrer
    les droits sur les passages de transition et donc d'indiquer qui
    peut passer d'une activité à une autre,
-   les profils de document associés au cycle : ce type d'élément permet
    de définir qui lors d'une activité peut voir/éditer/.. un document,
-   les représentations associées au cycle : ce type d'élément permet de
    définir des vues particulières associés aux états ou aux
    transitions,
-   les mails : nous allons voir cet élément qui permet d'envoyer un
    mail à différents types d'utilisateurs

## Mise en place

### Profil de cycle de vie

Nous allons maintenant paramétrer le cycle de vie. Pour ce faire, vous
devez éditer le cycle de vie et sélectionner l'onglet *droits*. Cet
onglet vous permet d'associer le droit de passage d'une transition a un
des rôles définis dans votre application.\
Pour ce faire vous utilisez l'interface suivante :\
**insérer ici une capture d'écran**

Cette interface vous présente un tableau avec en colonne les différentes
transitions possibles. Vous pouvez ajouter une ligne par rôle utilisé et
sélectionner quels droits s'appliquent à ce rôle en utilisant les case à
cocher, de la même manière vous pouvez ajouter des acteurs et définir
quels droits sont associés à ceux-ci.\
La définition de ce paramétrage étant assez simple, nous avons complété
pour vous la majorité des droits définis dans la spécification de notre
application.\
Il ne vous reste plus qu'à définir les droits associé au *validateur*.\
Vous devez donc ajouter une ligne, sélectionnez le *validateur* et
ajoutez les droits suivants :

-   *retour au brouillon*
-   *passage en approbation*

Vous pouvez consulter le tableau des droits et vérifier qu'il est bien
en concordance avec les droits.

### Profil de document

Nous allons créer le profil associé à l'activité de rédaction ce profil
n'autorise la modification et la visualisation du document que par le
rédacteur du document.\
Pour ce faire, veuillez dans le menu *dynacase* sous menu *Documents
internes* sélectionnez l'option *Profil de document*.\
Il vous est demandé le nom logique du profil
*QCO\_PROFIL\_QUALITY\_REDACTION* et la famille auquel associer ce
profil *QCO\_QUALITY*.\
Le document est crée et vous retrouvez une interface similaire à celle
vue précédemment.\
**insérer ici une capture d'écran**

Vous allez ajouter une ligne, sélectionnez le *rédacteur* et ajoutez les
droits suivants :

-   *voir*
-   *éditer*

Votre profil est créé et vous devez l'associer au cycle de vie. Pour ce
faire, ouvrez le document de cycle de vie et sélectionnez l'onglet
profil. Un tableau présentant l'ensemble des activités/actions
disponible est présenté.\
**insérer ici une capture d'écran**

Veuillez ajouter à la ligne *rédaction* le profil
*QCO\_PROFIL\_QUALITY\_REDACTION*.

### Représentation asssociée à l'état

Dans l'état applicable le document ne doit présenter que la partie
directement liée au document qualité et pas la partie liée aux
discussions. Pour ce faire, vous allez associer la représentation que
nous vous avons crée pour vous à l'état *applicable*.\
Vous devez donc ouvrir le cycle de vie et l'onglet *état*, là se
présente à vous l'interface suivante :\
**insérer ici une capture d'écran**

Vous sélectionnez l'état *applicable* et ajoutez dans la case
représentation la référence suivante :
*QCO\_REPRESENTATION\_APPLICABLE*.

Nous avons défini pour vous le document représentation, si vous désirez
en savoir plus sur ceux-ci, veuillez consulter le tutoriel
correspondant.

### Envoi de mail associé à une transition

Il nous reste un dernier type de document à étudier le *modèle de mail*.
En effet notre spécification indique que l'on doit envoyer un mail lors
du passage dans la transition *Passage en approbation*.\
Vous devez créer un document mail, pour cela comme toujours vous passez
dans le menu *dynacase*, sous section *document système* et vous
sélectionnez le mail.\
Un nom logique vous est demander nous allons utiliser :
*QCO\_MAIL\_QUAL\_T\_TO\_APPROBATION*\
Vous vous trouvez maintenant devant une IHM de gestion de modèle de mail
semblable à celle présentée ci-dessous :\
**insérer ici une capture d'écran**

Vous ajoutez les éléments suivants :

-   destinataire : vous sélectionnez le *validateur*
-   sujet : *Le document Workflow parametrage\_rev0 vous a été assigné*
-   contenu du mail : *Bonjour, le document Workflow parametrage\_rev0
    vous a été assigné, veuillez le consulter à l'URL suivante [URL]*

## Conclusion

Vous pouvez maintenant déployer le cycle de vie et ouvrir un document de
manuel de qualité, vous verrez un menu de changement de cycle de vie et
les différents mails envoyés sont accessibles directement sur le
roundcube de la VM situé sur http://ip-de-la-machine/roundcube.
