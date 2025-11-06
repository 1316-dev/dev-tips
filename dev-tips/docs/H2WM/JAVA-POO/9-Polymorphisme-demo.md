---
sidebar_position: 10
---

# Démo polymorphisme

Voir création d'une arraylist de type "Characteres", qui contient des types "Hero" et type "Monster"

## Classe Parent

```JAVA
package gestiondynamique;

import java.util.ArrayList;

public class Characters {

    public String name;
    public ArrayList<Attribute> attributes;

    public Characters(String name) {
        this.name = name;
        attributes = new ArrayList<Attribute>();
    }


    public void addAttribute(Attribute at) {
        attributes.add(at);
    }

    public void showInfo() {
        System.out.println("Name of player : " + name);
        for (Attribute attribute : attributes) {
            System.out.println(  "- " + attribute.name + " : " + attribute.value);
        }
    }
}

```

## Classe Enfant

```JAVA
package gestiondynamique;

import gestiondynamique.Characters;

public class Monster extends Characters {
    private String species; // spécifique à cette class


    public Monster(String name, String species) {
        super(name); // appel de la class parent
        this.species = species;
    }

    @Override // modificationde la méthod showInfo déclarer dans parents Characters
    public void showInfo() {
        System.out.println("-----------------------------------");
        System.out.println("Type : Monster");
        System.out.println("Species : " + species);
        super.showInfo(); // récupération de l'effet de la méthode de parents
    }
}
```



```JAVA
package gestiondynamique;

public class Hero extends Characters {
    private String teamName; // spécifique à cette class


    public Hero(String name, String teamName) {
        super(name);// appel de la class parent
        this.teamName = teamName;
    }

    @Override // modificationde la méthod showInfo déclarer dans parents Characters
    public void showInfo() {
        System.out.println("-----------------------------------");
        System.out.println("Type : Héros");
        System.out.println("Team : " + teamName);
        super.showInfo(); // récupération de l'effet de la méthode de parents
    }
}

```

## Autre Classe

```JAVA
package gestiondynamique;

public class Attribute {
    public String name;
    public String value;


    public Attribute(String name, String value) {
        this.name = name;
        this.value = value;
    }
    public Attribute() {
    }

    public void show() {
        System.out.println(name + " : " + value);
    }
}

```


## Main

```JAVA
package gestiondynamique;

import demoheritage.Animal;

import java.util.ArrayList;

public class TPRpgAttribute {
    public static void main(String[] args) {

        //Création de héros
        Hero h1 = new Hero("Andy", "Le Cercle des Héros");
        // ajout d'attributs
        h1.addAttribute(new Attribute("race", "humain"));
        h1.addAttribute(new Attribute("class", "Palladin"));
        h1.addAttribute(new Attribute("niveau", "3"));
        // afffichage
        //h1.showInfo();

        Hero h2 = new Hero("Nova", "Le Cercle des Héros");
        // ajout d'attributs
        h2.addAttribute(new Attribute("race", "efl"));
        h2.addAttribute(new Attribute("class", "archery"));
        h2.addAttribute(new Attribute("niveau", "2"));


        //Création de Monstres
        Monster m1 = new Monster("Arg", "Orc");
        // ajout d'attributs
        m1.addAttribute(new Attribute("taille", "big"));
        m1.addAttribute(new Attribute("dangerosity", "3"));
        m1.addAttribute(new Attribute("housing", "cave"));



        Monster m2 = new Monster("Zorg", "Orc Noirs");
        // ajout d'attributs
        m2.addAttribute(new Attribute("taille", "small"));
        m2.addAttribute(new Attribute("dangerosity", "2"));
        m2.addAttribute(new Attribute("housing", "mountain"));


        //Création d'une liste de Personnages
        ArrayList<Characters> characters = new ArrayList<>();
        characters.add(m1); // possible grâce au polymorphisme m1 est de type <Monster> hérité de <Characters>
        characters.add(h1); // possible grâce au polymorphisme h1 est de type <Hero> hérité de <Characters>
        characters.add(m2);
        characters.add(h2);
        
        //affichage de la listes
        for (Characters c : characters) {
            c.showInfo();
        }
    }
}
```