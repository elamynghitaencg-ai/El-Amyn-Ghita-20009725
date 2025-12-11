COMPTE RENDU DU PROJET — DÉTECTION DU CANCER DU SEIN
1. Introduction

Le cancer du sein constitue l’une des principales causes de mortalité chez les femmes dans le monde. La détection précoce joue un rôle déterminant dans l’amélioration du pronostic et des chances de survie.
Dans ce cadre, l’objectif de ce projet est de construire un modèle de Machine Learning capable de classer une tumeur comme bénigne ou maligne à partir d’un ensemble de caractéristiques mesurées sur des biopsies.

Le but ultime est d’apporter un soutien automatique au diagnostic préliminaire, tout en réduisant les erreurs critiques, en particulier les faux négatifs, qui représentent un danger majeur pour le patient.

2. Présentation du Dataset

Le dataset utilisé provient de la bibliothèque scikit-learn et se nomme Breast Cancer Wisconsin (Diagnostic).
Il comporte :

569 observations

30 variables explicatives (mesures géométriques et texturales)

1 variable cible :

Malignant (0)

Benign (1)

Ces données proviennent de l’analyse de cellules tumorales extraites par biopsie.

3. Préparation et Nettoyage des Données

Afin de simuler des conditions plus proches de la réalité, des valeurs manquantes ont été introduites artificiellement dans le dataset.

Les principales étapes de préparation sont les suivantes :

● Gestion des valeurs manquantes

Application de SimpleImputer(strategy = 'mean'), en ajustant l’imputeur uniquement sur le train set afin d’éviter le data leakage.

● Standardisation

Utilisation de StandardScaler pour harmoniser les échelles des variables et optimiser les performances des modèles tels que la Régression Logistique ou le SVM.

● Division du dataset

Utilisation de train_test_split avec :

test_size = 0.20

random_state = 42

stratify = y
pour garantir une bonne représentativité des classes.

4. Analyse Exploratoire (EDA)

L’analyse exploratoire a permis de mettre en évidence :

une forte corrélation entre plusieurs variables géométriques (radius, perimeter, area)

des distributions globalement régulières

quelques variables présentant une légère asymétrie

Ces observations confirment la qualité du dataset et facilitent l’application des modèles de classification.

5. Méthodologie et Modèles

Trois modèles de classification ont été testés :

● Logistic Regression

Utilisée comme modèle de référence (baseline), simple et efficace.

● Support Vector Machine (SVM)

Adapté aux frontières de décision non linéaires.

● Random Forest

Modèle d’ensemble robuste basé sur plusieurs arbres de décision.
Il offre une bonne résistance au bruit et limite le surapprentissage.

Un GridSearchCV a ensuite été réalisé afin d’optimiser certains hyperparamètres du Random Forest, tels que le nombre d’arbres (n_estimators) et la profondeur maximale (max_depth).

6. Évaluation des Performances

Les modèles ont été évalués à l’aide des métriques suivantes :

Accuracy

Précision

Recall (sensibilité)

F1-Score

Matrice de confusion

✔ Importance du recall

Dans le domaine médical, le recall est la métrique la plus critique, car il reflète la capacité du modèle à identifier correctement les cas malins.
Un faux négatif correspond à un patient malade classé à tort comme sain, ce qui peut retarder gravement la prise en charge.

✔ Résultat global

Le Random Forest s’est avéré être le modèle le plus performant, notamment en termes de recall et de F1-score.
La matrice de confusion montre un nombre très faible de faux négatifs, ce qui confirme sa pertinence dans ce contexte.

7. Interprétation des Résultats

L’analyse des importances de variables calculées par le Random Forest met en évidence plusieurs caractéristiques particulièrement influentes :

worst radius

worst perimeter

mean concavity

mean texture

Ces indicateurs sont cohérents avec les propriétés médicales connues : les tumeurs malignes présentent généralement des irrégularités géométriques plus marquées.

8. Conclusion

Le modèle développé présente d’excellentes performances pour la classification des tumeurs bénignes et malignes.
Le Random Forest, optimisé par validation croisée, offre un compromis idéal entre robustesse, précision et capacité de généralisation.

Ce projet démontre le potentiel des techniques de Machine Learning pour assister le diagnostic médical.
Cependant, certaines limites subsistent :

absence de validation sur un dataset extérieur

dataset relativement propre comparé aux données cliniques réelles

nécessité de tests supplémentaires pour une utilisation clinique réelle

Des améliorations possibles incluent :

l’utilisation de modèles plus avancés (XGBoost, LightGBM)

une analyse approfondie via SHAP ou LIME

un élargissement du dataset pour renforcer la robustesse du modèle
