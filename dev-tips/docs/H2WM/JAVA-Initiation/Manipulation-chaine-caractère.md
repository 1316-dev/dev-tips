---
sidebar_position: 7
---

# Manipulation chaine de caractère

```JAVA
import java.util.Scanner;

public class MainManipulationChaine {

	public static void main(String[] args) {

		/*
		 * Cr�ation d'un programme qui permettra de saisir une phrase puis de choisir : 
		 * (a) Remplacer tous les e de la phrase par des � 
		 * (b) Recherche la pr�sence d�un mot saisi dans la phrase 
		 * (c) Mettre en majuscule toute la phrase 
		 * Attention !!! : la phrase ne doit pas contenir de ponctuation
		 */

		// D�finir les ponctuations interdites
		char[] tabPonctuationInterdite = { '?', '.', ';', ':', '!', '/', ',', ',' };

		Scanner scan = new Scanner(System.in);

		System.out.println("Veuillez saisir une phrase (sans ponctuation) :");
		String phraseSaisie = scan.nextLine();
		phraseSaisie = verifierPonctuation(tabPonctuationInterdite, scan, phraseSaisie);

		// cr�ation d'une boucle sur l'affichage du menu au cas o� l'utilisateur ne tape
		// pas une proposition disponible
		String choix = "z";
		while (!(choix.equals("a")) && !(choix.equals("b")) && !(choix.equals("c"))) {
			System.out.println("Saisissez votre choix entre : ");
			System.out.println("(a) Remplacer tous les e de la phrase par des � ");
			System.out.println("(b) Recherche la pr�sence d�un mot saisi dans la phrase ");
			System.out.println("(c) Mettre en majuscule toute la phrase ");
			choix = scan.nextLine();
		}
		
		switch (choix) {

		case "a":
			String phraseModifiee = phraseSaisie.replace('e', '�');
			System.out.println(phraseModifiee);
			break;
		case "b":
			System.out.println("Quel mot recherchez vous ? : ");
			String motRecherche = scan.nextLine();
			String[] tabMots = phraseSaisie.split(" ");
			int compteur = 0;
			for (int ii = 0; ii < tabMots.length; ii++) {
				if (tabMots[ii].equalsIgnoreCase(motRecherche)) {
					compteur = compteur + 1;
				}
				continue;
			}
			if (compteur > 0) {
				System.out.println("Votre mot est pr�sent");
			} else
				System.out.println("Votre mot n'est pas pr�sent");

			break;
		case "c":
			System.out.println(phraseSaisie.toUpperCase());
			break;
		default:
			System.out.println("Merci de choisir un choix valide ");
		}
		
		scan.close();

	}

	// Convertion de la phrase dans un tableau de caract�re pour v�rifier la
	// pr�sence de ponctuation
	private static String verifierPonctuation(char[] tabPonctuationInterdite, Scanner scan, String phraseSaisie) {
		char[] tabPhrase = phraseSaisie.toCharArray();

		for (int ii = 0; ii < tabPonctuationInterdite.length; ii++) {
			for (int jj = 0; jj < tabPhrase.length; jj++) {
				if (tabPonctuationInterdite[ii] == tabPhrase[jj]) {
					System.out.println("Merci de ne pas mettre de ponctuation, entrez � nouveau votre phrase :");
					phraseSaisie = scan.nextLine();
					break;
				}
			}
		}

		System.out.println(phraseSaisie);
		return phraseSaisie;
	}
}
````