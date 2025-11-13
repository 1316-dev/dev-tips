---
sidebar_position: 7
---

```SQL
-- Inner join permet de récupérer seulement les clients qui ont des commandes qui ont des détails qui ont des articles
SELECT nom,prenom,portable,Commandes.id_commande, date_cmd, statut, designation, quantite, prix_ht  FROM Clients
INNER JOIN Commandes ON Clients.id_client = Commandes.id_client
INNER JOIN Details_commandes ON Commandes.id_commande = Details_commandes.id_commande
INNER JOIN Articles ON Details_commandes.id_article = Articles.id_article
```
![alt text](img/m6-demo1.PNG)

```SQL
-- nombre d'articles commandés par client
SELECT Commandes.id_commande, nom,prenom,portable, SUM(quantite) quantite_article  FROM Clients
INNER JOIN Commandes ON Clients.id_client = Commandes.id_client
INNER JOIN Details_commandes ON Commandes.id_commande = Details_commandes.id_commande
INNER JOIN Articles ON Details_commandes.id_article = Articles.id_article
GROUP BY Commandes.id_commande, nom,prenom,portable
```

![alt text](img/m6-demo2.PNG)

```SQL
-- somme dépensée par client
SELECT nom,prenom,portable, SUM(quantite) quantite_article, SUM(quantite*prix_ht) total_ht  FROM Clients
INNER JOIN Commandes ON Clients.id_client = Commandes.id_client
INNER JOIN Details_commandes ON Commandes.id_commande = Details_commandes.id_commande
INNER JOIN Articles ON Details_commandes.id_article = Articles.id_article
GROUP BY nom,prenom,portable
```

![alt text](img/m6-demo3.PNG)