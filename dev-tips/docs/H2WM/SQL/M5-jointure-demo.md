---
sidebar_position: 9
---

# DEMO JOINTURE et ORDER

> Tous les clients

```SQL
SELECT * FROM Clients
```

![alt text](img/M5-D2-1.PNG)

> Les clients avec une commande

```SQL
SELECT * FROM Clients
INNER JOIN Commandes ON Clients.id_client = Commandes.id_client
```

![alt text](img/M5-D2-2.PNG)

> Tous les clients et leurs commmande et ceux sans commande

```SQL
SELECT * FROM Clients
LEFT JOIN Commandes ON Clients.id_client = Commandes.id_client
```

![alt text](img/M5-D2-3.PNG)

> Les clients n'ayant pas de commande

```SQL
SELECT * FROM Clients
LEFT JOIN Commandes ON Clients.id_client = Commandes.id_client
WHERE id_commande IS NULL
```

![alt text](img/M5-D2-4.PNG)

> Trier par nom

```SQL
SELECT * FROM Clients
LEFT JOIN Commandes ON Clients.id_client = Commandes.id_client
WHERE id_commande IS NULL
ORDER BY nom
```

![alt text](img/M5-D2-5.PNG)

> Trier par nom inversé

```SQL
SELECT * FROM Clients
LEFT JOIN Commandes ON Clients.id_client = Commandes.id_client
WHERE id_commande IS NULL
ORDER BY nom DESC
```

![alt text](img/M5-D2-6.PNG)