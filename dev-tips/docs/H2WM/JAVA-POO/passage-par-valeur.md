# Passage par Valeur (voir slide p65)

Contrairement à certaines idées reçues, Java utilise strictement le passage par valeur (Pass-by-Value) pour tous les paramètres de méthode, qu'ils soient des types primitifs ou des objets. Il n'existe pas de véritable "passage par référence" (Pass-by-Reference) en Java comme dans certains autres langages (C++, C#, etc.).

Voici la différence clé dans la manière dont le passage par valeur s'applique en Java :

## 1️⃣ Passage par Valeur pour les Types Primitifs (e.g., int, boolean, char) 🔢

    Mécanisme : Lorsque vous passez un type primitif à une méthode, la valeur elle-même est copiée.

    Conséquence : La méthode appelée travaille avec cette copie locale de la valeur. Toute modification apportée à ce paramètre dans la méthode n'affecte pas la variable originale dans la méthode appelante.

    Exemple : Si vous passez int x = 10 à une méthode modifier(int val) et que vous faites val = 20 à l'intérieur, la variable x dans la méthode appelante restera 10.

## 2️⃣ Passage par Valeur pour les Objets (Types Non-Primitifs) 📦

    Mécanisme : Les variables d'objet en Java contiennent une référence (adresse mémoire) à l'objet réel stocké dans le heap. Lorsque vous passez un objet à une méthode, la valeur de cette référence est copiée et passée comme argument.

    Conséquence :

        Modification de l'état de l'objet : Comme la référence originale et la copie de la référence pointent toutes deux vers le même objet en mémoire, vous pouvez modifier les attributs (l'état) de cet objet à l'intérieur de la méthode, et cette modification sera visible à l'extérieur. C'est ce comportement qui crée souvent la confusion avec le "passage par référence".

        Réaffectation de la référence : Si vous essayez de réaffecter le paramètre de la méthode pour qu'il pointe vers un nouvel objet (par exemple, parametre = new AutreObjet();), cela ne changera que la copie locale de la référence dans la méthode. La référence originale dans la méthode appelante continuera de pointer vers l'objet initial.

Action dans la Méthode Appelée	Conséquence sur l'Original (pour les Objets)	Explication (Passage par Valeur)
Modifier l'état de l'objet (e.g., monObjet.setNom("Nouveau");)	Affecte l'objet original.	Les deux références (originale et copie) pointent vers le même objet.
Réaffecter la référence (e.g., monObjet = new AutreClasse();)	N'affecte pas la référence originale.	Seule la copie de la référence est modifiée pour pointer vers le nouvel objet; la référence originale reste inchangée.

## 📝 Résumé de la Confusion

La confusion vient du fait que :

    Types primitifs : La valeur est copiée (comportement clair du passage par valeur).

    Objets : La référence (qui est une valeur) est copiée, mais comme cette valeur copiée pointe vers le même objet, on peut modifier l'objet d'origine. C'est un passage par valeur de la référence.

En bref : Java est toujours passage par valeur. Le « ce qui est passé par valeur » diffère : la valeur du primitif ou la valeur de la référence d'objet.

Vous pouvez voir une explication détaillée de ce concept dans la vidéo ci-dessous : Java : 15- Passage par valeur vs. passage par référence. Cette vidéo explore la distinction entre le passage par valeur et le passage par référence dans le contexte de Java. 

```JAVA
// 1. Définition de la classe pour l'objet
class Personne {
    String nom;
    
    // Constructeur
    public Personne(String nomInitial) {
        this.nom = nomInitial;
    }
    
    // Getter pour afficher l'état
    public String getNom() {
        return nom;
    }
}

public class PassageParValeurDemo {

    // Méthode pour modifier un primitif (int)
    public static void modifierPrimitif(int nombre) {
        System.out.println("   -> Début méthode : nombre = " + nombre);
        // La copie locale est modifiée
        nombre = 99; 
        System.out.println("   -> Fin méthode : nombre = " + nombre);
    }

    // Méthode pour modifier un objet (Personne)
    public static void modifierObjet(Personne p) {
        System.out.println("   -> Début méthode : p.nom = " + p.getNom());
        
        // 1. Modification de l'ÉTAT interne de l'objet (via la référence copiée)
        p.nom = "Alice Modifiée"; 
        
        // 2. Tenter de réaffecter la RÉFÉRENCE copiée à un nouvel objet
        p = new Personne("Nouvelle Personne");
        
        System.out.println("   -> Après réaffectation LOCALE : p.nom = " + p.getNom());
    }


    public static void main(String[] args) {
        
        // --- CAS 1 : TYPE PRIMITIF (int) ---
        System.out.println("### 1. DÉMONSTRATION AVEC UN PRIMITIF (int) ###");
        int age = 10;
        System.out.println("AVANT l'appel : age = " + age);
        
        modifierPrimitif(age); 
        
        // L'original n'est pas affecté
        System.out.println("APRÈS l'appel : age = " + age); 
        
        System.out.println("\n--------------------------------------------\n");
        
        // --- CAS 2 : OBJET (Personne) ---
        System.out.println("### 2. DÉMONSTRATION AVEC UN OBJET (Personne) ###");
        Personne bob = new Personne("Bob");
        System.out.println("AVANT l'appel : bob.nom = " + bob.getNom());
        
        modifierObjet(bob);
        
        // La modification de l'état persiste, la réaffectation ne persiste pas
        System.out.println("APRÈS l'appel : bob.nom = " + bob.getNom());
    }
}
```

💡 Explication des Résultats

1. Cas du Primitif (int) : Passage par Valeur de la Valeur

    Résultat : AVANT l'appel : age = 10 et APRÈS l'appel : age = 10.

    Explication : Lorsque vous appelez modifierPrimitif(age), la valeur 10 est copiée dans la variable locale nombre de la méthode. Changer nombre à 99 modifie uniquement la copie, laissant la variable originale age intacte.

2. Cas de l'Objet (Personne) : Passage par Valeur de la Référence

    Résultat :

        AVANT l'appel : bob.nom = Bob

        APRÈS l'appel : bob.nom = Alice Modifiée