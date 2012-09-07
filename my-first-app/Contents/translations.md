# i18n & l10n

## Introduction

Nous allons maintenant voir l'implémentations des concepts
d'internationalisation et de régionalisation dans Dynacase. Pour rappel,
l'internationalisation consiste à préparer son adaptation une
application à des langues et des cultures différentes et la
régionalisation est le processus d'adaptation de l'application à une
culture particulière.

## Mise en pratique

### Internationalisation

Nous allons voir l'internationalisation au niveau des différents
éléments de Dynacase. Nous allons commencer par le code source, pour ce
faire veuillez ouvrir le fichier de code associé à la famille
*QCO\_QUALITY*.

Vous obtenez notamment le code suivant :

~~~~ {.Php}
    <?php
    public function checkUniqueTitle(){
        $searchOtherDocument = new SearchDoc("QCO_QUALITY");
        $searchOtherDocument->addFilter("QCO_TITLE = '%s'",$this->getValue("QCO_TITLE"));
        $nbDocument = $searchOtherDocument->count();
        if ($this->initid === null)
        {
            if ($nbDocument != 0){
                return array("err"=>"There is another document with the same title");
            }
        }
        else
        {
            if ($nbDocument > 1){
                return array("err"=>"There is another document with the same title");
            }
        }
    }
    ?>
~~~~

Cette fonction renvoie deux messages d'erreurs qui sont systématiquement
en anglais, nous allons donc la modifier de la façon suivante :

~~~~ {.Php}
    <?php
    public function checkUniqueTitle(){
        $searchOtherDocument = new SearchDoc("QCO_QUALITY");
        $searchOtherDocument->addFilter("QCO_TITLE = '%s'",$this->getValue("QCO_TITLE"));
        $nbDocument = $searchOtherDocument->count();
        if ($this->initid === null)
        {
            if ($nbDocument != 0){
                return array("err"=>_("There is another document with the same title"));
            }
        }
        else
        {
            if ($nbDocument > 1){
                return array("err"=>_("There is another document with the same title"));
            }
        }
    }
    ?>
~~~~

Nous avons inclu chaque chaîne de caractère dans un fonction \_(), cette
fonction permet de mettre en place le système de traduction.\
La fonction est maintenant prête pour être traduite, lors du processus
de régionalisation vous pourrez extraire ces chaînes de caractères et
les traduire. Attention, il y a une restriction au contenu de ces
chaînes, vous ne devez y mettre que des caractères US ASCII.\
De plus, si votre chaîne contient des parties variables comme la chaîne
suivante :

~~~~ {.Php}
    <?php
     $good = "very good";
     print "Dyncase is a $good tool";
    ?>
~~~~

Vous devez pour la rendre internationalisable la transformer de la
manière suivante

~~~~ {.Php}
    <?php
     $good = _("very good");
     print sprintf(_("Dyncase is a %s tool"),$good);
    ?>
~~~~

Vous pouvez remarquer comme précédemment l'utilisation de la fonction
\_() et aussi l'utilisation de
[sprintf](http://fr.php.net/manual/fr/function.sprintf.php). Cette
fonction permet (entre autre) de concétaner de manière traductible des
chaînes de caractères.

Nous allons maintenant voir l'internationalisation des documents
systèmes. Dans tous les documents systèmes possédant un libellé,
celui-ci est appelé *traduction label* et est utilisé dans le mécanisme
de traduction. Attention, toutefois seul les caractères US ASCII sont
acceptés dans ces chaînes.

### Régionalisation

Nous allons maintenant voir le mécanisme de régionalisation. Vous devez
générer le paquet de régionalisation, pour ce faire il vous faut vous
connecter au serveur http://adresse-ip-du-serveur/regionalisation.
L'interface suivante vous est présentée.

**Ajouter une capture d'écran**

Vous sélectionnez la cible de traduction ou en ajoutez une nouvelle,
puis vous sélectionnez les éléments à traduire (famille, application,
action,... ) et cliquez sur télécharger. Un fichier zip vous est alors
envoyé, ce fichier contient l'ensemble des dictionnaires de traduction
pour la langue en cours, ainsi que les CSS spécifiques à cette langue et
quelques page HTML d'exemple présentant les IHM sans traduction pour
permettre d'avoir le contexte de traduction.\
Ce paquet doit être utilisé par un traducteur et une équipe de design
prenant en compte les contraintes spécifiques à la culture pour laquelle
vous souhaitez traduire l'application.\
Une fois le travail effectué, vous vous reconnectez sur l'application
http://adresse-ip-du-serveur/regionalisation, vous sélectionnez à
nouveau la cible et vous uploadez le package. Une fois ce travail
effectué vous pouvez cliquer sur l'onglet exemple pour voir un exemple
de chaque formulaire de famille traduit.

## Conclusion

Ces mécanisme vous permette de mettre en place le contexte
d'internationalisation et d'effectuer simplement la régionalisation.
