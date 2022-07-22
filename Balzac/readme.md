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
1. De manière générale, j'ai plus éliminé qu’ajouter des entités et des coréférences ; j'en ai modifié de nombreuses aussi ;
2. On trouve systématiquement une coréférence entre une entité constituée par une coordination (« et ») et le premier terme de la coordination ;
3. Les âges sont systématiquement annotés comme TIME ;
4. Presque systématiquement, des parties d’un immeuble sont annotées comme FAC ;
5. On trouve souvent des coréférences entre des mots qui ne représentent pas des entités
à annoter et leurs pronoms relatifs ;
6. De manière générale, les entités qui ont une coréférence sont liées à la première tête de
chaîne qui les précède, même si elles se réfèrent en réalité à une entité précédente ;
7. Les chaînes de coréférences sont très souvent interrompues ;
8. Souvent les verbes sont annotés comme PERS et parfois sont liés par une coréférence à
leur sujet ;
9. Je n'ai pas pu reconnaître une règle pour le traitement des apostrophes : les entités qui
en contiennent sont parfois composés d'une seule lettre, isolée ou faisant partie d'un mot, parfois d'un mot entier, et parfois on trouve une double coréférence de chaque partie de l’apostrophe ;
10. Les mots du champ lexical de la nature (« la nature », « le ciel », « le soleil », « le monde », « la pluie », « le temps », etc.) sont généralement annotés comme LOC, sauf quand ils sont le sujet d'un verbe, et dans ce cas ils sont annotés comme PERS.

