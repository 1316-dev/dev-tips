---
sidebar_position: 2
---

#Bonnes Pratiques

**Tout est carré dans des carrés dans des carrés !!**
DAns les fichers
DAns l'algo

**peut être présenté dans la soutenance**
- ne pas dire l'email est bon mais pas le mot de passe :
    - car on sait que l'email est dans la base de donnée
    - il faut donc tester identifiant + mot de passe et afficher erreur
    - si "mot de passe oublié" cliqué : écrire "un lien a été envoyé" même si l'email n'existe pas 
    - lors de l'inscription si l'email existe on valide l'inscription quand même et on envoit un mail avec écrit votre compte existe déjà. on affiche "inscription validé ouvrez votre mail"

site : refactoring.guru
- https://refactoring.guru/refactoring

## Rangement des fichiers/dosiers

plutôt que ranger les dossiers par type :
- un dossier html 
- un dossier css avec tous les css
- un dossier js avec tous les js
- ...

**Ranger par context (features/besoin/métier)** :
- login /
    - tout les fichiers liées (css, js, java)
- Android
  - tout les fichiers liées (css, js, java)
- Apple
  - tout les fichiers liées (css, js, java)
- Input
  - tout les fichiers liées (css, js, java)
- AI module
  - tout les fichiers liées (css, js, java)
- ...

## Bien nommer les classes et les fichiers

Class : PascalCase

package : monpackage.java



## Apprendre à coder proprement

### Les commentaires
- Pour commenter une fonction ou un attributs /** /
cela va créer la javadoc de note programme

```JAVA
        /**
         * La fonctionnalité pour faire un virement
         * @param amount
         */
        public static void virement (int amount) {
            
        }
```

### If pour un boolean
- if sur un boolean :
    - if(boolean) au lieu de if(boolean == true)


### Exemple avec if else imbriqué si on peut se passer du else

- exemple : https://refactoring.guru/replace-nested-conditional-with-guard-clauses

#### Ancienne écriture :

```JAVA
package demotrainning;

public class DemoBankApp {
    /**
     * La fonctionnalité pour faire un virement
     *
     * @param amount
     */
    public static boolean virement(int amount) {
        //Simuler que le compte n'est pas bloqué
        boolean lockedAccount = false;
        //Simuler le comte cible n'est pas bloqué
        boolean targetAccountExist = true;
        //simuler un solde
        int solde = 3500;

        //Variable pour savoir si ca marche par défault ca ne marche pas
        boolean caMarche = false;

        //Si n'est pas bloqué je continue
        if (!lockedAccount) { // lockedAccount == false
            //Si le solde est suffisant je continue
            if (amount <= solde) {
                // Si le compte distant existe
                if (targetAccountExist) { //targetAccountExist == true
                    //Ca marche
                    caMarche = true;
                } else {
                    caMarche = false;
                }
            } else {
                caMarche = false;
            }
        } else {
            caMarche = false;
        }
        return caMarche;
    }

    public static void main(String[] args) {
        // Appeler la fonction
        boolean estCequeLeVirement1Marche = virement(1000);
        boolean estCequeLeVirement2Marche = virement(4000);

    }
}
```

Nouvelle logique on teste d'abord les erreurs en inversant les condition, si ca marche pas on return  
> "On passe les murs"  

> "un carré pour chaque erreur possible"  


#### Nouvelle écriture :

```JAVA
package demotrainning;

public class DemoBankApp {
    /**
     * La fonctionnalité pour faire un virement
     *
     * @param amount
     */
    public static boolean virement(int amount) {
        //Simuler que le compte n'est pas bloqué
        boolean lockedAccount = false;
        //Simuler le comte cible n'est pas bloqué
        boolean targetAccountExist = true;
        //simuler un solde
        int solde = 3500;

        // on inversa la condition de l'ancienne méthode
        // si le compte est bloqué (STOP ERREUR)
        if (lockedAccount) {
            return false;
        }
        // si le compte est bloqué (STOP ERREUR)
        if (amount > solde) {
            return false;
        }

        if (!targetAccountExist) {
            return false;
        }
        //ok
        return true;
    }

    public static void main(String[] args) {
        // Appeler la fonction
        boolean estCequeLeVirement1Marche = virement(1000);
        boolean estCequeLeVirement2Marche = virement(4000);

    }
}
```
## If else (sans le esle)

Dans une fonction, s'il n'y a pas de code après un else, autant enlever le else :

```JAVA
public void test(){
    boolean logged = true;
    if (logged){
        Sytem.out.println("test");
        return;
    }
    System.out.println("test2");
}
```

Plutot que :

```JAVA
public void test(){
    boolean logged = true;
    if (logged){
        Sytem.out.println("test");
        return;
    }
    else {
    System.out.println("test2");
    return;
    }
}
```

## Affichage String 3 méthodes

### String literal/interpolation (méthode plus ancienne)

System.out.print la bonne pratique

```JAVA
package entrainement;

public class DemoStringPropreApp {

    public static void main(String[] args) {
        // BAD
        String firstname = "Isaac";
        System.out.println("Bonjour " + firstname);

        // GOOD
        String firstname_1 = "Isaac";
        // "Bonjour %s" %s = un string (par ordre) => donc le premier string
        System.out.println(String.format("Bonjour %s %d", firstname_1, 15));

        // String format caché
        System.out.printf("Bonjour %s %d", firstname_1, 15);

        // "Bonjour %s" %s = un string (par ordre) => donc le premier string
        String stringTransformer = String.format("Bonjour %s %d", firstname_1, 15);
        // stringTransformer dans notre cas deviendra Bonjour Isaac 15
    }
}
```

```JAVA
StringBuilder monConstructeurDeChaineDeCharacter = new StringBuilder();

monConstructeurDeChaineDeCharacter.append()

for (int i = 1; i<=5; i++) {
    
    System.out.printf("i=%d",i)
}
```

### StringBuilder (plus moderne car plus performant mais moins lisible)

**Elle permet d'appeler une seule fois System.out.printf en construisant no string en amont**

https://www.ionos.fr/digitalguide/sites-internet/developpement-web/stringbuilder-en-java/

La classe Java StringBuilder dispose de quatre constructeurs qui aident à mettre la chaîne de caractères dans le format approprié pour la classe.  
Ils servent également à la configuration. Voici les constructeurs et leurs fonctions :

    - StringBuilder() : génère un StringBuilder vide d’une capacité maximale de 16 caractères.
    - StringBuilder(int capacity) : crée un StringBuilder sans caractères, dont le nombre maximal de caractères est défini à l’aide de l’argument capacity.
    - StringBuilder(CharSequence seq) : génère un StringBuilder avec les mêmes caractères que la séquence de caractères, CharSequence, déposée.
    - StringBuilder(String str) : crée un StringBuilder sur la base de la chaîne déposée.


```JAVA
StringBuilder monConstructeurDeChaineDeCharacter = new StringBuilder();


for (int i = 1; i<=5; i++) {
    monConstructeurDeChaineDeCharacter.append("i= ").append(i).append("\n");
    //monConstructeurDeChaineDeCharacter.append(i)
    //monConstructeurDeChaineDeCharacter.append("\n") //retour à la ligne
    //monConstructeurDeChaineDeCharacter.append("\n") //retour charriot, on ne quitte pas le paragraphe
}

System.out.printf(monConstructeurDeChaineDeCharacter.toString()); // toString pas obliger mais plus explicitee pour atutre développeur (marche sans car est fait implicitement dans JAVA)

```
voir autre exemple dans tp medecin generaliste
### Concatenation (plus simple et plus lisible, moins performant)

En utilisant le "+"

```JAVA

for (int i = 1; i<=5; i++) {
    System.out.println("i="+i);
}

```

autre comparaisons :

```JAVA
    public void afficher() {
        /* Avec une concaténation ;
        System.out.println(nom.toUpperCase() + "  " + prenom);
        System.out.println("Téléphone : " + telephone);
        System.out.println("Tarifs : " + tarif);
        */

        /* autre proposition avec un string builder
        StringBuilder sb = new StringBuilder();
        sb.append(this.nom.toUpperCase()).append(" ").append(this.prenom).append("\n");
        sb.append("Téléphone : ").append(this.telephone).append("\n");
        sb.append("Tarifs : ").append(MedecinGeneraliste.tarif).append("\n"); // on remplace le this car tarif est un attribut de classe
        System.out.println(sb.toString());
        */

        // autre proposition avec un string builder sans le sb à chaque fois
        //comme si tout était collé mais plus lisible avec un retour à la ligne
        StringBuilder sb = new StringBuilder();
        sb.append(this.nom.toUpperCase()).append(" ").append(this.prenom).append("\n")
            .append("Téléphone : ").append(this.telephone).append("\n")
            .append("Tarifs : ").append(MedecinGeneraliste.tarif).append("\n"); // on remplace le this car tarif est un attribut de classe
        System.out.print(sb); // to string appelé de manière explicite
        // System.out.print(sb.toString()) // plus explicite pour la relecture du code

    }
```