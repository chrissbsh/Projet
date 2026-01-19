Voici le contenu du document transcrit au format Markdown, structuré selon les sections originales.

# CentraleSupélec - PROJET SDP : Mention IA

**Encadrants :** K. Belahcène, V. Mousseau, M. Tydrichova, W. Ouerdane 

---

## 1. Prologue

Le concours de l'internat de médecine vient de se terminer. Les futurs médecins ont tous passé les examens du concours qui leur donnera accès aux spécialités de médecine. Dans ce concours très exigeant, les étudiants sont évalués dans différentes matières sur une échelle [0,100] et sont classés en fonction de leur moyenne pondérée.

En fonction de leurs souhaits et de leur rang de classement, ils choisiront l'une des spécialités. Chaque spécialité ayant un nombre de places fixé à l'avance, les futurs médecins choisissent leur spécialité dans l'ordre du classement. Le choix de chacun est donc contraint par le nombre de places et les choix des précédents.

### Données de l'exemple (Xavier et Yvonne)

| Candidat | Anatomie | Biologie | Chirurgie | Diagnostic | Epidemiologie | Forensic Pathology | Génétique |
| --- | --- | --- | --- | --- | --- | --- | --- |
| **Xavier** | 85 | 81 | 71 | 69 | 75 | 81 | 88 |
| **Yvonne** | 81 | 81 | 75 | 63 | 67 | 88 | 95 |
| **Poids** | 8 | 7 | 7 | 6 | 6 | 5 | 6 |
| <br><br><br> |  |  |  |  |  |  |  |

Les notes de Xavier et Yvonne ainsi que les poids des matières sont données dans le tableau ci-dessus, et le classement place Xavier avant Yvonne (la moyenne de Xavier étant supérieure à celle d'Yvonne, cf. équation 1).

*(Note : La formule ci-dessus illustre la comparaison des moyennes pondérées)* 

Yvonne souhaite comprendre pourquoi elle est moins bien classée que Xavier, et la seule explication qui lui est fournie par l'algorithme est le calcul de l'équation (1). La somme pondérée est souvent considérée comme interprétable. Cela signifie que, pour justifier l'affirmation , il serait suffisant de révéler la formule de somme pondérée ainsi que les valeurs précises des notes et des pondérations qui la composent, et laisser Yvonne effectuer le calcul.

Mais Yvonne ne s'en satisfait pas. Elle pourrait trouver plus clair qu'on formule le raisonnement suivant :  est meilleur que  car :

* L'avantage de  sur  en **Anatomie** pèse plus fort que son désavantage en **Chirurgie**.


* L'avantage de  en **Diagnostic** pèse plus fort que le désavantage en **Forensic Pathology**.


* L'avantage de  en **Epidémiologie** pèse plus fort que le désavantage en **Génétique**.


* x et y se valent en **Biologie**.



Une telle explication ne fait pas appel au calcul de somme pondérée, mais décompose l'affirmation  en arguments plus simples. C'est cette approche que l'on va adopter dans ce projet pour implémenter un algorithme qui calcule une explication de l'affirmation  à partir de ,  et du vecteur de poids.

---

## 2. Formulation du problème

Dans le calcul de somme pondérée, les cours  privilégient  par rapport à , tandis que les cours  sont en faveur de  (le cours B ne les différencie pas).

* Dans la justification de ,  constituent des **arguments pour** (pros).
*  constituent des **arguments contre** (cons).
* 
 est **neutre**.



La contribution des cours à la somme pondérée dans l'affirmation  est synthétisée dans le tableau ci-dessous. Une valeur strictement positive (négative, respectivement) correspond à un cours pour (contre, respectivement), et une valeur nulle à un cours neutre.

On note ,  et  ces ensembles de critères. Dans notre exemple, on a ,  et .

### Tableau des contributions 

| Cours | A | B | C | D | E | F | G |
| --- | --- | --- | --- | --- | --- | --- | --- |
| **Contribution** |  |  |  |  |  |  |  |
| <br><br><br> |  |  |  |  |  |  |  |

### Trade-off de type (1-1)

Dans la comparaison , un trade-off de type (1-1) correspond à une paire de cours  où  et  telle que la somme des contributions des cours  et  à la somme pondérée dans l'affirmation  est positive.

* Ainsi  est un trade-off de type (1-1) car , , et .


* Calculez  et . Pouvez-vous énumérer la liste de tous les trade-off de type (1-1) pour la comparaison  ?.



Une explication de type (1-1) de  est définie par l'ensemble  de trade-offs (1-1) disjoints tel que .
Dans l'exemple,  est une explication de type (1-1) de l'affirmation  (de longueur 3). Cette explication pourra être transcrite par le raisonnement énoncé dans le préambule.

> 
> **Question 1 :** Formuler un programme d'optimisation linéaire qui calcule une explication de type (1-1) de la comparaison  si elle existe, et retourne un certificat de non-existence dans le cas contraire. Implémentez cette formulation en utilisant un solveur d'optimisation.
> 
> 

### Extension aux autres candidats

On considère maintenant plus de candidats dont les notes sont reportées dans la table ci-dessous, et conduisent au classement suivant : .

| Candidat | A (8) | B (7) | C (7) | D (6) | E (6) | F (5) | G (6) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| **x** | 85 | 81 | 71 | 69 | 75 | 81 | 88 |
| **y** | 81 | 81 | 75 | 63 | 67 | 88 | 95 |
| **z** | 74 | 89 | 74 | 81 | 68 | 84 | 79 |
| **t** | 74 | 71 | 84 | 91 | 77 | 76 | 73 |
| **u** | 72 | 66 | 75 | 85 | 88 | 66 | 93 |
| **v** | 71 | 73 | 63 | 92 | 76 | 79 | 93 |
| **w** | 79 | 69 | 78 | 76 | 67 | 84 | 79 |
| **w'** | 57 | 76 | 81 | 76 | 82 | 86 | 77 |
| <br><br><br> |  |  |  |  |  |  |  |

### Trade-off de type (1-m)

Montrer par un argument simple qu'il n'existe pas d'explication de type (1-1) de la comparaison .

Pour étendre le langage d'explication on considère maintenant, dans l'affirmation , des trade-offs de type (1-m) () définis par une paire  où , et  telle que la somme des contributions des cours  à la somme pondérée dans l'affirmation  est positive.

* Par exemple,  est un trade-off de type (1-3) dans l'affirmation .



Une explication de type (1-m) de l'affirmation  est définie par l'ensemble  de trade-offs (1-m) disjoints tel que . Dans l'exemple ci-dessus,  est une explication de type (1-m) de l'affirmation  (de longueur 2).

> 
> **Question 2 :** Formuler un programme d'optimisation linéaire qui calcule une explication de type (1-m) de la comparaison  si elle existe, et retourne un certificat de non-existence dans le cas contraire. Implémentez cette formulation en utilisant un solveur d'optimisation.
> 
> 

Montrer qu'il n'existe pas d'explication de type (1-m) pour la comparaison .

### Trade-off de type (m-1)

On considère maintenant, dans l'affirmation , des trade-offs de type (m-1) () définis par une paire  où , et  telle que la somme des contributions des cours , et  à la somme pondérée dans l'affirmation  est positive.

* Par exemple,  est un trade-off de type (3-1) dans l'affirmation .



Une explication de type (m-1) de l'affirmation  est définie par l'ensemble  de trade-offs disjoints tel que . Dans l'exemple ci-dessus,  est une explication de type (3-1) de l'affirmation  (de longueur 2).

Trouver une explication de type (m-1) pour la comparaison .

> 
> **Question 3 :** Formuler un programme d'optimisation linéaire qui calcule une explication de type (m-1) de la comparaison  si elle existe, et retourne un certificat de non-existence dans le cas contraire. Implémentez cette formulation en utilisant un solveur d'optimisation.
> 
> 

### Combinaison des types

Montrer que pour la comparaison , il n'existe aucune explication de type (m-1), ni de type (1-m). Montrer qu'il existe une explication combinant des trade-offs de type (m-1) et (1-m) pour cette comparaison.

> 
> **Question 4 :** Formuler un programme d'optimisation linéaire qui calcule une explication incluant des trade-offs de type (1-m) ou (m-1) de la comparaison  si elle existe, et retourne un certificat de non-existence dans le cas contraire. Implémentez cette formulation en utilisant un solveur d'optimisation.
> 
> 

Les notes de deux candidats supplémentaires au concours viennent d'arriver et sont fournies dans la table ci-dessous. Saurez-vous expliquer à  qu'il est moins bien classé que  avec une explication de type (1-m) ou (m-1) ?.

| Candidat | A | B | C | D | E | F | G |
| --- | --- | --- | --- | --- | --- | --- | --- |
| **** | 89 | 74 | 81 | 68 | 84 | 79 | 77 |
| **** | 71 | 84 | 91 | 79 | 78 | 73,5 | 77 |
| <br><br><br> |  |  |  |  |  |  |  |

---

## 3. Travail demandé et organisation du projet

Une fois les éléments ci-dessus mis en place, il vous est demandé une mise en œuvre sur un jeu de données réel traité par régression logistique (vous pouvez utiliser le jeu de données ci-dessous, ou un autre de votre choix):

* Le jeu de données original est disponible sur UCI Machine Learning repository (Wolberg et al., 1993).


* Lien : `https://archive.ics.uci.edu/dataset/15/breast+cancer+wisconsin+original`
* Ce jeu de données (nettoyé) a déjà été utilisé à des fins d'évaluation comparative dans Ustun et Rudin (2016) et est disponible à l'adresse : `https://github.com/ustunb/miplib2017-slim/tree/master/models/data`.



### Organisation

* Le projet doit être réalisé en groupe de trois étudiants.


* Deux séances de cours seront consacrées à ce projet (**15/12/2025** et **19/01/2026**).


* La présence de tous aux deux séances projet est obligatoire et sera contrôlée.


* La participation active aux deux séances projet fait partie intégrante de l'évaluation du projet.



### Rendus

* A l'issue de la séance du **15/12/2025**, un rendu intermédiaire est demandé, et devra être déposé dans l'espace Edunao du cours.


* Pour le rendu intermédiaire, l'attendu est que la **Question 1** (au minimum) devra être traitée.


* Les soutenances sont planifiées le **03/02/2026**. Lors de la soutenance, la présence et la participation de chacun des membres du trinôme est requise.