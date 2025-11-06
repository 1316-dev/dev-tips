---
sidebar_position: 1
---
# Revision JAVA

site pour plus d'informations : https://gayerie.dev/epsi-b3-java/langage_java/introduction.html

## Static et Final

Le mot-clé static signifie que la valeur est identique pour toutes les instances de la classe.  
Final signifie que la variable ne peut pas changer.

## Primitifs :
- float
- boolean
- double
- int



- Déclaration de tableau
- Refractor (création de methodes)
```JAVA
public class Main {
    public static void main(String[] args) {
        // déclarer un tableau avec les ventes de la semaine
        double salesLea[] = {50, 600, 15, 150, 75, 300, 12};
        double salesJules [] = {20, 30, 12, 10, 75, 50, 12};

        // affficher la longueur du tableau
        System.out.println(salesLea.length);

        //afficher le tableau des ventes
        display(salesLea, "Léa");
        display(salesLea, "Jules");


        //calculer total et moyenne
        totalAndAverage(salesLea, "Léa");
        totalAndAverage(salesJules, "Jules");


        // trouver la meilleure des vente
        bestSale(salesLea, "Léa");
        bestSale(salesJules, "Jules");
    }

    private static void display(double[] sales, String name) {
        // affficher chaque valeur du tableau
        System.out.println(name + " : ");
        for (int index = 0; index < sales.length; index++) {
            System.out.print(sales[index] + "€,");
        }
        System.out.println();
    }

    private static void totalAndAverage(double[] sales,String name) {
        // calculer le total des ventes de la semaines
        double total = 0;

        for (int daySales = 0; daySales < sales.length; daySales++) {
            total = total + sales[daySales];
        }
        // calculer la moyenne des ventes on met un double pour forcer à avoir un double pendant le calcul
        double average = total / sales.length;
        System.out.printf("Average sales "+ name + " : " + "%.2f%n",average);
    }

    public static void bestSale(double[] sales, String name) {
        double maxSale = sales[0];
        int maxDay = 0;

        for (int day = 0; day < sales.length; day++) {
            if (sales[day] > maxSale) {
                maxSale = sales[day];
                maxDay = day;
            }
        }
        String dayStr = "";
        switch (maxDay) {
            case 0 : dayStr = "monday"; break;
            case 1 : dayStr = "tuesday"; break;
            case 2 : dayStr = "wednesday"; break;
            case 3 : dayStr = "thursday"; break;
            case 4 : dayStr = "friday"; break;
            case 5 : dayStr = "saturday"; break;
            case 6 : dayStr = "sunday"; break;


        }
        System.out.println("Best Sale " + name + " : " + maxSale + " on " + dayStr );
    }
}

```