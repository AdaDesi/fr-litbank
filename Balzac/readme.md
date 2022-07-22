### dossier pour stage ada

Ce dossier contient les prédictions, ainsi que les fichiers d'annotation corrigés pour deux romans de Balzac :
1. *La maison du Chat-qui-pelote*
2. *La maison Nucingen*
Il contient aussi les scripts Python utilisés pour nettoyer le fichier avec les prédictions, afin qu'il soit lu correctement par Brat.

La vérification de ces annotations, produites par le logiciel FrenchBookNLP, a été faite dans le cadre d'un stage de M2, réalisé au sein d'Obtic, équipe-projet du SCAI (Sorbonne Center for Artificial Intelligence) dédié aux humanités numériques, en collaboration avec le laboratoire Lattice (CNRS).
L'annotation des coréférences a été faite suivant le "Manuel d’annotation du corpus et organisation de formations sur l’annotation" crée pour le projet Democrat [LIEN].
L'annotation des entités nommées suit le guide d'annotation pour FrenchBookNLP, produit à partir du guide d'anntotation de la version multilangue de BookNLP [LIEN]. 

## ANNOTATIONS
Les prédictions ont été corrigées au moyen du logiciel Brat [LIEN]. Celui-ci ne permettait pas de lire le fichier avec toutes les annotations, que nous avons donc splitté, au moyen de la commande split de Bash; ensuite, puisqu'il manquait une des deux entités de certaines coréférences, nous avons ajouté à la main les entités qui permettaient de rétablir la liaison. 

Nous avions préalablement apporté quelques modifications aux fichiers contenant les prédictions et le texte :
1. Dans les fichiers d'annotation, nous sommes passé du caractère « ‘ » au caractère « ’ » pour l'apostrophe, car il n'était pas le même dans le fichier texte et dans les fichiers d'annotation ;
2. Le fichier avec les prédictions contenait des incohérences dûes à la gestion des espaces blancs et des retours chariot. Nous avons alors rétabli les bonnes bornes pour les mots, au moyen des deux scripts fournies.

Les

## REMARQUES SUR LES CORRECIONS

Après la vérification des annotations faites par French BookNLP, je peux tirer les remarques suivantes :
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


|Très fréquent|Fréquent|Occasionnel|Autre|
|---|---|---|---|---|
|Chaîne de coréférence interrompue|Annotation de parties d'immeubles annotées comme FAC|Annotation de mots du champs lexical de la nature comme LOC|Traitement des apostrophes|
|Présence d'une coréférence entre une entité constituée par une coordination (« et ») et le premier terme de la coordination|Annotation de pronoms relatifs d'entités qu'on n'annote pas|---|---|
|Présence d'une coréférence entre une entité contenant un adjectif possessif et cet adjectif|Mauvaise coréférence entre une entité et la première tête de chaîne qui la précéde|---|---|
|Age annoté comme TIME|Verbe conjugué annoté comme PERS et lié à son sujet|---|---|
