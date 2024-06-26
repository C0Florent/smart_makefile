# Smart Makefile

Solution de compilation intelligente pour C/C++

---

Aujourd'hui, je vais vous présenter un système de Makefile intelligent qui recompile les fichiers sources C/C++ quand les fichiers d'en-tête dont ils dépendents sont modifiés.

## 1- Exemple simple

Pour comprendre l'intérêt de ce système de Makefile, voici un cas où un Makefile plus simple ne fonctionne pas comme on le voudrait.

Imaginons un projet:
```log
$ tree
.
├── defs.h
├── long.c
├── main.c
└── Makefile
```

main.c:
```c
#include "defs.h"

int main(void)
{
    return MY_RETURN_VALUE;
}
```

defs.h:
```c
#ifndef MY_DEFS
    #define MY_DEFS

    #define MY_RETURN_VALUE 7

#endif /* MY_DEFS */
```

long.c est un gros fichier dont la compilation dure longtemps, il est préférable de ne pas le recompiler inutilement.

Comme on peut le voir, main.c inclut defs.h, pourtant, avec un Makefile simpliste tel que celui utilisé dans cet exemple, main.c ne sera pas recompilé si defs.h est modifié.

## 2- Pourquoi ce résultat ?

### Regardons le Makefile de ce projet

### Qu'est-ce qui fait qu'une règle est relancée ou non par `make` ?

#### Mise au point sur le vocabulaire utilisé

- Voir le [lexique en annexe](#make)

#### Lancement récursif des règles, fonctionnement par date de dernière modification

### Donc au final, comment fonctionne ce Makefile ? Pourquoi le compilation n'est-elle pas relancée ?

- Explication des fonctionnalités de `make` mises en jeu dans ce genre de Makefile

## 3- Quelles solutions avons-nous à notre disposition ?

### Décrire manuellement les dépendances de chaque source

- Démonstration de l'ajout explicite des dépendances de chaque fichier

### Différents éléments qui permettraient d'automatiser ce processus

#### Demander un coup de main au compilateur pour relever les dépendances

- `$ man gcc` `/-M` -> Présentations des options `-M` qui permettent de demander au compilateur de générer des fichiers de dépendances

#### Manipulation des règles `make` qui sont utilisées pour compiler les sources

- Redéfinition des règles implicites qui servent à compiler les .o
- Suppression de ces mêmes règles implicites
- Inclusion de Makefiles dans d'autres

## 4- Comment assembler ces solutions pour former un système de Makefile qui recompile les sources quand les en-têtes sont modifiés ?

- Démonstration en live de la construction du Makefile qui combine les éléments présentés précédemment.

## 5- Améliorations possibles

- Placement des fichiers .d dans un dossier séparé
- Recréation de .d seulement que le fichier source est modifié

## 6- Pour quels projets utiliser cette solution ?

Pour tous vos projets en C ou C++, compilés avec gcc ou clang, où vous aimeriez ne pas avoir besoin de recompiler votre projet entier à chaque fois que vous modifiez un .h/.hpp.
Donc, à ma connaissance, à peu près n'importe quel projet où vous voulez souvent lancer des compilations, et où elles peuvent durer longtemps.

*Ça pourrait servir pour le zappy*

## Lexique

### make

Entre parenthèses sont indiqués les noms utilisés dans [la documentation de make](https://www.gnu.org/software/make/manual/make.html).

- Règle (*rule*) : partie d'un Makefile qui décrit comment construire un fichier en particulier
- Modèle de règle (*pattern rule*) : Règle généralisée à partir d'un motif commun à différents noms de fichiers
- Cible (*target*) : nom du fichier qu'une règle vise à produire
- Prérequis (*prerequisite*) : Fichier dont une règle dépend (par exemple : .c pour fabriquer un .o)
- Recette (*recipe*) : liste de commandes qui définit comment une règle construit sa cible à partir des prérequis
