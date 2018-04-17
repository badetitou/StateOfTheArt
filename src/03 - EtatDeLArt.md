# État de l'art

La première étape de mon travail a été de le positionner par rapport à la littérature existante.

## Migration de plateforme

La _migration de plateforme_ traite de comment migrer une application d'un langage à un autre.
On y aborde par exemple la migration de plateforme pour des interfaces graphiques.

En particulier, l'article de Samir *et al.* [@samir2007swing2script] dans lequel il est question de la migration de Swing vers Ajax.
Les auteurs ont développé un outil appelé Swing2Script qui permet d'automatiser
  la migration d'application Java-Swing en une application web Ajax.
Cet outil permet d'extraire depuis une application Java les différentes fenêtres et de
  les transcrire au format XUL[^XUL].
Ensuite, l'outil ajoute à chacun des fichiers un fichier JavaScript contenant l'ensemble des fonctions pouvant être appelées.
Cependant, l'outil utilise une analyse dynamique de l'application pour détecter son fonctionnement.
Au vu de la taille des applications de Berger-Levrault ainsi que de l'impact de l'utilisation d'une telle stratégie sur les utilisateurs,
  je ne pourrai pas utiliser la même stratégie.

## Migration de librairie

La _migration de librairie_ présente des solutions sur comment changer de framework.

Teyton  *et al.* [@teyton2013automatic] ont proposé un outil permettant d'extraire depuis des migrations déjà effectuées
  les correspondances entre les appels d'un framework avec ceux d'un autre.
Pour cela, ils se basent sur les différences textuelles entre plusieurs versions d'un même projet.
À cause du nombre de versions qu'un projet peut avoir, ils utilisent un algorithme
  "diviser pour régner" afin d’accélérer le temps de calcul.
Ce travail peut nous servir une fois que BLCore aura migré, afin d'automatiser ou créer des outils
  facilitant le travail des développeurs.
Cependant, ce travail ne parle que de la migration au sein d'un même langage de programmation.
Il ne peut donc être utilisé tel quel pour faire migrer BLCore de GWT vers Angular 4.

L'article de Hora *et al.* [@hora2015automatic] explique une démarche pour extraire
  automatiquement des modifications faites dans un code afin d'en déduire des pattern.
Son objectif est de détecter les conventions de développement qui évoluent.
Son travail de recherche de correspondance entre certains morceaux de code
  et des nouveaux peut m'être utile pour la migration.
En effet, je vais aussi devoir trouver les correspondances entre du code Java
  et du code Angular.

Zhong  *et al.* [@zhong2010mining] ont voulu créer une approche visant à faire correspondre
  l'API[^api] d'un framework avec celui d'un autre, tous deux étant écrits dans des langages différents.
Pour cela, ils ont développé une stratégie appelée MAM (Mining API Mapping) qui prendra en
  paramètres deux projets dans deux versions différentes.
Ensuite, l'algorithme essaie de regrouper par minage les éléments identiques des deux projets
  (_i.e._ les classes, les méthodes).
Puis il construit un arbre d’exécution pour les méthodes et cherche les correspondances
  entre les méthodes qui sont appelées.
Cette approche ne peut pas m'aider à migrer BLCore,
  mais, si je migre quelques applications de Berger-Levrault,
  je pourrai réutiliser les stratégies employées par Zhong pour faciliter la migration d'autres applications.

L'article de Phan *et al.* [@phan2017statistical] propose de faire correspondre des éléments de code du langage Java
  vers le langage C#.
Plus précisément, ils ont développé un outil permettant de mettre en correspondance du code d'un langage utilisant
  une ou plusieurs API vers un autre langage utilisant une ou plusieurs autres API prédéfinies.
Pour cela, les auteurs utilisent un outil de recherche de correspondances entre des API provenant de Java vers C#.
Puis, ils utilisent une machine statistique de traduction automatique pour faire correspondre les utilisations des API Java et C#.
Une fois le modèle entraîné, ils arrivent à automatiser une partie de la migration.
Ce travail peut nous servir si l'on a migré BLCore et que l'on souhaite ensuite migrer les applications.
Comme lui, nous travaillons sur la migration de librairies de langages différents.

## Transformation de modèle

La _transformation de modèle_ traite de la modification d'un modèle source vers un modèle cible.

L'article de Baki *et al.* [@baki2016multi] présente un processus de migration d'un modèle UML vers un modèle SQL.
Pour faire la migration, les auteurs ont décidé d'utiliser des règles de transformation.
Ces règles prennent en entrée le modèle UML et donne en sortie le SQL définit par les règles.
Plutot que d'écrire les règles de migration à la main.
Les auteurs ont décomposées ces règles en petites briques.
Chaque brique peut correspondre soit à une condition à respectée pour que la règle soit validée, soit à un changement sur la sortie de la règle.
Ensuite, les auteurs ont développé un algorithme de programmation génétique pouvant manipuler ces règles.
L'algorithme va, à partir d'exemples, apprendre les règles de transformation à appliquer pour faire la transformation du modèle.
Pour cela, il va modifier les petites briques composants les règles et analyser si le modèle en sortie ressemble à
  celui explicité pour tout les exemples.
Puis, il sera utilisé sur des vrais données.
Ce travail peut être utilisé dans mon projet.
En effet, je peux aussi effectuer la migration en utilisant un modèle de l'application source et un
  modèle de l'application cible.
Toutefois, la complexité d'un code source Java semble plus grande que celle d'un modèle UML.
Il est possible que l'algorithme de programmation génétique ne soit pas assez performant pour régler mon problème de manière satisfaisante.

Falleri *et al.* [@falleri2008metamodel] ont travaillé sur le passage d'un méta-modèle à un autre.
C'est ce que l'on appelle l'alignement des méta-modèle.
Pour cela, les auteurs ont utilisé l'algorithme de *Similarity Flooding*.
Cet algorithme permet de trouver les similarités entre les deux graphe orientés et étiquetés aux arcs en entré du programme.
Les auteurs ont proposé des solutions pour convertir un méta-modèle en graphe orientés et étiquetés aux arcs.
Comme les auteurs, je peux décider d'effectuer la migration en passant par des modèles et méta-modèles.
Une fois les méta-modèle et modèles créés, je pourrai utilisé l'algorithme *Similarity Flooding* utilisée dans l'article
  pour effectuer la migration.

Wang *et al.* [@wang2017automatic] ont créé une méthodologie et un outil permettant de automatiquement faire la transformation d'un modèle vers un autre modèle.
Leur outil se distingue en effectuant une migration qui se base sur une analyse syntaxique et sémantique.
L'objectif de la méthodologie est d'effectuer la transformation d'un modèle vers un autre de manière itérative en modifiant le méta-modèle.
Une condition d'utilisation contraignante décrite par les auteurs est la nécessité d'avoir
  une méta-méta-modèle pour tous les méta-modèle intermédiaire.
Les auteurs ont implémenté un méta-méta-modèle dans leur outil.
Dans mon travail, une solution pour effectuer la migration serait d'utiliser des méta-modèle.
Le premier modèle proviendrait de l'application source, le second modèle respecterait le méta-modèle de destination.
J'ai donc la même problématique que les auteurs de passage d'un modèle à un autre.
En définissant un méta-méta-modèle que respecterai le méta-modèle de départ de l'application source et un méta-modèle de destination,
  la méthodologie proposé par les auteurs devrait pouvoir résoudre, totalement ou partiellement, mon problème de migration.

## Migration du code source

La *migration du code source* traite de la transformation du code source directement (*i.e.* sans passer par un modèle).

Brant *et al.* [@brant2010extreme] ont écrit un compilateur utilisant un outil nommé SmaCC.
SmaCC est un générateur d'analyseur pour Smalltalk.
Ils ont aussi utilisé le SmaCC Transformation Toolkit qui permet de définir des règles de transformations qui seront utilisées par SmaCC.
Ainsi, les auteurs sont parvenues à migrer une application Delphi de 1,5 million de ligne de code en C#.
Comme les auteurs, je veux effectuer la migration du code source d'une application.
Mon cas se différencie par les langages source et cible.
Ce travaille peut me servir si nous souhaitons effectuer la migration sans passer par un modèle intermédiaire.

Aucun des papiers trouvés et cités ne peut nous aider réellement à migrer le framework BLCore ou les applications si on décide que dans le futur, on supprime BLCore, puisqu'Angular, contrairement à GWT n'est pas du Java.
En revanche, si Berger-Levrault souhaite garder l'équivalent de BLCore dans le futur, alors ces travaux pourraient nous aider à migrer dans un deuxième temps les applications.

[^api]: API: Interface de programmation
[^XUL]: XUL: XML-based User interface Language est un langage de description d’interfaces graphiques fondé sur XML créé dans le cadre du projet Mozilla
