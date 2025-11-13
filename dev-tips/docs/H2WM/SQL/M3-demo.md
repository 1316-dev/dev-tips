---
sidebar_position: 4
---

```SQL
CREATE TABLE Clients(
	id_cli		NUMERIC(6)					CONSTRAINT PK_clients PRIMARY KEY,
	nom			VARCHAR(30)		NOT NULL,
	prenom		VARCHAR(30)		NULL,
	adresse		VARCHAR(120)	NULL,
	cpo			CHAR(5)			NOT NULL	CONSTRAINT CK_clients_cpo CHECK(cpo BETWEEN 1000 AND 95999), -- convertion implicite de Char en int
	ville		VARCHAR(80)		NOT NULL	CONSTRAINT DF_clients_ville DEFAULT 'Nantes'
);

CREATE TABLE Fiches(
	id_fic		NUMERIC(6)		IDENTITY(1001,1)
											CONSTRAINT PK_fiches PRIMARY KEY,
	id_cli		NUMERIC(6)		NULL,
	date_crea	DATETIME2		NOT NULL	CONSTRAINT DF_fiches_dateCrea DEFAULT GETDATE(),
	date_paye	DATETIME2		NULL,
	etat		CHAR(2)			NOT NULL	CONSTRAINT CK_fiches_etat CHECK(etat IN('EC', 'RE', 'SO')) 
											CONSTRAINT DF_fiches_etat DEFAULT 'EC',
-- on accepte qu'il n'y ai pas de date de paiement sinon elle doit être suppérieur à la date de creation
	-- CONTRAINTE QUI PORTE SUR 2 COLONNES DONC DOIT ETRE DECLARER EN CONTRAINTE DE TABLE
	CONSTRAINT CK_Fiches_dateCreaEtat CHECK ((date_paye IS NOT NULL AND etat = 'SO' AND date_paye > date_crea) OR (date_paye IS NULL AND etat <> 'SO'))
);

CREATE TABLE Modeles(
	id_modele	INT				IDENTITY	CONSTRAINT PK_modeles PRIMARY KEY,
	designation	VARCHAR(80)		NOT NULL,
	id_gam		CHAR(2)			NOT NULL,
	id_cate		CHAR(4)			NOT NULL
);

CREATE TABLE Articles(
	ref_art		CHAR(3)						CONSTRAINT PK_articles PRIMARY KEY,
	id_modele	INT				NOT NULL
);

CREATE TABLE Lignes_fic(
	id_fic		NUMERIC(6),
	no_lig		NUMERIC(2),
	ref_art		CHAR(3)			NOT NULL,
	date_depart	DATETIME2		NOT NULL	CONSTRAINT DF_lignesFic_depart DEFAULT GETDATE(),
	date_retour	DATETIME2		NULL,
	CONSTRAINT PK_lignesFic PRIMARY KEY(id_fic, no_lig),
	CONSTRAINT CK_LignesFic_dates CHECK (date_retour IS NULL OR date_retour > date_depart)
);

CREATE TABLE Gammes(
	id_gam		CHAR(2)						CONSTRAINT PK_gammes PRIMARY KEY,
	libelle		VARCHAR(30)		NOT NULL	CONSTRAINT UN_gammes_libelle UNIQUE
);

CREATE TABLE Categories(
	id_cate	CHAR(4)						CONSTRAINT PK_categories PRIMARY KEY,
	libelle		VARCHAR(30)		NOT NULL	CONSTRAINT UN_categories_libelle UNIQUE
);

CREATE TABLE Grille_tarifs(
	id_gam		CHAR(2),
	id_cate		CHAR(4),
	prix_jour	NUMERIC(5,2)	NOT NULL CONSTRAINT CK_GrilleTarif_prixJour CHECK (prix_jour > 0),
	CONSTRAINT PK_GrilleTarif_idGamIdCate PRIMARY KEY(id_gam, id_cate)

);



/****************************************************************************/
/*	SCRIPT DE CREATION DES TABLES DE LA BASE DE DONNEES Locations			*/
/*	Auteur : ENI Ecole														*/
/*	Date de création :														*/
/*	Version : 1.0															*/
/*	Objectif : Creation des contraintes d'intégrité référentielle et des	*/
/*	index																	*/		
/*	Modifications :															*/
/*	- ajout d’un index sur le nom et le prenom d'un client etendu à la		*/
/*	ville, pour accélérer les recherches et les tris						*/
/****************************************************************************/

-- 3. Creation des contrantes d'intégrité référentielle
ALTER TABLE Fiches
	ADD CONSTRAINT FK_Fiches_Clients FOREIGN KEY (id_cli) REFERENCES Clients(id_cli)
	ON DELETE SET NULL; -- tp mod3 / Attendu 2 / rond blanc 2 / tiret 1

ALTER TABLE Articles
	ADD CONSTRAINT FK_Articles_Modeles FOREIGN KEY (id_modele) REFERENCES Modeles(id_modele);

ALTER TABLE Lignes_fic
	ADD CONSTRAINT FK_LignesFic_Fiches FOREIGN KEY (id_fic) REFERENCES Fiches(id_fic)
	ON DELETE CASCADE;-- tp mod3 / Attendu 2 / rond blanc 2 / tiret 2,
	--CONSTRAINT FK_LignesFic_Articles FOREIGN KEY (ref_art) REFERENCES Articles(ref_art);

ALTER TABLE Lignes_fic
	ADD CONSTRAINT FK_LignesFic_Articles FOREIGN KEY (ref_art) REFERENCES Articles(ref_art)
	ON UPDATE CASCADE; -- tp mod3 / Attendu 2 / rond blanc 2 / tiret 3

ALTER TABLE Modeles
-- clé primaire à 2 colonnes donc appeler les deux dans les parenthèses
	ADD CONSTRAINT FK_Modeles_GrilleTarifs FOREIGN KEY(id_gam, id_cate) REFERENCES Grille_tarifs(id_gam, id_cate);

ALTER TABLE Grille_tarifs
	ADD CONSTRAINT FK_GrilleTarifs_Gammes FOREIGN KEY(id_gam) REFERENCES Gammes(id_gam),
	CONSTRAINT FK_GrilleTarifs_Categories FOREIGN KEY(id_cate) REFERENCES Categories(id_cate); 


-- 4.	L’ajout d’index pour accélérer les jointures
CREATE INDEX FK_Fiches_Clients ON Fiches(id_cli);
CREATE INDEX FK_LignesFic_Articles ON Lignes_fic(ref_art);
CREATE INDEX FK_LignesFic_Fiches ON Lignes_fic(id_fic);
CREATE INDEX FK_Articles_Modeles ON Articles(id_modele);

CREATE INDEX FK_Modeles_GrilleTarifs ON Modeles(id_gam, id_cate);
CREATE INDEX FK_GrilleTarifs_Gammes ON Grille_tarifs(id_gam);
CREATE INDEX FK_GrilleTarifs_Categories ON Grille_tarifs(id_cate);



/****************************************************************************/
/*	SCRIPT DE SUPPRESSION DES TABLES DE LA BASE DE DONNEES Locations		*/
/*	Auteur : ENI Ecole														*/
/*	Date de création :														*/
/*	Version : 1.0															*/
/*	Objectif : Suppression des contraintes d'intégrité référentielle puis	*/
/*	des tables																*/		
/*	Modifications :															*/
/****************************************************************************/

ALTER TABLE Fiches DROP CONSTRAINT FK_Fiches_Clients;
ALTER TABLE Lignes_fic DROP CONSTRAINT FK_LignesFic_Articles;
ALTER TABLE Lignes_fic DROP CONSTRAINT FK_LignesFic_Fiches;
ALTER TABLE Articles DROP CONSTRAINT FK_Articles_Modeles;

ALTER TABLE Modeles DROP CONSTRAINT FK_Modeles_GrilleTarifs;
ALTER TABLE Grille_tarifs DROP CONSTRAINT FK_GrilleTarifs_Gammes, FK_GrilleTarifs_Categories;
--ALTER TABLE Grille_tarifs DROP CONSTRAINT FK_GrilleTarifs_Categories;

DROP TABLE Lignes_fic, Fiches, Clients, Articles, Modeles, Grille_tarifs, Categories, Gammes;

```
