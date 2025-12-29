#  Détection de fraude bancaire

##  Cybersécurité financière & Machine Learning

###  Description du projet

Ce projet traite un problème critique de **cybersécurité financière** : la détection de transactions bancaires frauduleuses dans un environnement **fortement déséquilibré**, où moins de 0,2 % des transactions sont frauduleuses.

L’objectif principal n’est pas la précision globale, mais la **réduction des faux négatifs**, c’est-à-dire les fraudes non détectées, qui peuvent engendrer des pertes financières importantes.

Le projet repose sur le dataset **Credit Card Fraud Detection** (Kaggle) et explore plusieurs approches de détection d’anomalies et de classification supervisée.

###  Objectifs

* Détecter efficacement les transactions frauduleuses
* Atteindre :

  * **Recall > 90 %**
  * **ROC-AUC > 0.95**
* Comparer différentes approches :

  * Isolation Forest (non supervisée)
  * XGBoost (supervisée)
  * XGBoost avec SMOTE
* Optimiser le **seuil de décision**
* Analyser les erreurs (fraudes manquées)

###  Dataset

* **Nom** : Credit Card Fraud Detection
* **Source** : Kaggle
* **Taille** : 284 807 transactions
* **Fraudes** : 492 (≈ 0,17 %)
* **Features** :

  * `V1` à `V28` : variables anonymisées (PCA)
  * `Amount` : montant de la transaction
  * `Class` : variable cible

    * `0` : transaction légitime
    * `1` : fraude

📎 Lien Kaggle :
[https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud](https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud)


###  Méthodes utilisées

####  Prétraitement

* Normalisation de la variable `Amount` avec `StandardScaler`
* Séparation **train / test (80 % / 20 %)**
* Stratification pour conserver la proportion de fraudes

#### Modèles testés

* **Isolation Forest**

  * Détection d’anomalies non supervisée
* **XGBoost**

  * Gestion du déséquilibre avec `scale_pos_weight`
* **XGBoost + SMOTE**

  * Rééquilibrage artificiel de la classe minoritaire

####  Optimisation du seuil

* Utilisation de la **courbe Precision–Recall**
* Choix d’un seuil maximisant le rappel tout en limitant les faux positifs


###  Métriques d’évaluation

Les métriques suivantes ont été utilisées :

* Recall (prioritaire)
* Precision
* F1-score
* ROC-AUC
* Matrice de confusion
* Courbe ROC
* Courbe Precision–Recall

⚠️ **L’accuracy n’est pas utilisée comme métrique principale**, car elle est trompeuse dans un contexte déséquilibré.


###  Visualisations produites

* Répartition des classes (fraude / non fraude)
* Distribution des montants des transactions
* Boxplot : montants selon le type de transaction
* Courbe ROC
* Courbe Precision–Recall
* Matrices de confusion
* Comparaison des performances des modèles


###  Résultats principaux

| Modèle                               | Recall      | ROC-AUC    | Commentaire           |
| ------------------------------------ | ----------- | ---------- | --------------------- |
| Isolation Forest                     | Moyen       | Faible     | Trop de faux positifs |
| XGBoost (seuil 0.5)                  | Insuffisant | > 0.95     | Seuil non adapté      |
| XGBoost + seuil optimisé             | Élevé       | > 0.95     | Bon compromis         |
| **XGBoost + SMOTE + seuil optimisé** | **> 90 %**  | **> 0.95** | ✅ **Meilleur modèle** |


###  Analyse des erreurs

Les fraudes non détectées présentent souvent :

* Des **montants faibles**
* Des caractéristiques proches des transactions légitimes
* Un fort chevauchement dans l’espace des features

Cela met en évidence les limites des modèles purement statistiques et la nécessité de systèmes hybrides (règles métier + ML).


###  Exécution du projet (Google Colab)

1. Télécharger le dataset depuis Kaggle
2. Importer le fichier CSV dans Colab
3. Ouvrir le notebook
4. Exécuter les cellules dans l’ordre :

   * Chargement des données
   * Prétraitement
   * Entraînement des modèles
   * Évaluation et visualisations


###  Licence

Ce projet est réalisé dans un **cadre académique**.
Usage pédagogique uniquement
