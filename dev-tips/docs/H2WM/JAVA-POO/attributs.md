
# Les Attributs

Différence entre un attribut de classe (ou statique) et un attribut d'instance (ou non-statique) :

## Attribut de Classe (Statique)

Un attribut de classe est déclaré avec le mot-clé static.

![alt text](attributDeClasse.png)

exemple avec un setter :

```JAVA
    public static void setTarif(int newTarif) {
        MedecinGeneraliste.tarif = newTarif;
    }
```

## Attribut d'Instance (Non-Statique)

Un attribut d'instance est déclaré sans le mot-clé static. C'est le type d'attribut le plus courant.

![alt text](attributDInstance.png)

exemple avec un setter :

```JAVA
  public void setNom(String nom) {
        this.nom = nom;
    }
```

**À Retenir**

La différence fondamentale réside dans l'endroit où la donnée est stockée et comment elle est partagée :

![alt text](attributSynthese.png)

**En résumé** :  
Si on change la valeur d'un **attribut d'instance** sur un objet, cela n'affecte pas les autres objets.  
Si on change la valeur d'un **attribut de classe**, ce changement est visible immédiatement par toutes les instances.

## Exemple 

```JAVA
public class MedecinGeneraliste {
    private String nom; // attribut d'instance
    private String prenom; // attribut d'instance
    private String telephone; // attribut d'instance
    private static int tarif = 25; // attribut de classe / commun a tous les medecins
}
```
Pour trouver un attribut de classe on utilise le nom de la classe plutot que this
```JAVA
// autre proposition avec un string builder
        StringBuilder sb = new StringBuilder();
        sb.append(this.nom.toUpperCase()).append(" ").append(this.prenom).append("\n");
        sb.append("Téléphone : ").append(this.telephone).append("\n");
        sb.append("Tarifs : ").append(MedecinGeneraliste.tarif); // on remplace le this car tarif est un attribut de classe

```