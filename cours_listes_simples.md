# Cours : Les listes en Python

**Sommaire**
- [1. Qu'est-ce qu'une liste ?](#1-quest-ce-quune-liste-)
- [2. Créer une liste](#2-créer-une-liste)
- [3. Accéder aux éléments : indices](#3-accéder-aux-éléments--indices)
- [4. Modifier un élément](#4-modifier-un-élément)
- [5. Longueur d'une liste : `len`](#5-longueur-dune-liste--len)
- [6. Parcourir une liste avec `for`](#6-parcourir-une-liste-avec-for)
- [7. Ajouter des éléments : `append`](#7-ajouter-des-éléments--append)
- [8. Tester l'appartenance : `in`](#8-tester-lappartenance--in)
- [9. Slices : extraire une partie de liste](#9-slices--extraire-une-partie-de-liste)
- [10. Concaténer deux listes : `+`](#10-concaténer-deux-listes--)
- [11. Modifier une liste en place](#11-modifier-une-liste-en-place)
- [12. La bibliothèque `math`](#12-la-bibliothèque-math)
- [13. Afficher proprement avec `print`](#13-afficher-proprement-avec-print)
- [14. Insérer un élément à un indice donné : `insert`](#14-insérer-un-élément-à-un-indice-donné--insert)
- [15. Supprimer un élément d'une liste](#15-supprimer-un-élément-dune-liste)

---

## 1. Qu'est-ce qu'une liste ?

Une liste est une suite ordonnée d'éléments. Ces éléments peuvent être des entiers, des flottants, des chaînes de caractères, etc.

```python
L = [42, -9, 81, 0, 46]      # liste d'entiers
mois = ["janvier", "février", "mars"]  # liste de chaînes
jours = [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31]
```

---

## 2. Créer une liste

### Liste vide

On crée souvent une liste vide que l'on remplira ensuite élément par élément :

```python
L = []
```

### Liste par énumération

On liste directement les éléments entre crochets, séparés par des virgules :

```python
L = [1, 2, 5, 10, 20]
```

### Liste par `range`

Pour créer une liste des entiers de `a` à `b - 1` :

```python
L = list(range(5))       # [0, 1, 2, 3, 4]
L = list(range(1, 6))    # [1, 2, 3, 4, 5]
L = list(range(10, 0, -1))  # [10, 9, 8, 7, 6, 5, 4, 3, 2, 1]
```

---

## 3. Accéder aux éléments : indices

Les éléments d'une liste sont numérotés à partir de **0**. On accède à l'élément d'indice `i` avec `L[i]`.

```python
L = [17, 39, 61, 48, 42]
L[0]   # 17  (premier élément)
L[1]   # 39
L[4]   # 42  (cinquième élément)
```

On peut aussi utiliser des **indices négatifs** pour compter depuis la fin :

```python
L[-1]  # 42  (dernier élément)
L[-2]  # 48  (avant-dernier)
```

> [!WARNING]
> Accéder à un indice qui n'existe pas provoque une erreur `IndexError`. Si `L` a 5 éléments, les indices valides sont 0, 1, 2, 3, 4 (et -1, -2, -3, -4, -5).

---

## 4. Modifier un élément

On modifie un élément en lui affectant une nouvelle valeur via son indice :

```python
L = [42, -9, 81, -12, 0]
L[1] = 9      # L vaut maintenant [42, 9, 81, -12, 0]
L[3] = 12     # L vaut maintenant [42, 9, 81, 12, 0]
```

C'est ainsi que l'on peut **modifier une liste en place**, sans en créer une nouvelle.

---

## 5. Longueur d'une liste : `len`

`len(L)` renvoie le nombre d'éléments de la liste `L` :

```python
L = [31, 12, 9, 65, 81, 42]
len(L)   # 6
```

Les indices valides vont donc de `0` à `len(L) - 1`.

---

## 6. Parcourir une liste avec `for`

### Parcours par valeur

La façon la plus simple : on récupère directement chaque élément.

```python
L = [31, 12, 9, 65]
for x in L:
    print(x)
# Affiche : 31, puis 12, puis 9, puis 65
```

### Parcours par indice

Quand on a besoin de connaître la position de l'élément dans la liste :

```python
L = [31, 12, 9, 65]
for i in range(len(L)):
    print(i, L[i])
# Affiche : 0 31, puis 1 12, puis 2 9, puis 3 65
```

> [!TIP]
> Utilisez le parcours par indice quand vous devez **modifier** les éléments de la liste, ou quand la position de l'élément compte (indices pairs/impairs, etc.).

### Tester la parité d'un indice

L'opérateur modulo `%` donne le reste de la division entière. `i % 2 == 0` est vrai si `i` est pair.

```python
L = [31, 12, 9, 65, 81, 42]
for i in range(len(L)):
    if i % 2 == 0:
        print(L[i])   # affiche les éléments d'indices pairs : 31, 9, 81
```

---

## 7. Ajouter des éléments : `append`

`L.append(x)` ajoute l'élément `x` à la **fin** de la liste `L`. C'est la méthode de base pour construire une liste progressivement.

```python
L = []
L.append(10)   # L vaut [10]
L.append(20)   # L vaut [10, 20]
L.append(30)   # L vaut [10, 20, 30]
```

**Exemple** : construire la liste des carrés de 1 à 5 :

```python
carres = []
for i in range(1, 6):
    carres.append(i * i)
# carres vaut [1, 4, 9, 16, 25]
```

---

## 8. Tester l'appartenance : `in`

`x in L` renvoie `True` si `x` est dans la liste `L`, `False` sinon :

```python
L = [10, 20, 30, 42]
20 in L    # True
99 in L    # False
```

On peut aussi tester la non-appartenance avec `not in` :

```python
99 not in L   # True
```

---

## 9. Slices : extraire une partie de liste

Un *slice* (tranche) permet d'extraire une sous-liste sans modifier l'originale.

```python
L = [17, 39, 61, 48, 42, 27, 75]
L[2:]    # [61, 48, 42, 27, 75]  — du rang 2 jusqu'à la fin
L[:4]    # [17, 39, 61, 48]      — du début jusqu'au rang 3 (exclu : 4)
L[2:5]   # [61, 48, 42]          — du rang 2 au rang 4 (exclu : 5)
```

La syntaxe générale est `L[début:fin]` où `fin` est **exclu**.

> [!NOTE]
> `L[k:]` désigne tous les éléments à partir de l'indice `k` et `L[:k]` désigne tous les éléments avant l'indice `k`. Ces deux slices sont complémentaires : ensemble ils reconstituent toute la liste.

---

## 10. Concaténer deux listes : `+`

L'opérateur `+` entre deux listes crée une **nouvelle** liste en mettant bout à bout les deux listes :

```python
A = [1, 2, 3]
B = [4, 5, 6]
C = A + B   # C vaut [1, 2, 3, 4, 5, 6]
```

On peut combiner slices et concaténation pour réorganiser une liste :

```python
L = [17, 39, 61, 48, 42, 27, 75]
k = 4
nouvelle = L[k:] + L[:k]
# nouvelle vaut [42, 27, 75, 17, 39, 61, 48]
```

Pour **modifier la liste en place** (sans en créer une nouvelle), on peut réaffecter le contenu :

```python
L = [17, 39, 61, 48, 42, 27, 75]
k = 4
L[:] = L[k:] + L[:k]
# L vaut maintenant [42, 27, 75, 17, 39, 61, 48]
```

---

## 11. Modifier une liste en place

Certains exercices demandent de modifier la liste `L` elle-même (sans en créer une nouvelle). On le fait soit élément par élément, soit en réaffectant via `L[:]` :

```python
# Modifier élément par élément
L = [42, -9, 81, -12, -65, 0, 46]
for i in range(len(L)):
    if L[i] < 0:
        L[i] = -L[i]
# L vaut [42, 9, 81, 12, 65, 0, 46]
```

```python
# Réaffecter le contenu avec L[:] = ...
L = [17, 39, 61, 48, 42]
L[:] = L[2:] + L[:2]
# L vaut [61, 48, 42, 17, 39]
```

> [!WARNING]
> `L = L[2:] + L[:2]` crée une **nouvelle** liste et fait pointer `L` vers elle. `L[:] = L[2:] + L[:2]` modifie le contenu de la liste existante. La différence est importante si d'autres variables pointent vers la même liste.

---

## 12. La bibliothèque `math`

Pour certains calculs mathématiques, on importe des fonctions de la bibliothèque `math` :

```python
from math import sqrt, floor, ceil

sqrt(9)      # 3.0  — racine carrée (renvoie un flottant)
sqrt(2025)   # 45.0

floor(3.7)   # 3    — arrondi à l'entier inférieur
ceil(3.2)    # 4    — arrondi à l'entier supérieur
round(3.5)   # 4    — arrondi à l'entier le plus proche
```

**Exemple** : trouver le plus petit entier dont le carré est ≥ `a` :

```python
from math import sqrt, ceil
a = 2000
n = ceil(sqrt(a))   # n = 45 car 44² = 1936 < 2000 et 45² = 2025 ≥ 2000
```

---

## 13. Afficher proprement avec `print`

### Afficher plusieurs valeurs sur une même ligne

```python
print("bonjour", "monde")     # bonjour monde
print(1, 2, 3)                # 1 2 3  (séparés par des espaces par défaut)
```

On peut choisir le séparateur avec `sep` :

```python
print(1, 2, 3, sep="-")       # 1-2-3
print(1, 2, 3, sep="")        # 123
```

### Ne pas sauter de ligne avec `end`

Par défaut `print` termine par un saut de ligne (`\n`). On peut changer cela :

```python
print("vendredi", end=" ")
print(1, end=" ")
print("janvier")
# Affiche : vendredi 1 janvier
```

### Afficher le contenu d'une liste avec des espaces

```python
L = [99, 28, 51]
for x in L:
    print(x, end=" ")
print()   # saut de ligne final
# Affiche : 99 28 51
```

### Construire une chaîne de caractères

On peut aussi construire une chaîne puis l'afficher d'un coup :

```python
jour = "jeudi"
numero = 1
mois = "janvier"
print(jour + " " + str(numero) + " " + mois)
# Affiche : jeudi 1 janvier
```

Ou plus lisiblement avec une f-string :

```python
print(f"{jour} {numero} {mois}")
# Affiche : jeudi 1 janvier
```

---

## 14. Insérer un élément à un indice donné : `insert`

`L.insert(i, x)` insère l'élément `x` **avant** l'élément d'indice `i`. Tous les éléments à partir de l'indice `i` sont décalés d'une position vers la droite.

```python
L = [10, 20, 30, 40]
L.insert(2, 99)   # insère 99 avant l'indice 2
# L vaut [10, 20, 99, 30, 40]
```

Cas particuliers :

```python
L = [10, 20, 30]
L.insert(0, 99)         # insère en début de liste → [99, 10, 20, 30]
L.insert(len(L), 99)    # insère en fin de liste   → [10, 20, 30, 99]
                        # (équivalent à L.append(99))
```

> [!NOTE]
> Si `i` est supérieur ou égal à `len(L)`, l'élément est simplement ajouté en fin de liste, sans erreur.

---

## 15. Supprimer un élément d'une liste

Il existe plusieurs façons de supprimer un élément, selon que l'on connaît sa **valeur** ou son **indice**.

### Supprimer par valeur : `remove`

`L.remove(x)` supprime la **première occurrence** de la valeur `x` dans `L`.

```python
L = [10, 20, 30, 20, 40]
L.remove(20)   # supprime le premier 20
# L vaut [10, 30, 20, 40]
```

> [!WARNING]
> Si la valeur `x` n'est pas dans la liste, `remove` lève une erreur `ValueError`. On peut se prémunir avec un test `if x in L` avant d'appeler `remove`.

### Supprimer par indice : `pop`

`L.pop(i)` supprime l'élément à l'indice `i` et le **renvoie**.

```python
L = [10, 20, 30, 40]
x = L.pop(1)   # supprime L[1] = 20 et le renvoie
# x vaut 20, L vaut [10, 30, 40]
```

Sans argument, `pop()` supprime et renvoie le **dernier** élément :

```python
L = [10, 20, 30, 40]
x = L.pop()    # supprime et renvoie 40
# x vaut 40, L vaut [10, 20, 30]
```

### Supprimer par indice : `del`

`del L[i]` supprime l'élément à l'indice `i` sans le renvoyer.

```python
L = [10, 20, 30, 40]
del L[2]   # supprime L[2] = 30
# L vaut [10, 20, 40]
```

On peut aussi supprimer une tranche entière :

```python
L = [10, 20, 30, 40, 50]
del L[1:3]   # supprime les éléments aux indices 1 et 2
# L vaut [10, 40, 50]
```

### Récapitulatif

| Méthode | Critère | Renvoie la valeur ? |
|---|---|---|
| `L.remove(x)` | par valeur (première occurrence) | non |
| `L.pop(i)` | par indice | oui |
| `del L[i]` | par indice | non |

---

## Récapitulatif des notions par exercice

| Exercice | Notions clés |
|---|---|
| 1. Négatif → opposé | Parcours par indice, modification en place, `if` |
| 2. Carrés entre deux nombres | `append`, `sqrt`, `ceil`, boucle `for` |
| 3. Consécutifs décroissants alternant de signe | `append`, compteur de signe, boucle `for` décroissante |
| 4. Séparer en indices pairs/impairs | Parcours par indice, `% 2`, `append` |
| 5. Impairs puis pairs | Deux boucles `for`, `append`, `% 2` |
| 6. Rotation de liste | Slices, concaténation `+`, modification en place `L[:]` |
| 7. Un, deux ou cinq | `append`, compteur de position `% 3`, `//` ou `*` |
| 8. Inverser indices et valeurs | `append`, parcours par indice, lecture et écriture dans deux listes |
| 9. Affichage en tas binaire | Compteur, variable de longueur de ligne, `print(..., end=...)` |
| 10. Dates de l'année | Trois listes, double compteur, boucles imbriquées simples |
