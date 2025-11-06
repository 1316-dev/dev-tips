---
sidebar_position: 4
---

# Boucles et Conditions

## Les Boucles

### For
```JAVA
for (int compteur2 = 1; compteur2 <= 5; compteur2++)
        {
            IO.println (compteur2);
        }
        IO.println ("Terminé");
```
### For each
```JAVA
String[] tabSaisons = {"printemps","été","automne","hiver"};
for (String saison : tabSaisons) {
    System.out.println(saison);
}
```
### while
```JAVA
int compteur = 1;
        while (compteur <= 5)
        {
            IO.println (compteur);
            compteur++;
        }
       IO.println ("Terminé");
```
### do while
```JAVA
int compteur = 1;
        do
        {
            IO.println (compteur);
            compteur++;
        }
        while (compteur <= 5);
        IO.println ("Terminé");
```

## Les conditions

### if
```JAVA
   int age = 19;

    if (age >= 18 ) {
        IO.print("Vous êtes majeur");
    } else IO.print("vous êtes mineur");
```
### if imbriqués
```JAVA
    int entier = 15;
    If (entier % 3 = 0) {
        System.out.print("Fizz")
    }
    If (entier % 5 = 0) {
        System.out.print("Buzz")
    }
    else System.out.print(entier)
```
### if else if
```JAVA
int note = 10;
    if (note < 8) {
        IO.println("non acquis");
    } else if (note > 8 && note <= 12) {
        IO.println("en cours d'acquisition");
    } else if (note > 12) {
        IO.println("acquis");
    }
```
### switch case avec int
```JAVA
    int choix = 1;
    switch (choix) {
        case 1 : 
            System.out.print("Lundi")
            break;
        case 2 : 
            System.out.print("Mardi")
            break;
        case 3 : 
            System.out.print("Mercredi")
            break;
            //gestion des erreurs de saisis de choix
        default : IO.println("choix n'ont pris en compte");
    }
```

### switch case avec String
```JAVA
    int jour = "lundi";
    switch (choix) {
        case "lundi" : 
            System.out.print("Semaine")
            break;
        case "mardi" : 
            System.out.print("Semaine")
            break;
        case "Samedi" : 
            System.out.print("Weekend")
            break;
            //gestion des erreurs de saisis de choix
        default : IO.println("choix n'ont pris en compte");
    }
```