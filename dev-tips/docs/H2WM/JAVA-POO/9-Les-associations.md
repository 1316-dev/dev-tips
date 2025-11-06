---
sidebar_position: 9
---

# Association

Différence entre unidirectionnel et bidirectionnel

![alt text](association.png)

## Unidirectionnel

Une classe A prend en attribut un type Classe B

Exemple : Une classe Voiture a un attribut de type Moteur. Le Moteur ne connaît pas (n'a pas de référence à) la Voiture.


## Bidirectionnel

La classe A prend en attribut un type Classe B

La classe B prend en attribut un type Classe A

Les deux classes garde doivent conserver une référence l'une à l'autre

Exemple : Une classe Client a une liste d'attributs de type CompteBancaire. La classe CompteBancaire a un attribut de type Client (son propriétaire).

## Cardinalité (Multiplicité)

###  Notation et Exemples Courants

La notation de la multiplicité en UML est très standardisée. Voici les valeurs les plus courantes et leur signification :

![alt text](cardinalite.png)

### Application dans un Diagramme de Classes

Considérons une association entre une classe Équipe et une classe Joueur :
Eˊquipe0..1⟵​Jouer dans1..∗⟶​Joueur

    Côté Joueur vers Équipe (Multiplicité: 0..1) :

        Un Joueur peut être dans zéro ou une Équipe. (Il peut être sans équipe ou dans une seule).

    Côté Équipe vers Joueur (Multiplicité: 1..*) :

        Une Équipe doit avoir au moins un Joueur (un ou plusieurs).

La cardinalité est essentielle car elle permet de définir **les règles métier** et d'influencer la manière dont la relation sera implémentée en code (par exemple, si vous utilisez un simple attribut, une liste, ou si vous permettez la valeur null).

## Les relations d'agrégation (losange blanc en UML)

Relation contenu-contenant  **"Possède un"** (possession faible) où le contenu survit à la destriction du contenant
Si on détruit la classe A, la classe B peut continuer à exister et vis-versa.

Exemple Classe Train et classe Wagon avec le losange sur la classe train

## Les relations par composition (losange noir en UML)

Relation contenu-contenant **"fait partie de"** (possession forte) où le contenu ne survit pas à la destruction du contenant
Si on détruit la classe A, la classe B **ne peut pas** continuer à exister

Exemple Classe Livre et classe Page avec le losange sur la classe Livre

    L'essentiel à retenir, que vous avez très bien formulé, est la dépendance existentielle :

    **Agrégation** : Relation faible. La partie peut avoir une vie indépendante.

    **Composition** : Relation forte. La partie est gérée exclusivement par le tout.