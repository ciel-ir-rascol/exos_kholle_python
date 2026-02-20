# Exercices sur les listes simples

## 1. Sommaire
- [1. Sommaire](#1-sommaire)
- [2. Liste : négatif -\> opposé](#2-liste--négatif---opposé)
- [3. Liste des carrés entre deux nombres](#3-liste-des-carrés-entre-deux-nombres)
- [4. Liste d’entiers consécutifs décroissants et alternant de signe](#4-liste-dentiers-consécutifs-décroissants-et-alternant-de-signe)
- [5. Séparer en indices pairs et indices impairs](#5-séparer-en-indices-pairs-et-indices-impairs)
- [6. Liste des entiers impairs suivi des pairs](#6-liste-des-entiers-impairs-suivi-des-pairs)
- [7. Rotation de liste](#7-rotation-de-liste)
- [8. Un, deux ou cinq](#8-un-deux-ou-cinq)
- [9. Inverser indices et valeurs dans une liste](#9-inverser-indices-et-valeurs-dans-une-liste)
- [10. Affichage en tas binaire (une seule boucle for)](#10-affichage-en-tas-binaire-une-seule-boucle-for)
- [11. Afficher toutes les dates de l’année](#11-afficher-toutes-les-dates-de-lannée)

## 2. Liste : négatif -> opposé
On donne une liste `L` d’entiers et on demande d’écrire un code qui modifie `L` en sorte que chaque élément `x` négatif de `L` est changé en son opposé `−x`. Par exemple, si `L = [42,-9, 81,-12,-65, 0, 46]` alors `L` doit être modifiée en la liste `[42, 9, 81, 12, 65, 0, 46]`
Exemple :
```python
a = 2035
b = 2025
L =[2035, -2034, 2033, -2032, 2031, -2030, 2029, -2028, 2027, -2026, 2025]
```

## 3. Liste des carrés entre deux nombres
On donne deux entiers positifs $a,b$ avec $a\leq b$. Créer,la liste croissante des carrés parfaits entre a et b.

Exemple :
```python
a=2000
b=3000
L=[2025, 2116, 2209, 2304, 2401, 2500, 2601, 2704, 2809]
```

> [!TIP]
> Afin de calculer la racine carrée vous pourrez utiliser la library `math`
> ```python 
> from math import sqrt
> sqrt(4) # Renvoi la racine carrée de 4
> ```
> Vous pouvez aussi utiliser la fonction `round` pour arrondir un résultat à l'unité
> ```python
> round(1.618) # Renvoi 2

## 4. Liste d’entiers consécutifs décroissants et alternant de signe
On donne deux entiers `a` et `b` avec $a\geq b\geq 0$, par exemple `a=2035` et `b=2025`. On demande de créer la liste des entiers consécutifs depuis `a` jusqu’à `b` en ordre décroissant et en alternant les signes, `a` devant apparaître positivement. 

## 5. Séparer en indices pairs et indices impairs
Soit une liste L. Séparer cette liste en deux listes distinctes :
- La liste IP des éléments de L d’indices pairs.
- La liste II des éléments de L d’indices impairs.

Exemple :
```python
L = [31, 12, 9, 65, 81, 42]
IP = [31, 9, 81]
II = [12, 65, 42]
```

## 6. Liste des entiers impairs suivi des pairs
On donne un entier $n\geq 1$ on demande d’écrire une liste `L` formée d’abord de tous les entiers
impairs entre 1 et n puis de tous les entiers pairs

Exemples:
```python
n=6
# Construire la liste L avec une boucle :
L = [1,3,5,2,4,6]
```
```python
n=5
# Construire la liste L avec une boucle :
L = [1,3,5,2,4]
```

## 7. Rotation de liste
Voici, sur un exemple, ce que l’on veut coder dans le cas général. On se donne une liste, par exemple :
```python
L = [17, 39, 61, 48, 42, 27, 75, 81, 64, 10]
```
et un indice k de cette liste, ici ce sera k=4 qui pointe vers l’élément 42. On souhaite effectuer une rotation des éléments dans la liste en sorte que l’élément à l’indice k soit désormais en début de liste. Donc ici, le contenu de L devra avoir changé et valoir :
```python
L = [42, 27, 75, 81, 64, 10, 17, 39, 61, 48]
```
Plus généralement, les éléments à partir de l’indice k se retrouvent en début de liste et le bloc des éléments d’indices initialement inférieurs à k se retrouve, dans le même ordre, en un bloc en fin de liste. **Bien noter qu’on ne demande pas de créer une nouvelle liste mais de modifier la liste initiale**.

> [!TIP]
> Vous pouvez utiliser des slices :
> ```python
> L = [1,2,3,4,5,6]
> L[:3] # Renvoi [1,2,3]
> L[2:] # Renvoi [3,4,5,6]
> ```
> Rappel :
> ```python
> A = [1,2,3]
> B = [4,5,6]
> C = A+B # C vaut [1,2,3,4,5,6]
> ```

## 8. Un, deux ou cinq
On considère la suite d’entiers suivante :
```text
1, 2, 5, 10, 20, 50, 100, 200, 500, ...
```
où les nombres se suivent par paquet de trois en rajoutant à chaque paquet un zéro terminal au paquet précédent. On donne un entier $n\geq 0$ et on demande de construire la liste des `n` premiers éléments de la suite. Par exemple, si `n = 7`, le code doit produire la liste :
```python
[1, 2, 5, 10, 20, 50, 100]
```

## 9. Inverser indices et valeurs dans une liste
On donne un entier $n\geq 0$ et on donne une liste `L` de `n` entiers qui contient une fois et une seule chaque entier entre `0 et n-1`. Par exemple, pour `n = 5`, on pourrait avoir :
```python
L = [1, 4, 0, 3, 2]
```
On demande de construire une nouvelle liste `M` de `n` entiers et dont l’élément à chaque indice `i` est l’indice de l’entier `i` dans la liste `L`. Avec l’exemple précédent :
```python
M = [2, 0, 4, 3, 1]
```
**Explication** : Par exemple,
- `M[2] = 4` car `L[4] = 2`.
- `M[1] = 0` car `L[0] = 1`.

La construction de `M` ne doit pas modifier la liste `L`. On commencera par créer, avec la méthode `append()` une liste `M` de `n` entiers valant tous `−1` puis on remplira convenablement la liste `M`.

## 10. Affichage en tas binaire (une seule boucle for)
Observez l’exemple suivant que l’on demande de coder dans toute sa généralité : on donne une liste `L` d’entiers telle que :
```python
[99, 28, 51, 76, 85, 52, 97, 97, 20, 78, 74, 34, 72, 75]
```
et on demande de l’afficher comme suit :
```text
99
28 51
76 85 52 97
97 20 78 74 34 72 75
```
La première ligne contient le premier élément, la 2e les deux éléments suivants, la 3e contient les 4 éléments suivants et ainsi de suite, chaque ligne (sauf éventuellement la dernière) contenant deux fois plus d’éléments que la précédente.
Il est attendu de **n’utiliser qu’une seule boucle `for`** parcourant les éléments de la liste `L`.

> [!TIP]
> - Maintenir un compteur pour chaque ligne mémorisant le nombre d’éléments de la ligne courante qui ont été affichés.<br>
> - Maintenir une variable indiquant la longueur finale de la ligne que l’on est en train d’afficher.<br>
> - Lorsqu’on arrive en fin de ligne, afficher un saut de ligne et réinitialiser le compteur.

## 11. Afficher toutes les dates de l’année
On vous demande d’afficher sur 365 lignes successives les dates de tous les jours de l’année.
Pour simplifier on suppose que **février est formé de 28 jours**. Par exemple, si le jour de l’An est
un vendredi, le code devra afficher :

```text
vendredi 1 janvier
samedi 2 janvier
dimanche 3 janvier
lundi 4 janvier
mardi 5 janvier
mercredi 6 janvier
....
....
vendredi 24 décembre
samedi 25 décembre
dimanche 26 décembre
lundi 27 décembre
mardi 28 décembre
mercredi 29 décembre
jeudi 30 décembre
vendredi 31 décembre
```

> [!NOTE]
> En 2026, le 1er jour de l'année était un jeudi.<br>
> Vous utiliserez 3 listes :
> - Une pour les noms des jours de la semaine.
> - Une pour les noms de mois.
> - Une contenant le nombre de jours des 12 mois de l'année.