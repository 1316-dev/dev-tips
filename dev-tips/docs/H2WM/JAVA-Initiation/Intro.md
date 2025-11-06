---
sidebar_position: 1
---

# Intro

## Généralité

### Java est un langage : 
* typé
* procédural
* orienté objet
* événementiel

### Syntaxe :
* {} bloc d'instructions
* ; fin d'instructions
* // commentaire sur une ligne (répond à pourquoi plutôt que quoi)
* /* */ commentaire sur plusieurs lignes

### Variables
* commence par une minusculre
* camelcase
* éviter : "_" et "$"
* interdit : espace, chiffre en premier et mot clé du langage

### Constantes:
* CONSTANTE
* MA_CONSTANTE
* final : ne peut pas être modifié
* static : permet d'accéder à la constante

### Méthodologie :

Régléchir fonctionnel

! ![diagramme](image.png)

```JAVA
public class Main {
    public static void main(String[] args) {

        // Prix pour chaque viennoiserie
        // Tableau entier (4 elements)
        // PS: Tableau vide de 4 elements
        // (en java int par defaut/vide = 0)
        int[] prices = new int[4];

        // Element : 1 -> Fonctionnellement c'est Chocolatine
        prices[0] = 12;

        // Element : 2 -> Fonctionnellement c'est Escargot au chocolat
        prices[1] = 6;

        // Element : 3 -> Fonctionnellement c'est Croissant au chocolat
        prices[2] = 2;

        // Element : 4 -> Fonctionnellement c'est Pain au choclat
        prices[3] = 1;

        // Afficher du texte
        System.out.println("Hello and welcome!");
    }
}
```


