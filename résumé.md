Voici un résumé complet du document "Projet SDP 2025-26" de CentraleSupélec (Mention IA).

### 1. Contexte et Objectif du Projet

Le projet porte sur l'**explicabilité des décisions algorithmiques**, spécifiquement dans le cadre d'un classement par **somme pondérée**.

* 
**Le Scénario :** Un concours d'internat de médecine où les candidats sont classés selon leurs notes dans différentes matières et des poids associés.


* 
**Le Problème :** Une candidate (Yvonne) est moins bien classée qu'un autre (Xavier) et ne se satisfait pas de la simple formule mathématique de la moyenne pondérée comme explication.


* **L'Objectif :** Développer un algorithme capable de générer une explication intelligible sous forme d'arguments logiques (trade-offs) plutôt que par un calcul arithmétique. L'idée est de dire : "L'avantage de X sur Y dans la matière A pèse plus lourd que son désavantage dans la matière B".



### 2. Formalisation du Problème

La comparaison entre deux candidats ( et  avec ) est décomposée en trois ensembles :

* 
**Pros() :** Matières où  est meilleur que  (arguments pour).


* 
**Cons() :** Matières où  est meilleur que  (arguments contre).


* 
**Contribution :** La différence de score pondérée pour chaque matière.



Le but est de trouver un ensemble de **Trade-offs** (compromis) disjoints qui couvrent tous les éléments de l'ensemble *Cons* (tous les désavantages).

### 3. Étapes et Travail Demandé (Questions)

Le projet demande de formuler des programmes d'**optimisation linéaire** pour trouver ces explications, avec une complexité croissante :

* **Question 1 : Explication de type (1-1)**
* Un critère "Pro" compense exactement un critère "Con".


* Tâche : Formuler et implémenter le programme linéaire pour trouver ces paires. Si impossible, fournir un certificat de non-existence.




* **Question 2 : Explication de type (1-m)**
* Un seul critère "Pro" très fort compense plusieurs critères "Cons" ().


* Tâche : Implémentation et démonstration sur les candidats  et .




* **Question 3 : Explication de type (m-1)**
* Plusieurs critères "Pros" sont nécessaires pour compenser un seul critère "Con".


* Tâche : Implémentation et application à la comparaison .




* **Question 4 : Explication Mixte**
* Combinaison de trade-offs de type (1-m) et (m-1) pour les cas complexes où un seul type ne suffit pas (exemple donné : ).


* Application finale sur deux nouveaux candidats  et .





### 4. Application sur Données Réelles

Après la mise en œuvre théorique, les étudiants doivent appliquer leur méthode sur un jeu de données réel :

* Données : **Breast Cancer Wisconsin** (disponible sur UCI Machine Learning repository).


* Méthode : Utiliser les poids issus d'une régression logistique pour générer les explications.



### 5. Organisation et Logistique

* 
**Groupe :** Trinômes (3 étudiants).


* **Calendrier :**
* Séance 1 : 15/12/2025 (Rendu intermédiaire sur la Question 1 attendu à l'issue).


* Séance 2 : 19/01/2026.


* Soutenances : 03/02/2026.




* 
**Évaluation :** Basée sur la participation active, le rendu intermédiaire et la soutenance finale.