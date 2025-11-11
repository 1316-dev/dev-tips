---
sidebar_position: 2
---

# Le langage de requête SQL avec SQL Server

## Le langage SQL

Langage informatique permettant de communiquer avec le SGBDR

SQL est une mise en oeuvre des concepts du modèle relationnel

Langage à base de requêtes : Norme SQL

Il fait :

- l'administration de la base = l'administrateur
- la gestion des structures = le concepteur
- la gestion du contenu = le developpeur

Il ne fait pas :

- la présentaiton des résultats
- la gestion des erreurs

### Le transact SQL

Chaque SGBD aura sa surcouche prore

Surcouche procédural au langage SQL

Ajoute : Conditionnelles, Boucles, Variables, Procédure, Fonctions...

### Historique

Langage stable qui n'evolue pas souvent

![alt text](img/historique.png)

### Les trois catégories d'instructions

#### DDL

Le DDL est utilisé par **le concepteur ou l'administrateur** pour créer, modifier et supprimer les objets de la base de données (tables, vues, index, etc.).

Data DEfinition Language :

- CREATE : créer objet
- ALTER : mettre à jour objet
- DROP : supprimer objet

#### DML

Le DML est le langage le plus utilisé par **le développeur**. Il permet de manipuler les données stockées dans les tables.

- Data Manipulation Language :
- INSERT : enregistrer données
- UPDATE : mettre à jour données
- DELETE : supprimer données
- SELECT : selctionner données

#### DCL

Le DCL, bien que souvent regroupé avec le DML, gère l'intégrité des données via les transactions. C'est fondamental pour garantir que les opérations DML (INSERT, UPDATE, DELETE) sont exécutées de manière atomique et cohérente.

Data Control Language :

- BEGIN TRAN
- COMMIT TRAN
- SAVE TRAN
- ROLLBACK TRAN
- GRANT

### SQL Server Management Studio

Un environnement intégré permettant de gérer toute infrastructure SQL

![alt text](img/sql-management-studio.PNG)