### dossier pour stage ada

Ce dossier contient les prédictions, ainsi que les fichiers d'annotation corrigés pour deux romans de Balzac :
1. *La maison du Chat-qui-pelote*
2. *La maison Nucingen*
Il contient aussi les scripts Python utilisés pour nettoyer le fichier avec les prédictions, afin qu'il soit lu correctement par Brat.

La vérification de ces annotations, produites par le logiciel FrenchBookNLP, a été faite dans le cadre d'un stage de M2, réalisé au sein d'Obtic, équipe-projet du SCAI (Sorbonne Center for Artificial Intelligence) dédié aux humanités numériques, en collaboration avec le laboratoire Lattice (CNRS). 
L'annotation des coréférences a été faite suivant le "Manuel d’annotation du corpus et organisation de formations sur l’annotation" crée pour le projet Democrat [LIEN].
L'annotation des entités nommées suit le guide d'annotation pour FrenchBookNLP, produit à partir du guide d'anntotation de la version multilangue de BookNLP [LIEN]. 
Ce travail a été accompli par Ada Desideri (étudiante de M2), avec l'aide de Johanna Cordova (ingénieure d'étude à Obtic), Marco Naguib et Frédérique Mélanie (ingénieurs d'étude au Lattice), et en dialoguant avec Motasem Alrahabi (coordinateur scientifique d'Obtic). 

## REMARQUES SUR LES CORRECTIONS

Après la vérification des annotations faites par French BookNLP, je peux tirer les **remarques** suivantes :
1.	De manière générale, j'ai l'impression d'avoir plus éliminé qu’ajouté des entités et des coréférences ;
2.	Les chaînes de coréférences sont très souvent interrompues ;
3.	On trouve systématiquement une coréférence entre une entité constituée par une coordination et le premier terme de la coordination (par exemple, « Augustine et lui » et mis en relation avec « Augustine ») ; quand ce n'est pas le cas, la coordination et sa première partie renvoient à une entité précédente ;
4.	Il se passe la même chose lorsqu'une entité contient un adjectif possessif, qui fait donc partie de deux entités (par exemple, pour le premier cas, dans « nos filles », « filles » renvoie à « nos » ; pour le deuxième cas, « son atelier » et « son » renvoient toutes les deux à « ce passant ») ;
5.	Les âges sont systématiquement annotés comme TIME ;
6.	Les parties d’un immeuble sont presque toujours annotées comme FAC ;
7.	On trouve souvent des coréférences entre des mots qui ne représentent pas des entités à annoter (par exemple « la queue ») et leurs pronoms relatifs ;
8.	De manière générale, les entités qui ont une coréférence sont liées à la première tête de chaîne qui les précède, même si elles se réfèrent en réalité à une entité précédente ;
9.	Souvent les verbes sont annotés comme PERS et parfois sont liés par une coréférence à leur sujet ;
10.	Je n'ai pas pu reconnaître une règle pour le traitement des apostrophes : les entités qui en contiennent sont parfois composés d'une seule lettre, qui peut être isolée (par exemple, « l' » dans « l'avaient ») ou qui peut faire partie d'un mot (par exemple, « l'e » dans « l'embrasse », ou « qu'e » dans « qu'elle »), parfois d'un mot entier (par exemple « l'artiste ») ;
11.	Les mots du champ lexical de la nature (« la nature », « le ciel », « le soleil », « le monde », « la pluie », « le temps », etc.) sont généralement annotés comme LOC, sauf quand ils sont le sujet d'un verbe, et dans ce cas ils sont annotés comme PERS.  

***Pour résumer :***
|Très fréquent|Fréquent|Occasionnel|Autre|
|---|---|---|---|
|Chaîne de coréférence interrompue|Annotation de parties d'immeubles annotées comme FAC|Annotation de mots du champs lexical de la nature comme LOC|Traitement des apostrophes|
|Présence d'une coréférence entre une entité constituée par une coordination (« et ») et le premier terme de la coordination|Annotation de pronoms relatifs d'entités qu'on n'annote pas| | |
|Présence d'une coréférence entre une entité contenant un adjectif possessif et cet adjectif|Mauvaise coréférence entre une entité et la première tête de chaîne qui la précéde| | |
|Age annoté comme TIME|Verbe conjugué annoté comme PERS et lié à son sujet| | |

## ANNOTATIONS
Les prédictions ont été corrigées au moyen du logiciel Brat [LIEN]. Celui-ci ne permettait pas de lire le fichier avec toutes les annotations, que nous avons donc splitté, au moyen de la commande split de Bash; ensuite, puisqu'il manquait une des deux entités de certaines coréférences, nous avons ajouté à la main les entités qui permettaient de rétablir la liaison. 

Nous avions préalablement apporté quelques **modifications aux fichiers contenant les prédictions et les textes** :
1. Dans le fichier des prédictions, nous avons substitué le caractère « ‘ » par le caractère « ’ » pour l'apostrophe, car il n'était pas le même dans le fichier texte et dans le fichier des prédictions ;
2. Le fichier avec les prédictions contenait des incohérences dûes à la gestion des espaces blancs et des retours chariot. Nous avons alors rétabli les bonnes bornes pour les mots, au moyen des deux scripts fournies.

**Lors de la vérification des prédictions sur Brat**, j'ai fait les choix suivants :
1. En passant d'un fichier d'annotation au suivant, au moment de l'ouverture du deuxième, je remonte quelques lignes pour annoter les dernières entités qui apparaissaient dans le fichier précédent, afin de les relier aux éventuelles nouvelles occurrences. Donc, pour une entité donnée, la tête de chaîne du deuxième fichier correspond au dernier maillon de la chaîne du fichier précédent.
2. De manière générale, pour établir une coréférence à partir d'un certain mot, je le lie au dernier maillon le plus explicite de la chaîne; par exemple, si on a une chaine composée par "Augustine->elle->sa fille->Augustine->elle", et que l'on doit ajouter "la femme du peintre" à cette chaîne, on crée une coréférence entre "la femme du peintre" et la dernière occurrence de "Augustine".

**En ce qui concerne l'annotation des personnages**, j'ai essayé d'établir des cas le plus précis possibles pour décider si un certain syntagme représente une entité nommée ou pas. De manière générale, j'ai privilegié les interprétations du texte selons lesquelles un syntagme représenterait une entité nommée.

-Les mots annotés sont en gras dans les exemples.-

**Je n'ai pas annoté un syntagme quand :**

1. Il représente le deuxième terme d'une comparaison, explicite ou pas, sauf s'il s'agit d'un référent unique - Caracalla, Humboldt, celle-là, etc.- :

|Exemples|Roman|
|---|---|
|Avec un enthousiasme d’archéologue|La maison du chat-qui-pelote|
|Autant de couches de diverses peinture que la joue d’une vieille duchesse en a reçu de rouge|La maison du chat-qui-pelote|
|Comme celui d’une veuve|La maison du chat-qui-pelote|
|Avait trouvé une secrète admiratrice dans **Mademoiselle Virginie**|La maison du chat-qui-pelote|
|**Il le** trouva trop joli pour un tigre|La maison Nucingen|

2. Il fait partie de l’imagination d’un personnage :

|Exemples|Roman|
|---|---|
|*Théodore* se créait un rival d’un l’un *des commis* et mettait les autres dans les intérêts de *son* rival|La maison du chat-qui-pelote|
|Si *je* me mariais, *je* voudrais avoir toute la peine, et voir *ma* femme heureuse|La maison du chat-qui-pelote|
|S’il y avait beaucoup de femme comme **celle-là**…|La maison du chat-qui-pelote|
|*J’*étais occupé à me dire [...] [qu']il vaudrait mieux se laisser aller à l’adorable passion enviée par *J.-J. Rousseau*, aimer tout bonnement une jeune personne comme *Isaure*|La maison Nucingen|

3. Il s’agit d’une manière de décrire un personnage qui vient d'être cité :

|Exemples|Roman|
|---|---|
|**Le commis** qui paraissait le plus jovial|La maison du chat-qui-pelote|
|**Ol** redevient l’homme du midi, le voluptueux, le diseur de riens, l’inoccupé Rastignac|La maison Nucingen|
|En **ta** qualité d’ancien propriétaire de journaux et revues|La maison Nucingen|
|**Le marquis d’Aiglement**, son tuteur|La maison Nucingen|

4. On se réfère à une catégorie abstraite, qui ne peut en aucun cas être associée à un référent unique ou partagé par beaucoup de personnes, ou qui sert à enoncer un principe général :

|Exemples|Roman|
|---|---|
|Quel autre nom le flâneur pouvait-il donner aux X et aux V que traçaient sur la façade les pièces de bois...|La maison du chat-qui-pelote|
|Le plus spirituel **des peintres modernes** n’inventerait pas de charge si comique|La maison du chat-qui-pelote|
|Quelques incertitudes qui devaient inquiéter de consciencieux flaneurs|La maison du chat-qui-pelote|
|Ceux qui croient que le monde devient de plus en plus spirituel|La maison du chat-qui-pelote|
|À plus d’un négociant parisien|La maison du chat-qui-pelote|
|Le front n’est-il pas ce qui se trouve de plus prophétique en l’homme ?|La maison du chat-qui-pelote|
|L’homme le plus froid devait en être impressionné|La maison du chat-qui-pelote|
|Les plus célèbres docteurs|La maison du chat-qui-pelote|
|Tout le monde|La maison du chat-qui-pelote|
|Un homme du monde n’aurait pu reprocher à *cette charmante créature* que des gestes mesquins|La maison du chat-qui-pelote|
|La coquetterie innée chez la femme|La maison du chat-qui-pelote|
|Comme disent les femmes|La maison du chat-qui-pelote|
|Tout homme supérieur doit avoir, sur les femmes, les opinions de l’Orient|La maison Nucingen|
|La loi punit le contrefacteur|La maison Nucingen|
|Pour **eux**, il n’y a plus de moi. Toi, voilà **leur** Verbe incarné.|La maison Nucingen|
|Le banquier est un conquérant qui...|La maison Nucingen|

5. Il représente un nom écrit ou cité :

|Exemples|Roman|
|---|---|
|*Les passants* lisaient Guillaume ; et à gauche, successeur du sieur Chevrel|La maison du chat-qui-pelote|
|Guillaume et Lebas, ces mots ne feraient-ils pas une belle raison sociale ?|La maison du chat-qui-pelote|
|*Son père* s’appelait le chevalier de Sommervieux|La maison du chat-qui-pelote|

**J'ai annoté un syntagme quand :**

1. Il s'agit d'une description qui sert comme référence à un personnage :

|Exemples|Roman|
|---|---|
|*Ce débris de la bourgeoisie du du seizième siècle* offrait à l’observateur|La maison du chat-qui-pelote|
|*Cet inconnu* se dépitait si bien...|La maison du chat-qui-pelote|
|Réfugiés au fond de *leur* grenier pour jouir de la colère de *leur victime*|La maison du chat-qui-pelote|
|*Le rusé négociant*|La maison du chat-qui-pelote|
|*Ce premier ministre* était admis à partager les plaisirs de la famille|La maison du chat-qui-pelote|
|Dix de *ces employés dont le sybaritisme enfle aujourd’hui les colonnes du budget*|La maison du chat-qui-pelote|
|Un homme du monde n’aurait pu reprocher à *cette charmante créature* que des gestes mesquins|La maison du chat-qui-pelote|La maison du chat-qui-pelote|
|en rendant à *un orphelin* le bienfait qu’il avait reçu jadis de *son prédécesseur*|La maison du chat-qui-pelote|
|Certains moments pendant lesquels *deux femmes* ne sont pas toujours libres de diriger *leurs* pas dans les galeries|La maison du chat-qui-pelote|
|L’alliance d’*une femme aimante* avec *un homme d’imagination*|La maison du chat-qui-pelote|
|Ce serait faire *mon* malheur que de me sacrifier à *un autre*|La maison du chat-qui-pelote|
|*Un poisson qui pèse dix-huit mille livres de rentes*|La maison Nucingen|


2. Il réfère à une personne ou un ensemble de personnes, même abstraits, mais faisant parti d’un contexte dans la narration, ou ayant une caractéristique particulière, reconnue de manière unique par beaucoup de monde (groupe de personnes rassemblées par un métier, une activité, un lieu de vie, une relation avec un autre personnage, un lieu, un événement, etc.)

|Exemples|Roman|
|---|---|
|Qui donnent *aux historiens* la facilité de reconstruire par analogie l’ancien Paris|La maison du chat-qui-pelote|
|*L’artiste* avait voulu se moquer *du marchand* et *des passants*|La maison du chat-qui-pelote|
|La queue des chats de *nos ancêtres*|La maison du chat-qui-pelote|
|Malgré le bruit que faisaient *quelques maraîchers attardés* passant au galop|La maison du chat-qui-pelote|
|*Elle* avait entendu *des plaisants* parier qu’*elle* y était empalée|La maison du chat-qui-pelote|
|*Les auteur dont la lecture leur était permise par leur mère*|La maison du chat-qui-pelote|
|*Ce démon dont les terribles pièges lui étaient prédits par la parole tonnante des prédicateurs*|La maison du chat-qui-pelote|
|Ce soir-là, *tous les amants* dormirent presque aussi paisiblement que *monsieur et madame Guillaume*|La maison du chat-qui-pelote|
|Chez *les prisonniers* comme chez *les amants*|La maison du chat-qui-pelote|
|*Cette maison*, *où* une pensée entachée de poésie devait produire un contraste avec *les êtres* et les choses|La maison du chat-qui-pelote|
|*Il* songeait déjà pour *mademoiselle Virginie* à *l’un de ses amis*|La maison du chat-qui-pelote|
|*Ces vieilles familles où se conservaient, comme de précieuses traditions, les mœurs, les costumes caractéristiques de leurs professions*|La maison du chat-qui-pelote|
|aux voisins|La maison du chat-qui-pelote|
|Parcourir les salons en s’y montrant avec l’éclat emprunté de la gloire de *son mari*, se voir jalousée par *les femmes*|La maison du chat-qui-pelote|
|*Une jeune fille* assise dans un comptoir entre *deux femmes* telles que…|La maison du chat-qui-pelote|
|*Une femme de beaucoup d’esprit* disait...|La maison Nucingen|
