# Cours : Les boucles imbriquées en Python

**Sommaire**
- [1. Qu'est-ce qu'une boucle imbriquée ?](#1-quest-ce-quune-boucle-imbriquée-)
- [2. Double boucle `for` : principe](#2-double-boucle-for--principe)
- [3. Double boucle sur deux listes différentes](#3-double-boucle-sur-deux-listes-différentes)
- [4. Double boucle sur une même liste : deux indices](#4-double-boucle-sur-une-même-liste--deux-indices)
- [5. Ne parcourir que les couples avec j > i](#5-ne-parcourir-que-les-couples-avec-j--i)
- [6. Compter dans une boucle imbriquée](#6-compter-dans-une-boucle-imbriquée)
- [7. Variable sentinelle : le booléen](#7-variable-sentinelle--le-booléen)
- [8. Variable sentinelle : `None`](#8-variable-sentinelle--none)
- [9. Affichage ligne par ligne avec `print`](#9-affichage-ligne-par-ligne-avec-print)
- [10. Boucles à plus de deux niveaux](#10-boucles-à-plus-de-deux-niveaux)
- [11. Condition sur deux indices simultanément](#11-condition-sur-deux-indices-simultanément)
- [12. Affichage conditionnel caractère par caractère](#12-affichage-conditionnel-caractère-par-caractère)
- [13. Transformer une liste en réduisant sa taille](#13-transformer-une-liste-en-réduisant-sa-taille)

---

## 1. Qu'est-ce qu'une boucle imbriquée ?

Une boucle imbriquée, c'est une boucle placée **à l'intérieur** d'une autre boucle. À chaque tour de la boucle extérieure, la boucle intérieure s'exécute **en entier**.

Pour visualiser cela, imaginez que vous deviez citer toutes les cases d'un planning : pour chaque jour de la semaine (boucle extérieure), vous listez toutes les heures de la journée (boucle intérieure). Une fois la journée parcourue en entier, vous passez au jour suivant.

```python
jours = ["lundi", "mardi", "mercredi"]
heures = [8, 9, 10]

for jour in jours:
    for heure in heures:
        print(jour, heure, "h")
```

```txt
lundi 8 h
lundi 9 h
lundi 10 h
mardi 8 h
mardi 9 h
mardi 10 h
mercredi 8 h
mercredi 9 h
mercredi 10 h
```

> [!NOTE]
> `print` est appelé 3 × 3 = **9 fois**. En général, si la boucle extérieure tourne `n` fois et la boucle intérieure tourne `m` fois, le corps de la boucle intérieure s'exécute `n × m` fois.

---

## 2. Double boucle `for` : principe

Le cas le plus courant : deux boucles `for` sur des `range`. Voici comment suivre l'exécution pas à pas.

```python
for i in range(1, 4):
    for j in range(1, 4):
        print(i, j)
```

```txt
1 1
1 2
1 3
2 1
2 2
2 3
3 1
3 2
3 3
```

Pour bien comprendre l'ordre d'exécution, lisez le code de haut en bas en retenant cette règle : **chaque fois que `i` avance d'un cran, `j` repart de zéro et fait un tour complet**.

> [!TIP]
> Pour vérifier votre compréhension, demandez-vous : quelle est la première valeur affichée ? La dernière ? Combien de lignes y a-t-il en tout ?

**Compter le nombre d'itérations totales** est souvent utile pour estimer si un programme va être rapide ou lent. Ici, `i` prend 3 valeurs et `j` prend 3 valeurs : le corps de la boucle intérieure s'exécute $3 \times 3 = 9$ fois.

---

## 3. Double boucle sur deux listes différentes

On peut utiliser une double boucle pour explorer toutes les **combinaisons** entre les éléments de deux listes `L` et `M`.

**Exemple** : afficher tous les couples `(x, y)` où `x` est dans `L` et `y` est dans `M`.

```python
L = [1, 2, 3]
M = [10, 20]

for x in L:
    for y in M:
        print(x, y)
```

```txt
1 10
1 20
2 10
2 20
3 10
3 20
```

**Application** : vérifier si une liste contient au moins un élément en commun avec une autre (sans utiliser `in`).

```python
L = [7, 2, 5]
M = [1, 3, 4, 6]
commun = False

for x in L:
    for y in M:
        if x == y:
            commun = True

print(commun)   # False
```

Ici, pour chaque élément `x` de `L`, on parcourt toute la liste `M` pour voir si `x` y figure.

---

## 4. Double boucle sur une même liste : deux indices

On peut aussi faire une double boucle sur la **même liste**, en utilisant deux indices `i` et `j`. C'est utile quand on veut comparer des éléments entre eux.

**Exemple** : afficher tous les couples de valeurs `(L[i], L[j])` pour tous les couples d'indices possibles.

```python
L = [5, 11, 3]

for i in range(len(L)):
    for j in range(len(L)):
        print(L[i], L[j])
```

```txt
5 5
5 11
5 3
11 5
11 11
11 3
3 5
3 11
3 3
```

> [!NOTE]
> Avec cette approche, on voit le couple `(5, 11)` **et** le couple `(11, 5)`. On voit aussi chaque élément combiné avec lui-même : `(5, 5)`, `(11, 11)`, `(3, 3)`. Ce n'est pas toujours souhaitable — voir la section suivante pour l'éviter.

---

## 5. Ne parcourir que les couples avec j > i

Quand on cherche des **paires** dans une liste (comme des entiers opposés ou des inversions) sans vouloir les doublons ni les couples `(x, x)`, on démarre la boucle intérieure à `i + 1`.

```python
L = [5, 11, 3]

for i in range(len(L)):
    for j in range(i + 1, len(L)):
        print(i, j, "->", L[i], L[j])
```

```txt
0 1 -> 5 11
0 2 -> 5 3
1 2 -> 11 3
```

On obtient exactement les 3 paires sans répétition, et sans jamais comparer un élément avec lui-même.

> [!TIP]
> La clé est `range(i + 1, len(L))` : `j` commence toujours **après** `i`. Cela garantit que chaque paire d'indices `(i, j)` n'apparaît qu'une seule fois et que `i ≠ j`.

**Exemple** : afficher toutes les paires d'entiers dont la somme est positive.

```python
L = [-2, 5, -1, 4]

for i in range(len(L)):
    for j in range(i + 1, len(L)):
        if L[i] + L[j] > 0:
            print(L[i], "+", L[j], "=", L[i] + L[j])
```

```txt
-2 + 5 = 3
5 + -1 = 4
5 + 4 = 9
-1 + 4 = 3
```

---

## 6. Compter dans une boucle imbriquée

Un compteur initialisé avant la boucle intérieure permet de dénombrer des éléments selon un critère.

**Exemple** : compter combien de fois la valeur maximale d'une liste apparaît dans cette liste.

La stratégie : trouver d'abord le maximum, puis compter ses occurrences avec une boucle intérieure.

```python
L = [3, 7, 2, 7, 5, 1, 7]
maxi = L[0]
for x in L:
    if x > maxi:
        maxi = x

compteur = 0
for x in L:
    if x == maxi:
        compteur = compteur + 1

print(maxi, "apparaît", compteur, "fois")   # 7 apparaît 3 fois
```

Pour compter les occurrences de **toutes** les valeurs distinctes sans répétition, on peut utiliser le même principe avec une liste `dejaVus` pour mémoriser les valeurs déjà traitées :

```python
L = [4, 2, 4, 1, 2, 4]
dejaVus = []

for i in range(len(L)):
    if L[i] not in dejaVus:
        compteur = 1                           # L[i] lui-même compte pour 1
        for j in range(i + 1, len(L)):
            if L[j] == L[i]:
                compteur = compteur + 1
        dejaVus.append(L[i])
        print(L[i], ":", compteur)
```

```txt
4 : 3
2 : 2
1 : 1
```

> [!NOTE]
> Le compteur est initialisé à **1** (et non 0) car l'élément `L[i]` est déjà lui-même une occurrence. La boucle intérieure ne comptabilise que les occurrences supplémentaires aux indices `j > i`.

> [!TIP]
> La liste `dejaVus` sert à éviter d'afficher deux fois la même valeur : dès qu'une valeur a été traitée, on la mémorise pour ne pas la recompter.

---

## 7. Variable sentinelle : le booléen

Une **variable sentinelle** est une variable dont la valeur change quand une condition est rencontrée pendant la boucle. C'est le moyen standard pour répondre à la question « existe-t-il un élément qui vérifie… ? »

On l'initialise à `False` avant les boucles, puis on la passe à `True` si la condition est rencontrée.

**Exemple** : y a-t-il deux nombres, un dans `L` et un dans `M`, dont la somme vaut 42 ?

```python
L = [17, 22, 5, 33, 8]
M = [34, 8, 20]
somme42 = False

for x in L:
    for y in M:
        if x + y == 42:
            somme42 = True

print(somme42)   # True
```

On vérifie : 22 + 20 = 42 et 8 + 34 = 42.

> [!WARNING]
> Ne réinitialisez pas `somme42` à `False` à l'intérieur des boucles, sinon vous effaceriez une découverte précédente. La variable ne doit être initialisée qu'**une seule fois**, avant toutes les boucles.

Une fois les boucles terminées, on lit simplement la valeur de `somme42` : `True` si au moins une paire a été trouvée, `False` sinon.

---

## 8. Variable sentinelle : `None`

La valeur spéciale `None` signifie « rien », « pas encore trouvé ». Elle s'utilise comme sentinelle quand on veut soit renvoyer une valeur trouvée, soit indiquer qu'il n'y a rien eu.

On l'initialise à `None` avant les boucles, puis on lui affecte le résultat dès qu'on le trouve.

**Exemple** : trouver deux éléments opposés dans une liste (comme −3 et 3), et retenir leurs indices.

```python
L = [-2, 1, -3, 5, -7, -4, 5, -5, 3, -8]
opp = None

for i in range(len(L)):
    for j in range(i + 1, len(L)):
        if L[i] + L[j] == 0:
            opp = [i, j]

print(opp)   # [2, 8]
```

On vérifie : `L[2]` vaut −3 et `L[8]` vaut 3, leur somme est bien 0.

Si la liste ne contient aucune paire d'opposés, `opp` reste à `None` à la fin des boucles.

> [!NOTE]
> On teste `L[i] + L[j] == 0` plutôt que `L[i] == -L[j]` : les deux sont équivalents, mais la formulation avec la somme est souvent plus lisible.

**Tester si le résultat a été trouvé :**

```python
if opp is None:
    print("Pas d'éléments opposés")
else:
    print("Opposés aux indices", opp[0], "et", opp[1])
```

> [!TIP]
> Pour tester si une variable vaut `None`, on utilise `is None` (et non `== None`). C'est la convention Python.

---

## 9. Affichage ligne par ligne avec `print`

Pour afficher un motif sur plusieurs lignes (pyramide, triangle…), on combine la double boucle avec `print(..., end=" ")` pour rester sur la même ligne, et `print()` sans argument pour passer à la ligne suivante.

**Rappel :** par défaut, `print` termine toujours par un saut de ligne (`\n`). On peut changer cela avec `end`.

```python
print("a", end=" ")
print("b", end=" ")
print("c")
# Affiche : a b c
```

**Exemple** : afficher un triangle rectangle de `n = 4` lignes où la ligne `k` contient `k` fois le symbole `*`.

```python
n = 4

for k in range(1, n + 1):           # boucle extérieure : numéro de ligne
    for j in range(k):              # boucle intérieure : nombre d'éléments sur la ligne
        print("*", end=" ")
    print()                         # saut de ligne à la fin de chaque ligne
```

```txt
*
* *
* * *
* * * *
```

> [!TIP]
> Le `print()` seul, **après** la boucle intérieure et **dans** la boucle extérieure, est indispensable : c'est lui qui provoque le passage à la ligne entre deux lignes du motif. Sans lui, tout s'afficherait sur une seule ligne.

**Exemple avec un compteur externe** : afficher un carré de `n = 3` lignes où chaque case contient un numéro séquentiel, mais en partant du bas.

```python
n = 3
c = n * n   # compteur qui décrémente à chaque case affichée

for k in range(n):
    for j in range(n):
        print(c, end=" ")
        c = c - 1
    print()
```

```txt
9 8 7
6 5 4
3 2 1
```

Le compteur `c` est initialisé **avant** les deux boucles et se décrémente à l'intérieur de la boucle intérieure.

---

## 10. Boucles à plus de deux niveaux

On peut imbriquer autant de boucles que nécessaire. Trois, quatre niveaux, ou plus. Le principe reste identique : chaque boucle s'exécute en entier à chaque tour de la boucle qui la contient.

**Exemple** : afficher toutes les listes de 3 éléments formées d'éléments parmi 0 et 1.

```python
for a in range(2):
    for b in range(2):
        for c in range(2):
            print([a, b, c])
```

```txt
[0, 0, 0]
[0, 0, 1]
[0, 1, 0]
[0, 1, 1]
[1, 0, 0]
[1, 0, 1]
[1, 1, 0]
[1, 1, 1]
```

Il y a $2^3 = 8$ listes au total.

> [!NOTE]
> Le nombre total d'itérations du corps de la boucle la plus intérieure est le **produit** des longueurs de toutes les boucles. Avec 4 boucles parcourant chacune {0, 1, 2}, on obtient $3^4 = 81$ itérations.

> [!WARNING]
> Attention à l'indentation : chaque niveau d'imbrication ajoute **une tabulation** supplémentaire. Une indentation incorrecte changerait complètement le comportement du programme.

```python
# Correct : print à l'intérieur des 4 boucles
for a in range(3):
    for b in range(3):
        for c in range(3):
            for d in range(3):
                print([a, b, c, d])   # 81 lignes affichées
```

---

## 11. Condition sur deux indices simultanément

Dans une double boucle avec indices `i` (ligne) et `j` (colonne), on peut écrire des conditions qui portent **sur les deux indices à la fois**. C'est utile pour produire des motifs comme un damier ou des formes géométriques.

**Exemple** : afficher une grille `n × n` avec un motif alterné selon la **parité de `i + j`**.

```python
n = 4

for i in range(n):
    for j in range(n):
        if (i + j) % 2 == 0:
            print("#", end=" ")
        else:
            print(".", end=" ")
    print()
```

```txt
# . # .
. # . #
# . # .
. # . #
```

La clé : `(i + j) % 2` vaut 0 quand `i` et `j` ont la **même parité** (tous les deux pairs ou tous les deux impairs), et 1 sinon.

> [!TIP]
> Pour identifier la case à afficher différemment, posez-vous la question : quelle relation entre `i` et `j` caractérise cette case ? Parité alternée : `(i + j) % 2`. Diagonale descendante : `i == j`. Diagonale montante : `i + j == n - 1`.

On peut aussi combiner plusieurs conditions avec `or`. Par exemple, pour marquer la première et la dernière colonne :

```python
n = 4

for i in range(n):
    for j in range(n):
        if j == 0 or j == n - 1:
            print("|", end="")
        else:
            print(".", end="")
    print()
```

```txt
|..|
|..|
|..|
|..|
```

---

## 12. Affichage conditionnel caractère par caractère

Pour dessiner des formes géométriques en mode texte (triangles, bordures…), on affiche à chaque position `(i, j)` soit le caractère du motif, soit un espace, selon des conditions sur `i` et `j`.

La structure générale est toujours :

```python
for i in range(n):
    for j in range(...):
        if <condition pour afficher le caractère>:
            print(caractère, end="")
        else:
            print(" ", end="")
    print()
```

**Exemple** : rectangle creux de `n` lignes et `m` colonnes. Seul le contour est affiché avec `*`, l'intérieur est vide.

Les conditions pour qu'une case soit `*` :
- première ligne : `i == 0`
- dernière ligne : `i == n - 1`
- première colonne : `j == 0`
- dernière colonne : `j == m - 1`

```python
n = 4
m = 6

for i in range(n):
    for j in range(m):
        if i == 0 or i == n - 1 or j == 0 or j == m - 1:
            print("*", end="")
        else:
            print(" ", end="")
    print()
```

```txt
******
*    *
*    *
******
```

> [!NOTE]
> On parcourt ici une grille rectangulaire complète : la boucle intérieure va toujours de `0` à `m - 1`, quel que soit `i`.

> [!TIP]
> Avant d'écrire le code, listez les conditions qui font qu'une case est « sur le bord » : première ligne ? dernière ligne ? première colonne ? dernière colonne ? Ensuite, combinez ces conditions avec `or`.

---

## 13. Transformer une liste en réduisant sa taille

Certains algorithmes répètent une transformation sur une liste jusqu'à ce qu'il n'en reste qu'un élément. À chaque étape, on construit une **nouvelle liste** plus courte à partir de la liste courante, puis on remplace la liste courante par la nouvelle.

**Exemple** : à partir d'une liste, construire la liste des moyennes de termes successifs (arrondie à l'entier le plus proche).

```python
L = [10, 4, 8, 2]
nouvelle = []

for i in range(len(L) - 1):
    nouvelle.append((L[i] + L[i + 1]) // 2)

print(nouvelle)   # [7, 6, 5]
```

On parcourt les indices de `0` à `len(L) - 2` (inclus) pour pouvoir accéder à `L[i + 1]` sans dépasser la liste.

**Répéter jusqu'à un seul élément** : on place cette transformation dans une boucle extérieure qui tourne tant que la liste contient plus d'un élément.

```python
L = [10, 4, 8, 2, 6]

while len(L) > 1:
    nouvelle = []
    for i in range(len(L) - 1):
        nouvelle.append((L[i] + L[i + 1]) // 2)
    L = nouvelle   # on remplace L par la liste réduite

print(L)   # [6]
```

> [!NOTE]
> `L = nouvelle` remplace entièrement `L` par la nouvelle liste. Après cette ligne, `L` est plus courte d'un élément qu'avant la boucle intérieure.

> [!WARNING]
> Ne modifiez pas `L` pendant qu'on la parcourt : construisez toujours une liste `nouvelle` séparée, puis affectez `L = nouvelle` **après** la boucle intérieure.

---

## Récapitulatif des notions par exercice

| Exercice | Chapitres | Notions clés |
|---|---|---|
| 1. Pyramide croissante | §2, §9 | Double boucle `for`, `print(..., end=" ")`, `print()` |
| 2. Triangle lignes décroissantes | §2, §9 | Double boucle `for`, `print(..., end=" ")`, `print()` |
| 3. Motif carré et sa diagonale | §2, §11 | Double boucle avec indices, condition `j == i`, affichage conditionnel |
| 4. Damier de nombres | §2, §11 | Double boucle avec indices, condition sur `(i + j) % 2` |
| 5. Intersection de listes | §3 | Double boucle sur deux listes, `==`, `append` |
| 6. Triangle de Floyd | §9 | Double boucle `for`, compteur externe, `print(..., end=" ")` |
| 7. Afficher les effectifs | §6 | Double boucle avec `j > i`, compteur, liste `dejaVus` |
| 8. Triangle et son bord | §12 | Double boucle, affichage conditionnel `*` / espace, conditions sur `i` et `j` |
| 9. Différences successives | §13 | Boucle `while`, construction d'une nouvelle liste, `L[i] - L[i+1]` |
| 10. Écart minimal d'indices | §5, §8 | Double boucle avec `j > i`, variable sentinelle `None`, `abs(i - j)` |
