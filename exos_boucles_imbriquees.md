# Exercices sur les boucles imbriquées

**Sommaire**
- [1. Pyramide croissante de nombre](#1-pyramide-croissante-de-nombre)
- [2. Triangle : lignes consécutives décroissantes](#2-triangle--lignes-consécutives-décroissantes)
- [3. Motif carré et sa diagonale](#3-motif-carré-et-sa-diagonale)
- [4. Damier de nombre](#4-damier-de-nombre)
- [5. Intersection de listes](#5-intersection-de-listes)
- [6. Triangle de Floyd](#6-triangle-de-floyd)
- [7. Afficher les effectifs d'une liste d'entiers](#7-afficher-les-effectifs-dune-liste-dentiers)
- [8. Triangle et son bord](#8-triangle-et-son-bord)
- [9. Différences successives](#9-différences-successives)
- [10. Écart minimal d'indices (boucles imbriquées)](#10-écart-minimal-dindices-boucles-imbriquées)

## 1. Pyramide croissante de nombre
On vous donne un entier `n > 0` et on vous demande de construire le motif formé de `n` lignes de la manière suivante :

- la 1re ligne contient le nombre 1 écrit une seule fois,
- la 2e ligne contient le nombre 2 écrit 2 fois,
- la 3e ligne contient le nombre 3 écrit 3 fois,
- et ainsi de suite jusqu'à avoir écrit `n` lignes.

Sur une même ligne, deux nombres seront séparés par un espace. Exemple pour `n = 6` :

```
1
2 2
3 3 3
4 4 4 4
5 5 5 5 5
6 6 6 6 6 6
```

## 2. Triangle : lignes consécutives décroissantes
Écrire un code qui, à partir d'un entier `n`, affiche le motif suivant (exemple pour `n = 6`) :

```
1
2 1
3 2 1
4 3 2 1
5 4 3 2 1
6 5 4 3 2 1
```

- il y a `n` lignes,
- chaque ligne contient un nombre de plus que la précédente,
- la `k`-ième ligne affiche tous les entiers en décroissant de `k` à 1.

## 3. Motif carré et sa diagonale
Étant donné un entier naturel `n >= 1`, construire un carré de côté `n` respectant les deux contraintes suivantes :

- la diagonale descendante est constituée du chiffre 0,
- les autres cases du carré sont constituées du chiffre 1.

Exemple pour `n = 10` :

```
0 1 1 1 1 1 1 1 1 1
1 0 1 1 1 1 1 1 1 1
1 1 0 1 1 1 1 1 1 1
...
1 1 1 1 1 1 1 1 1 0
```

Deux chiffres côte à côte sont séparés par un espace.

## 4. Damier de nombre
Réaliser un programme qui affiche un damier de forme carrée, de côté de longueur `n > 0`, rempli alternativement du nombre 4 et du nombre 2. La case en haut à gauche sera toujours 4. Par exemple, pour `n = 7` :

```
4242424
2424242
4242424
2424242
4242424
2424242
4242424
```

On remarquera que tous les 4 de la grille sont aux cases dont les indices de ligne et de colonne ont toujours la même parité.

## 5. Intersection de listes
On donne deux listes `L` et `M` chacune formée d'entiers distincts. Écrire une liste `inter` valant la liste des éléments communs aux deux listes. Voici quelques exemples :

```
L = [8, 9, 3, 5]  M = [1, 2, 3, 4, 6, 8, 9]  ->  [8, 9, 3]
L = [8, 9, 2, 4]  M = [8, 4, 7]               ->  [8, 4]
L = [6]           M = [1, 2, 5]               ->  []
```

## 6. Triangle de Floyd
**Question 1.** Le triangle de Floyd à `n` lignes est obtenu en plaçant sur `n` lignes successives, dans l'ordre croissant, les entiers consécutifs à partir de 1, la ligne numéro `k` comportant exactement `k` entiers. Écrire un code qui affiche le triangle de Floyd à `n` lignes. Exemple pour `n = 5` :

```
1
2 3
4 5 6
7 8 9 10
11 12 13 14 15
```

**Question 2.** Écrire un code qui, à partir d'un entier `N`, construit une liste `[ligne, colonne]` donnant la position de `N` dans le triangle de Floyd. Exemple : `N = 13` → `[5, 3]` ; `N = 4` → `[3, 1]`.

## 7. Afficher les effectifs d'une liste d'entiers
On donne une liste `L` d'entiers. Afficher le nombre de fois que les différents nombres de la liste `L` apparaissent dans `L`. L'ordre d'affichage respecte l'ordre d'apparition dans la liste, sans répétition. Exemple pour `L = [81, 31, 81, 12, 81, 9, 12, 65]` :

```
81 : 3
31 : 1
12 : 2
9 : 1
65 : 1
```

On utilisera une liste `dejaVus` pour ne pas traiter deux fois le même élément.

## 8. Triangle et son bord
On donne un entier `n >= 1`. Dessiner en mode texte un triangle de côté `n`. Exemple pour `n = 9` :

```
*
**
* *
*  *
*   *
*    *
*     *
*      *
*********
```

L'intérieur du triangle est creux (caractère espace). De haut en bas, le nombre d'espaces va en augmentant de 1. Bien vérifier le résultat pour `n` valant 1, 2 ou 3.

## 9. Différences successives
On donne une liste `L` d'entiers. On réduit `L` à un unique élément par le procédé suivant : à chaque étape, on constitue une nouvelle liste dont les éléments sont la différence de deux éléments successifs de `L`. On recommence jusqu'à n'avoir plus qu'un élément. Calculer cet unique élément.

Exemple : `L = [9, 5, 6, 3, 6, 2, 6]` → `[4, -1, 3, -3, 4, -4]` → ... → `[93]`.

## 10. Écart minimal d'indices (boucles imbriquées)
On donne une liste `L` d'entiers. Déterminer l'écart minimal d'indices où se trouveraient des valeurs identiques. Si la liste ne contient que des valeurs différentes, renvoyer 0. On utilisera deux boucles for imbriquées.

Exemple : `L = [16, 14, 17, 13, 15, 14, 16, 15, 13, 14, 16, 15, 13, 16]` → écart minimal = 3 (par exemple 15 apparaît aux indices 4 et 7).