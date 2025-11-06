---
sidebar_position: 3
---

# Les Tableaux

## Déclaration Tableau

Pour afficher le contenu d'un tableau, on fait une boucle for

```JAVA
void main () {
    String [] saisons = {"printemps","été","automne","hiver"};
    for (int ii = 0 ; ii < saisons.length; ii++) {
        String nomSaison = saisons [ii] ;
        IO.println(nomSaison);
    }
    int[] année = new int [12];
    for (int jj = 0 ; jj < année.length; jj++) {
        année[jj] = jj +1 ;
        IO.println(année[jj]);
    }
}
```

## utiles: 
- Arrays.toString() : affiche le texte d'un tableau


## Déclaration Tableau 2D

```JAVA
import java.util.Arrays;

void main ()  {
    int [] [] tab2D = new int [] [] {
            {1,2,3,4,5},
            {6,7,8,9,10},
            {11,12,13,14,15}
    };
    for (int ii = 0 ; 0 <15; ii++)
    IO.println(Arrays.toString(tab2D[ii]));
}
```
