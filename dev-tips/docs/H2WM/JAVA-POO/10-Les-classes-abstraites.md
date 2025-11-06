---
sidebar_position: 10
---

# Les classes Abstraites

N'a lieu d'être que dans le cadre de l'héritage

On utilise le mot abstract.

Les classes abstraites sont l'opposé des classes concrètes

Classes abstraites = non-instanciables / "on ne peut pas le créér" ex : Forme

Classes concrètes = instanciables ex : Rond / Rectangle

**Toutes les classes enfants concrètes qui hérite de cette classe doivent redéfinir les méthodes abstaites définis**

Notion de contrat (voir 11- Les interfaces):

Toutes les méthodes qui seront définit abstraites dans la classe abstraites doivent être redéfinit dans les classes enfants concrètes

## méthode abstraites

C'est une méthode dont on n'est **pas obliger de définir le comportement** (ce qu'il y a entre {}) mais on **définit sa signature.**

### Exemple 

CLASSE PARENT :  FORME

```JAVA
package model;

public abstract class Forme {
    private String name;

    //constructeur
    public Forme(String name) {
        this.name = name;
    }

    //méthode abstraite pour calculer la surface
    public abstract double calculerSurface();
}
```

La méthode sera ensuite redefinit dans les classes enfant/hérité

CLASSE ENFANT : ROND

```JAVA
package model;

public class Cercle extends Forme {
    private double rayon;

        public Cercle (String name, double rayon) {
            super(name);
            this.rayon = rayon;
        }

    @Override
    public double calculerSurface() {
        double surfaceRond = Math.PI * rayon * rayon;
        return surfaceRond;
    }

}
```

CLASSE ENFANT : RECTANGLE

```JAVA
package model;

public class Rectangle extends Forme {
    private double longueur;
    private double largeur;

    public Rectangle (String name, double longueur, double largeur) {
        super(name);
        this.longueur = longueur;
        this.largeur = largeur;

    }

    @Override
    public double calculerSurface() {
        double surfaceRectangle =  longueur*largeur ;
        return surfaceRectangle;
    }
}
```

