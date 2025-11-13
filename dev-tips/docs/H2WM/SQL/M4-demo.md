---
sidebar_position: 6
---

```SQL

---Insertion du Client 14
BEGIN TRAN tran_client14;
-- Clients
INSERT INTO Clients (id_cli,nom,prenom,adresse,cpo,ville)
VALUES (14,'Boutaud','Sabine','Rue des platanes',75002,'Paris');
-- Fiches
INSERT INTO Fiches (id_cli,date_crea,date_paye,etat)
VALUES (14,GETDATE()-15,GETDATE()-13,'SO');
-- Gammes
INSERT INTO Gammes (id_gam,libelle)
VALUES	('PR','Matériel Professionnel'),
		('HG','Haut de gamme'),
		('EG','Entrée de gamme');
-- Categories 
INSERT INTO Categories (id_cate,libelle)
VALUES	('FOA','ski de fond alternatif'),
		('FOP','ski de fon patineur');
-- Grilles tarifs
INSERT INTO Grille_tarifs (id_gam,id_cate,prix_jour)
VALUES	('EG','FOA',10),
		('HG','FOP',30),
		('PR','FOP',90);

-- Modèles
-- pour désactiver l'identity
SET IDENTITY_INSERT Modeles ON;
INSERT INTO Modeles (id_modele,designation,id_gam,id_cate)
VALUES	(1,'Fisher Cruiser','EG','FOA'),
		--('Fischer Sporty Crown','MG','FOA'),
		--('Fischer RCS Classic GOLD','PR','FOA'),
		(4,'Fischer SOSSkating VASA','HG','FOP'),
		(5,'Fischer RCS CARBOLITE Skating','PR','FOP');
		--('Décathlon Allegre junior 150','EG','PA'),
		--('Fischer mini ski patinette','MG','PA'),
		--('Décathlon Apparition','EG','SURF'),
		--('Salomon 24X+Z12','EG','SA'),
		--('Salomon Pro Link Equipe 4S','PR','SA'),
		--('Salomon 3V RACE JR+L10','PR','SA');

-- Pour réactiver l'identity
SET IDENTITY_INSERT Modeles OFF;

-- Articles

INSERT INTO Articles (ref_art,id_modele)
VALUES	('F05',1),
		('F50',4),
		('F60',5);
-- Lignes fic
INSERT INTO Lignes_fic (id_fic,no_lig,ref_art,date_depart,date_retour)
VALUES	(1001,1,'F05', GETDATE()-15,GETDATE()-13),
		(1001,2,'F50',DATEADD(DAY, -15, GETDATE()),DATEADD(DAY, -14, GETDATE())),
		(1001,3,'F60',DATEADD(DAY, -13, GETDATE()),DATEADD(HOUR, 6, DATEADD(DAY, -13, GETDATE())));
        -- autre écriture ('1001',3,'F60',GETDATE()-13,DATEADD(HH,6, GETDATE()-13));

-- PERMET D'AFFICHER UNE TABLE ENTIERE
SELECT * FROM Articles;
SELECT * FROM Categories;
SELECT * FROM Clients;
SELECT * FROM Fiches;
SELECT * FROM Gammes;
SELECT * FROM Grille_tarifs;
SELECT * FROM Lignes_fic;
SELECT * FROM Modeles;


-- à selectionner sans "--" pour exécuter

-- ROLLBACK TRAN tran_client14;

-- COMMIT TRAN tran_client14;

--réinitialiser l'identity de la tables fiches (ex avec un compeur démarrant à 1000)
DBCC CHECKIDENT ('Fiches', RESEED, 1000);
```