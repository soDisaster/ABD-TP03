ABD - TP 03
===========

Auteurs
-------

- BERNARD Thomas
- SAINT-OMER Anne-Sophie

Exercice 1
----------

Données :  

Relation R(K,A,B,C) avec :  
- K : clé primaire, avec valeurs entières dans l'intervalle (1, 100000)  

Relation mémorisée avec une structure hash statique (static hash) sur la clé K en pages de taille Dp = 1024o.
Nombre d'enregistrements (record) sur le disque Ne = 100000  
Taille d'un enregistrement (record) Lr = 100o  
Nombre de pages nécessaires = (Ne * Lr) / Dp = (100000 * 100) / 1024 = 9 766

Le principe du static hash : 
Lorsqu'on recherche une clé, on connait son emplacement.

On a 100 000 enregistrements. 
Il y a 100 enregistrements par pages donc 1000 pages.

#### Expression 1

```sql
SELECT *
FROM R;
```

Cout de l'expression : 9 766

#### Expression 2

```sql
SELECT *
FROM R
WHERE K = 50;
```

Il y a une lecture puisqu'on cherche une clé et qu'on connait son emplacement.
Cout de l'expression : 1

#### Expression 3

```sql
SELECT *
FROM R
WHERE K BETWEEN 50 AND 100
```

Ils peuvent se trouver sur 9 766 pages différentes.
En moyenne : 
Nombre de pages / 2 = 9 766 / 2 = 4 883

#### Expression 4

```sql
SELECT *
FROM R
WHERE K BETWEEN 50 AND 100
ORDER BY K;
```

Le ORDER BY ne change rien.
Ils peuvent se trouver sur 9 766 pages différentes.
En moyenne : 
Nombre de pages / 2 = 9 766 / 2 = 4 883

Exercice 2
----------

Exercice 3
----------
