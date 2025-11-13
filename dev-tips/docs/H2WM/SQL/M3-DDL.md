---
sidebar_position: 3
---

# Le langage de requête SQL avec SQL Server

Clé étrangères sont très importantes = jointure

## DDL : La gestion de la structure de la base de données

Voir l'image pour commencer avec management SQL

![alt text](img/demo-sql-management.png)

![alt text](img/demo-numeroligne.PNG)

### La Création des tables - CREATE TABLE

On termine la requête par un ";"
![alt text](img/create-table.PNG)

```SQL
CREATE TABLE clients(
-- nom de colonnes Types,
id_client INT,
nom VARCHAR(50),
prenom VARCHAR (40),
date_naissance DATE,
ville VARCHAR(50),
portable NUMERIC(10),
fixe NUMERIC(10)
);
```

### Convention d'écriture

Les mots clés SQL en majuscules (ex : CREATE TABLE)
Nom des tables au pluriel et en snake_case (ex : Conges_mens)
Nom des colonnes explicites, en minuscule et snale_case(ex : date_modif)
Règles de nommages cohérentes

### Les types de données pour SQL Server

1. Cractère
![alt text](img/char.PNG)
On utilise surtout CHAR et VARCHAR

2. Numériques
![alt text](img/numerique.PNG)
On privilégie le NUMERIC au FLOAT

3. Date
![alt text](img/date.png)

4. Autres
![alt text](img/autres-donnes.png)

Ce sont les types propriéaire du SGBT de SQL SErver

on utilise pas les standards de la norme pour des questions de perfs.

Pour info :
![alt text](img/synonyme.PNG)

attention : dernière ligne inversée

### Mise en oeuvre de l'intégrité des données

Objectifs:

- Assurer la cohérence des données
- Appliquer les règles de fonctionnement issues de l'analyse
- Tradutcion des règles du modèle relationnel

Mise en oeuvre

- Attribut requis (NULL = pas OBLIGATOIRE /NOT NULL =  OBLIGARTOIRE)
- Contrainte (CONSTRAINT)
- Déclencheur de base de données (TRIGGER)

CONTRAINTE :

Syntaxe : CONSTRAINT NOM (typeDeContrainte_nomTable[_compementInfos]) TYPE de contrainte

Si une contrainte fait intervenir 2 colonnes alors c'est une contrainte de tables

exemple :

```SQL
CONSTRAINT PK_Clients PRIMARY KEY
```

![alt text](img/contrainte.PNG)

![alt text](img/type-contrainte.png)

Ces trois mots-clés SQL sont des **contraintes fondamentales**
pour l'intégrité et la cohérence des données

PRIMARY KEY pour clé primaire  | **Unicité**  
UNIQUE pour une clé secondaire | **Unicité**  
CHECK pour vérifier/tester (définit une condition) | **Restreint le Domaine des Valeurs**  
DEFAULT 'mettre valeur par défault'

![alt text](img/contrainte-type.PNG)

Exemple :

```SQL
--------demo 1------------
CREATE TABLE Clients(
-- nom de colonnes Types,
	-- Clé Primaire
	id_client		INT	NOT NULL CONSTRAINT PK_Clients PRIMARY KEY,
	nom				VARCHAR(50)	NOT NULL,
	prenom			VARCHAR (40) NULL,
	-- Contrainte d'âge: assure que la personne est née (date antérieure à la date actuelle)
	date_naissance	DATE NULL CONSTRAINT CK_Clients_dateNaissance CHECK (date_naissance < GETDATE()),
	-- Valeur par défaut si non spécifiée
	ville			VARCHAR(50) NOT NULL DEFAULT 'Nantes',
	-- Clé secondaire
	portable		NUMERIC(10) NULL CONSTRAINT UN_Clients_portable UNIQUE,
	fixe			NUMERIC(10) NULL,
	-- Contrainte d'unicité composite (Clé Secondaire)
	CONSTRAINT UN_Clients_nomPrenomDateNaissance UNIQUE (nom,prenom,date_naissance),
	-- Contrainte CHECK : au moins un téléphone doit être renseigné
	CONSTRAINT CK_Clients_telephone CHECK (portable IS NOT NULL OR fixe IS NOT NULL)
);
```

L'intégrité référentiel :

Grâce au Clé étrangère

Définition

![alt text](img/foreign-key.png)

Exemple

![alt text](img/foreign-key-exemple.png)

### MODIFICATION DE TABLE - ALTER TABLE

- Ajouter une Colonne

 ```SQL
ALTER TABLE Articles ADD descritpion VARCHAR(100) NOT NULL;
```

- Modifier une colonne

```SQL
ALTER TABLE Articles ALTER COLUMN descritpion VARCHAR(500) NULL;
```

- Supprimer une colonne

```SQL
ALTER TABLE Articles DROP COLUMN descritpion;
```

### MODIFICATION DES CONTRAINTES - ALTER TABLE

Sera bien adaptée pour les clées étrangères

- Ajouter une Contrainte

 ```SQL
ALTER TABLE Articles 
WITH NOCHECK
ADD CONSTRAINT FK_Articles_Categories
    FOREIGN KEY (ide_categorie);
```

- Supprimer une Contrainte

```SQL
ALTER TABLE Clients DROP CONSTRAINT UN_Clients_portable;
```

- Activer/Désactiver un contrainte (ne s'applique qu'aux contraintes de clés étrangère et de valisation) **PAS UNE BONNE PRATIQUE**

```SQL
ALTER TABLE Articles NOCHECK CONSTRAINT ALL;
```

démo 1 :

```SQL
--------demo 1----------------------------------------------
-- Module 3 : La gestion de la structure de base de données
-- INDIQUE LA BASE DE DONNEES SUR LAQUELLE S'EXECUTE LE SCRIPT
Use GesCom
GO 

CREATE SEQUENCE SQ_Clients AS INT START WITH 15 INCREMENT BY 5.

CREATE TABLE Clients(
-- nom de colonnes Types,
	-- Clé Primaire
	id_client		INT	NOT NULL CONSTRAINT PK_Clients PRIMARY KEY
								 CONSTRAINT DF_Clients_idClient DEFAULT NEXT VALUE FOR SQ_Clients,
	nom				VARCHAR(50)	NOT NULL,
	prenom			VARCHAR (40) NULL,
	-- Contrainte d'âge: assure que la personne est née (date antérieure à la date actuelle)
	date_naissance	DATE NULL CONSTRAINT CK_Clients_dateNaissance CHECK (date_naissance < GETDATE()),
	-- Valeur par défaut si non spécifiée
	ville			VARCHAR(50) NOT NULL DEFAULT 'Nantes',
	-- Clé secondaire
	portable		NUMERIC(10) NULL CONSTRAINT UN_Clients_portable UNIQUE,
	fixe			NUMERIC(10) NULL,
	-- Contrainte d'unicité composite (Clé Secondaire)
	CONSTRAINT UN_Clients_nomPrenomDateNaissance UNIQUE (nom,prenom,date_naissance),
	-- Contrainte CHECK : au moins un téléphone doit être renseigné
	CONSTRAINT CK_Clients_telephone CHECK (portable IS NOT NULL OR fixe IS NOT NULL)
);

CREATE TABLE Commandes(
	-- Clé Primaire
	id_commande INT NOT NULL CONSTRAINT PK_Commandes PRIMARY KEY,
	-- Contrainte date de commande inférieur ou égale à la date du jour
	date_cmd	DATETIME2(7) NOT NULL CONSTRAINT CK_Commandes_dates CHECK (date_cmd<=GETDATE()),
	-- Constrainte sur des valeurs autorisées AP,EP,PR,AC,LI,EL
	statut		CHAR(2) NOT NULL CONSTRAINT CK_Commandes_statut CHECK (statut IN ('AP', 'EP', 'PR', 'AC')), 
	id_Client	INT NOT NULL
);

CREATE TABLE Details_commandes(
	id_commande		INT NOT NULL,
	numero_ligne	INT NOT NULL,
	id_article		INT NOT NULL,
	-- Clé Primaire sur deux colonnes
	CONSTRAINT PK_Details_commandes PRIMARY KEY (id_commande,numero_ligne)
);

CREATE TABLE Articles(
	-- Clé Primaire
	id_article	INT NOT NULL CONSTRAINT PK_Articles PRIMARY KEY IDENTITY,
	-- Clé secondaire
	designation VARCHAR(50) NOT NULL CONSTRAINT UN_Article_designation UNIQUE,
	prix_ht		NUMERIC(8,2) NOT NULL,
	prix_ttc	AS prix_ht*1.2
);

CREATE TABLE Categories (
	-- Clé Primaire
	id_categorie	INT  CONSTRAINT PK_Categorie PRIMARY KEY IDENTITY,
	libelle			VARCHAR(50)  NOT NULL,
	id_cat_parent	INT  NULL
)
```

```SQL
ALTER TABLE Commandes
	ADD CONSTRAINT FK_Commandes_Clients FOREIGN KEY (id_client) REFERENCES Clients(id_client)
	-- les commandes du client seront automatiquement supprimées lors de la suppression du client
	ON DELETE CASCADE;

ALTER TABLE Details_commandes
	ADD CONSTRAINT FK_DetailsCommandes_Commandes FOREIGN KEY (id_commande) REFERENCES Commandes(id_commande);

ALTER TABLE Details_commandes
	ADD CONSTRAINT FK_DetailsCommandes_Articles FOREIGN KEY (id_article) REFERENCES Articles(id_article);

ALTER TABLE Articles
	ADD id_categorie INT NULL;

ALTER TABLE Articles
	ADD CONSTRAINT FK_Articles_Categories FOREIGN KEY (id_categorie) REFERENCES Categories(id_categorie);

ALTER TABLE Categories
	ADD CONSTRAINT FK_Categories_Categories FOREIGN KEY (id_cat_parent) REFERENCES Categories(id_categorie);

ALTER TABLE Details_commandes
	ADD quantite INT NOT NULL DEFAULT (1);

```

Diagramme généré

![alt text](img/generer-diagramme.PNG)

### Les Valeurs auto-incrémentées

- Identity existe que sur SQL server
  - Génère des valeurs entières
  - Associé à une colonne d'une table
  - Pas nécessairement mais généralement sur la clé primaire
  - 1 seul par table
  - Peut produire des trous dans la numérotation
  - Désactivable/réactivable

![alt text](img/identity.PNG)

- Séquence existe sur tous
  - Génère des valeurs entières
  - Compteur défini indépendamment de toute table
  - Peut être utiliser pour générer des valeurs pour autre chose qu'une colonne

CREATION D'UNE SEQUENCE  

![alt text](img/sequence.png)

UTILISATION D'UNE SEQUENCE

![alt text](img/sequence-utilisation.PNG)

### Les index

Obj : Accéder plus rapidement à l'information  

Par principe **on place des index sur les foreignkey** : jointure

**Pour les performances** il est préférable d'avoir **moins d'index** que trop d'index

- Päs sur des index créés automatiquement  
  - Clés primaires (index organisé et unique)
  - Clés secondaires (index non-organisé et unique)
- Sur les attributs utilisés pour  
  - Des jointures (clés étrangères)
  - Des restrictions
  - Des regroupements
  - Des tris

```SQL
-- on place des index sur les foreign key
CREATE INDEX IN_Commmandes_idClient ON Commandes(id_client);
CREATE INDEX IN_DetailsCommmandes_idCommandes ON Details_commandes(id_commande);
CREATE INDEX IN_DetailsCommmandes_idArticle ON Details_commandes(id_article);
CREATE INDEX IN_Categories_idCatParent ON Categories(id_cat_parent);
CREATE INDEX IN_Articles_idCateorie ON Articles(id_categorie);
```

