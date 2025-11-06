---
sidebar_position: 5
---
# Les classes et instances - Démo

## Classe ("on déclare")

```JAVA
package demo3.model;

public class Person {
    //Attributs
    public String firstname;
    public int age;

    // Constructeur pour éviter dans l'application de créer chaque attribut
    // fonction avec le Même nom que la class
    // le nom du paramètre est subjectif, juste pour le développeur
    public Person(String firstname, int age) {
        this.firstname = firstname; // on met le this car le nom du paramètre à le même nom qu'une variable déclaré
        this.age = age;
    }

    //methode / fonctionnalité
    public void manger() {
        System.out.println("Je mange");
    }
}
```
```JAVA
package demo3.model;

public class Recette {
    public String name;
    public double price;
}
```


## Instance : ("on fait poper la données")



```JAVA
package demo3;

import demo3.model.Person;
import demo3.model.Recette;

public class DemoPersonApp {
    public static void main(String[] args) { // cela veut dire que c'est un programme qui se lance
        //Pour tester la classe demo3.model.Person

        // Créer une instance (grace au new) => on va pop une personne dans notre monde
        Person person1 =  new Person("Mel",25);


        person1.manger();

        //J'instancie une deuxieme personne

        Person person2 = new Person("Léo",16);




        // J'instancie une recette
        Recette recette1 = new Recette();
        recette1.name = "Pizza";
        recette1.price = 15.50;
    }


}
```
