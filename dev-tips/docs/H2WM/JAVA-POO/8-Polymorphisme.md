---
sidebar_position: 8
---

# Polymorphisme

La capcité d'une methode à changer / à se comporter différemment en fonction de l'objet (lié à l'hérritage) qui lui est passé

Cela permet d'être conceptuel (ouvrir des possibilités)
On crée une classe dans laquelle on sait qu'il y aura des choses mais on ne sait pas encore quoi.  
ex : Une classe : être vivant
ex : Une classe : Widget

**Le polymorphisme est la capacité à exécuter une même action de différentes manières.**

## Exemple 1 :

Classe parents Forme
Classes enfants Rectangle / rond

méthode : calculersurface() avec une surcharge dans chaque clase enfant (polymorphisme) 

## Exemple 2 :

![alt text](polymorphisme.png)

## Autres exemple

un type Chien peut être un Animal :

> Possible  

**On peut ne rien mettre en les balise dans le new** cela dépend de l'entreprise où l'on travail

```JAVA
ArrayList<Animal> animaux = new ArrayList<Animal>();

animaux.add(Chien); // On peut mettre tous les types héritées de Animal
animaux.add(Chat);
```
un type Animal ne peut pas être un Chien :

> Pas possible  

```JAVA
ArrayList<Chien> animaux = new ArrayList<Chien>();

animaux.add(Animal);
animaux.add(Chat);
```

## Casting

Le casting est l'action de forcer une variable de référence à être traitée temporairement comme un type différent. Il est principalement utilisé pour changer la perspective du compilateur sur un objet, sans modifier l'objet lui-même.

### Upcasting (Montée) : Vers le Parent ⬆️

    Action : Changer le type de référence vers un type parent (super-classe ou interface).

    Syntaxe : Souvent implicite (automatique).

    Sûr ? Oui. Un Chien est toujours un Animal.

    Conséquence : La variable perd l'accès aux méthodes et attributs spécifiques au type enfant. C'est la base du polymorphisme.

        Exemple : Animal monAnimal = new Chien(); (Le Chien existe toujours, mais la variable monAnimal ne peut pas appeler la méthode aboyer().)

### Downcasting (Descente) : Vers l'Enfant ⬇️

    Action : Changer le type de référence vers un type enfant (sous-classe).

    Syntaxe : Explicite (doit être écrit entre parenthèses).

    Sûr ? Non. Risque de ClassCastException si l'objet réel n'est pas du type spécifié.

    Utilité : Retrouver l'accès aux méthodes et attributs spécifiques du type enfant qui étaient masqués par l'Upcasting.

        Exemple : Chien monChien = (Chien) monAnimal; (Permet maintenant d'appeler monChien.aboyer(), mais uniquement si l'objet pointé par monAnimal était bien un Chien à l'origine.)

```JAVA
//on fait un CASTING
// force dans le code a se comporter comme un chien
Chien nomVariable = (Chien) monAnimal;
nomVariable.aboyer() 
```

# Clarification Terminologique (Pour aller plus loin) 

Il est souvent utile de distinguer les deux principaux types de polymorphisme que l'on rencontre dans les langages comme Java :

## Polymorphisme Statique (ou Surcharge - Overloading)

    Quand ? Résolu à la compilation.

    Comment ? Plusieurs méthodes dans la même classe (ou dans des classes liées) partagent le même nom mais ont des signatures différentes (nombre, type ou ordre des paramètres).

    Exemple :

        additionner(int a, int b)

        additionner(double a, double b)

        additionner(int a, int b, int c)

## Polymorphisme Dynamique (ou Redéfinition/Écrasement - Overriding)

    Quand ? Résolu à l'exécution (via l'héritage).

    Comment ? Une classe enfant redéfinit (écrase) une méthode héritée de sa classe parente pour fournir une implémentation spécifique. C'est le cas de votre exemple.

    Votre Exemple :
    Java

    Forme maForme; // Déclaration statique
    maForme = new Rectangle(5, 10); // Instance dynamique
    maForme.calculerSurface(); // La bonne méthode est choisie à l'exécution !

    Ici, bien que la variable soit de type Forme, c'est la version de Rectangle de calculerSurface() qui est exécutée.

Votre exemple de calculerSurface() concerne le polymorphisme dynamique (le plus souvent appelé simplement "polymorphisme" dans le contexte de l'héritage), qui est le cœur de la flexibilité en POO.


