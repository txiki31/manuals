# Workflow : The beginning

## Introduction

Nous allons maintenant voir une notion importante de Dynacase : les
workflows. Ceux-ci permettent de définir un cycle de vie dans lequel des
documents peuvent évoluer.\
Nous allons voir dans ce document les différents éléments qui composent
un cycle de vie et comment en définir la structure et l'intégrer dans la
plateforme.

Les différents objets/notions composants un cycle de vie sont les
suivants :

-   Transitions : une transition est un objet permettant de définir le
    passage d'une activité à une autre du cycle de vie,
-   Activité : une activité décrit l'action qui se déroule sur le
    document pendant l'activité,
-   État : un état peut-être le résultat d'une activité, c'est à dire
    que lorsqu'une activité est terminée et donc que l'on en sort grâce
    à une transition, on peut passer le document dans un état. Ce
    passage a pour effet de créer une copie du document et de la rendre
    modifiable tout en la libellant avec l'intitulé de l'état

## Construction du cycle de vie

Nous allons construire le cycle de vie en conformité avec celui décrit
dans la spécification. Pour ce faire veuillez ouvrir Dynacase Studio et
créer un nouveau document de cycle de vie, en allant dans le menu
Dynacase et en cliquant sur Cycle de vie. Un nom logique vous est
demandé et vous précisez *QCO\_QUALITY\_WORKFLOW*.

Vous devez voir une IHM similaire à celle-ci dessous :

**image IHM à insérer ici**

Vous avez créé un document de cycle de vie vide, nous allons maintenant
lui ajouter les éléments manquants. Pour ce faire, veuillez aller dans
l'onglet *Activité* et ajouter les activités suivantes :

-   *QCO\_WFL\_QUAL\_A\_REDACTION* : avec le label *writing*,
-   *QCO\_WFL\_QUAL\_A\_VALIDATION* : avec le label *validation*,
-   *QCO\_WFL\_QUAL\_A\_APPROBATION* : avec le label *approbation*,
-   *QCO\_WFL\_QUAL\_A\_DIFFUSION* : avec le label *diffusion*.

Maintenant allez dans l'onglet *état* et ajoutez les deux états suivants
:

-   *QCO\_WFL\_QUAL\_E\_APPLICABLE* : avec le label *applicable*,
-   *QCO\_WFL\_QUAL\_E\_ABANDONNE* : avec le label *abandonned*.

Et finalement, vous créez dans l'onglet *Transition* les transitions :

  --------------------------------------------------------------------------
  Nom logique       Transition entrée Transition sortie  Label       Passage
                                                                     à
                                                                     l'état
  ----------------- ----------------- ------------------ ----------- -------
  QCO\_WFL\_QUAL\_T QCO\_WFL\_QUAL\_A QCO\_WFL\_QUAL\_A\ To          
  \_TO\_VALIDATION  \_REDACTION       _VALIDATION        validation  

  QCO\_WFL\_QUAL\_T QCO\_WFL\_QUAL\_A QCO\_WFL\_QUAL\_A\ Return in   
  \_RETURN\_IN\_WRI \_VALIDATION      _REDACTION         writing     
  TING                                                               

  QCO\_WFL\_QUAL\_T QCO\_WFL\_QUAL\_A QCO\_WFL\_QUAL\_A\ To          
  \_TO\_APPROBATION \_VALIDATION      _APPROBATION       approbation 

  QCO\_WFL\_QUAL\_T QCO\_WFL\_QUAL\_A QCO\_WFL\_QUAL\_A\ Return in   
  \_RETURN\_IN\_WRI \_APPROBATION     _REDACTION         writing     
  TING\_2                                                            

  QCO\_WFL\_QUAL\_T QCO\_WFL\_QUAL\_A QCO\_WFL\_QUAL\_A\ To          QCO\_WF
  \_TO\_APPLICABLE  \_APPROBATION     _DIFFUSION         diffusion   L\_QUAL
                                                                     \_E\_AP
                                                                     PLICABL
                                                                     E

  QCO\_WFL\_QUAL\_T QCO\_WFL\_QUAL\_A QCO\_WFL\_QUAL\_A\ Revision    
  \_REVISION        \_DIFFUSION       _REDACTION                     

  QCO\_WFL\_QUAL\_T QCO\_WFL\_QUAL\_A                                QCO\_WF
  \_ABANDON         \_REDACTION                                      L\_QUAL
                                                                     \_E\_AB
                                                                     ANDONNE
  --------------------------------------------------------------------------

Vous avez maintenant fini de configurer le cycle de vie. Allez dans
l'onglet visualisation et vous pouvez voir le cycle sous forme d'un
graphique.

**Image du cycle**

## Conclusion

Vous pouvez maintenant intégrer votre nouveau cycle de vie et visualiser
le graphe.
