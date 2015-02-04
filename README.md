# ABD-TP03
Administration de Bases de Données - TP 03


Exercice 1
----------

Le principe du static hash : 
Lorsqu'on recherche une clé, on connait son emplacement.


On a 100 000 enregistrements. 
Il y a 100 enregistrements par pages donc 1000 pages.

```sql
SELECT
FROM R;
```

1000.


```sql
SELECT
FROM R
WHERE K = 50;
```
Il y a une lecture puisqu'on cherche une clé et qu'on connait son emplacement.
Résultat : 1.


```sql
SELECT
FROM R
WHERE K BETWEEN 50 AND 100
```

Ils peuvent se trouver sur 1000 pages différentes.
En moyenne : 
Nombre de pages / 2 = 1000 / 2 = 500



```sql
SELECT
FROM R
WHERE K BETWEEN 50 AND 100
ORDER BY K;
```

Le ORDER BY ne change rien.
Ils peuvent se trouver sur 1000 pages différentes.
En moyenne : 
Nombre de pages / 2 = 1000 / 2 = 500



Exercice 1

