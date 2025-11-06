---
sidebar_position: 6
---

# Ttry catch

capter une erreur

```JAVA
 int choix = -1;
    while (choix > 4 || choix < 0) {
        String choixStr = IO.readln("entrez votre choix : ");
        try {
            choix = Integer.parseInt(choixStr);
        } catch (Exception ex) {
            System.out.println("Erreur veuillez saisir un nombre entre 1 et 4");
        }

        if (choix == 1) {
            additionner(numeroUn, numeroDeux);
        }
        if (choix == 2) {
            soustraire(numeroUn, numeroDeux);
        }
        if (choix == 3) {
            multiplier(numeroUn, numeroDeux);
        }
        if (choix == 4) {
            if (numeroDeux == 0) {
                IO.println("Division par zéro impossible.");
            } else diviser(numeroUn, numeroDeux);
        }
        if (choix > 4) {
            IO.println("choix d'opération non valide !");
        }
    }

```