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

#### Question 1
		
```
																		+---+
																		| 4 |
																	+-------+
																	| 0000	|
																	|		|
																	| [...] |
																	| 		|
										+---+						| 0111  |
										| 4 |						---------
			+-------+-------+-------+-------+						| 1000  | ----> A
	A2		|  4    |   12  |   20  |   36  |						| [...]	|  
			+-------+-------+-------+-------+						| 1100	| ----> A3
										+---+						| [...] |
										| 4	|						| 1111  | ----> D
	A3 		+-------+-------+-------+-------+                       +-------+
			|  68   |       |       |       |
			+-------+-------+-------+-------+						Directory
```

A2 est complet ! On créé un nouveau bucket A3 qui prend en compte les 4 derniers bits de la clé, on ajoute donc un bit au Directory, qui considère maintenant les 4 derniers bits.  
L'ajout du 0 devant les bits 000 à 111 ne change rien en ce qui concerne les flèches reliant le directory aux buckets.  
En ce qui concerne l'ajout du 1 devant les bits de 000 à 111, on devra relier chacune de ces nouvelles valeurs aux buckets.  

#### Question 2

```


										+---+						
										| 3 |						
			+-------+-------+-------+-------+						
	B		|  1    |   17  |       |       |	<- 001					 
			+-------+-------+-------+-------+					
										+---+						
										| 3	|						
	B2 		+-------+-------+-------+-------+                     
			|  5    |  21   |  69   |       |	<- 101
			+-------+-------+-------+-------+					

```

Si on souhaite ajouter 17 et 69, ils se trouveront tous les deux dans le bucket B. Or, il reste une seule place dans ce dernier. On créé un nouveau bucket B2. On considère désormais les 3 derniers bits de la clé. On modifie la trajectoire des flèches entre le directory et les buckets.  

#### Question 3

Retirer la clé 21 n'a pas d'impact. les clés 001 et 101 ne pointeront pas sur un bucket vide. Il restera les clés 1 et 5.  

#### Question 4

Le bucket C sera vide si on enlève 10 mais on ne peut pas diminuer l'index du directory à 2.  
Sinon la clé OO pointerait vers le bucket A et le bucket A2. Un merge n'est donc pas possible.  

Exercice 3
----------

#### Question 1

Le hash index est une meilleure alternative que le heap file structure dans ce cas.  
Il faudrait parcourir en moyenne Nombre de pages / 2 en utlisant un heap file strcture.  
Ici le coût de la requête avec un hash index est de 1.  

```sql
SELECT 
FROM T
WHERE K = 50;
```

#### Question 2

On privilégie un hachage extensible à un hachage linéaire dans le cas de données mal équilibrées.  

#### Question 3

#### Question 4

On privilégie un hachage linéaire à un B+ Tree dans le cas où on cherche une clé précise.  
