---
sidebar_position: 5
---

# METHODES

## Fonctions (return)

Renvoie quelquechose avec return

```JAVA
static int add(int a, int b){
        int result1 = a + b;
        // Retourner une valeur 
        return result1;
    }

    public static void main(String[] args) {
       // Additionner 10 et 20
       int result1 = add(10, 20);
       
       System.out.println("Le resultat 1 est : " + result1);
       
       // Additionner 5 et 8
       int result2 = add(5, 8);
       
       System.out.println("On remarque que le resultat 2 est : " + result2);
    }

```

## Procedure (void)

C'est une fonction classique qui execute du code et ne renvoi rien
```JAVA
private static void afficherBonjour(int repetition) {
    IO.println("#########################");
    IO.println("affichage de " + repetition + " fois bonjour");
    IO.println("#########################");
    for (int ii = 0 ; ii < repetition ; ii++) {
        IO.println("Bonjour");
    }
}
```
