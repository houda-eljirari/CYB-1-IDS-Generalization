# CYB-1 — Cross-Dataset Generalization of Intrusion Detection Systems

**Projet de recherche académique — Master Systèmes Distribués et Intelligence Artificielle (SDIA)**

## 1. Présentation

Ce projet étudie la capacité des systèmes de détection d'intrusion (IDS) à généraliser leurs performances lorsqu'ils sont évalués sur un jeu de données différent de celui utilisé pendant leur entraînement.

Les performances élevées obtenues sur un benchmark ne garantissent pas nécessairement une bonne capacité de détection dans un autre environnement réseau. Elles peuvent notamment être influencées par des différences de distribution, des caractéristiques propres au jeu de données ou des artefacts liés au processus de collecte.

L'objectif est donc d'évaluer la robustesse des détecteurs d'intrusion et d'analyser les facteurs qui peuvent limiter leur généralisation.

## 2. Problématique de recherche

**Un détecteur d'intrusion entraîné sur un jeu de données peut-il conserver ses performances sur un autre jeu de données ou sur une période ultérieure ? Quelle part des performances observées peut être liée à des caractéristiques spécifiques du jeu d'entraînement ?**

Le projet examine notamment les écarts entre les évaluations intra-dataset et inter-datasets.

## 3. Jeux de données

Deux jeux de données publics sont étudiés :

- **CIC-IDS2017** : jeu de données de trafic réseau contenant du trafic bénin et plusieurs catégories d'attaques.
- **UNSW-NB15** : jeu de données de trafic réseau comprenant des observations normales et différentes catégories d'activités malveillantes.

Les fichiers de données sont conservés localement et ne sont pas inclus dans ce dépôt GitHub.

Les utilisateurs doivent récupérer les jeux de données depuis leurs sources officielles et respecter leurs conditions d'utilisation et de redistribution.

## 4. Objectifs expérimentaux

Le protocole de recherche est organisé autour des expériences suivantes.

### A. Évaluation intra-dataset

Entraîner et évaluer les modèles sur un même jeu de données afin d'établir des performances de référence.

### B. Évaluation inter-datasets

Étudier le transfert entre les deux jeux de données :

- CIC-IDS2017 → UNSW-NB15
- UNSW-NB15 → CIC-IDS2017

Cette expérience permet de mesurer la dégradation éventuelle des performances lorsque le domaine d'évaluation change.

### C. Audit des caractéristiques

Analyser les variables utilisées par les modèles, leur importance et leur éventuelle dépendance aux particularités des jeux de données.

### D. Ablation des caractéristiques

Retirer certaines variables ou certains groupes de variables afin d'observer leur influence sur les performances et la généralisation.

### E. Évaluation temporelle

Lorsque les informations temporelles disponibles le permettent, étudier la stabilité des performances sur des périodes distinctes.

## 5. Méthodologie

La démarche expérimentale repose sur les principes suivants :

- Harmoniser les variables communes aux deux jeux de données en tenant compte de leur signification et de leurs unités.
- Définir une cible binaire cohérente : trafic normal ou attaque.
- Séparer les données avant toute opération d'apprentissage du prétraitement.
- Éviter les fuites de données entre les ensembles d'entraînement et de test.
- Contrôler les doublons et les observations présentant des caractéristiques identiques.
- Utiliser des partitions reproductibles et des graines aléatoires documentées.
- Comparer les performances intra-dataset et inter-datasets.
- Analyser les erreurs et les limites d'interprétation des résultats.

Les doublons ne sont pas supprimés automatiquement : leur présence doit être interprétée en fonction de leur origine et de leur impact sur le protocole d'évaluation.

## 6. Modèles et métriques

Les modèles envisagés pour les premières expériences sont :

- Régression logistique ;
- Random Forest ;
- Réseau de neurones MLP.

Les modèles sont choisis pour permettre une comparaison entre une approche linéaire, une méthode d'ensemble et un modèle neuronal tabulaire, tout en restant compatibles avec un environnement de calcul CPU.

Les métriques étudiées comprennent notamment :

- Precision ;
- Recall ;
- F1-score ;
- Accuracy ;
- Balanced Accuracy ;
- PR-AUC / Average Precision.

Le F1-score et le rappel sont particulièrement importants compte tenu du déséquilibre entre les classes.

## 7. Organisation du dépôt

```text
CYB-1-IDS-Generalization/
│
├── data/
│   ├── raw/
│   ├── interim/
│   └── processed/
│
├── notebooks/
│   ├── 01_data_audit.ipynb
│   ├── 02_dataset_harmonization.ipynb
│   ├── 03_intra_dataset_baselines.ipynb
│   ├── 04_cross_dataset_evaluation.ipynb
│   ├── 05_feature_audit_ablation.ipynb
│   └── 06_temporal_evaluation.ipynb
│
├── src/
│   ├── data/
│   ├── models/
│   ├── evaluation/
│   └── visualization/
│
├── configs/
├── results/
│   ├── tables/
│   └── figures/
│
├── tests/
├── paper/
├── presentation/
│
├── requirements.txt
├── .gitignore
└── README.md
```

## 8. Environnement technique

Le projet utilise principalement :

- Python 3.11
- JupyterLab
- NumPy
- Pandas
- Scikit-learn
- Matplotlib
- Seaborn
- Imbalanced-learn
- SHAP

Les versions exactes des dépendances seront documentées dans `requirements.txt`.

## 9. Reproductibilité

Les expériences doivent être reproductibles autant que possible.

Les éléments suivants sont conservés dans le dépôt lorsqu'ils sont de taille raisonnable :

- Code source et notebooks ;
- Paramètres expérimentaux ;
- Graines aléatoires ;
- Indices des partitions ;
- Tableaux et figures de résultats validés ;
- Documentation du protocole.

Les données brutes et les fichiers de données volumineux restent exclus du dépôt.

## 10. État d'avancement

Le projet est actuellement en phase de préparation expérimentale.

| Composant | État |
|---|---|
| Audit initial des jeux de données | Réalisé |
| Analyse des distributions et de la qualité | Réalisée |
| Étude des doublons | Réalisée sur les échantillons |
| Harmonisation des variables communes | En cours de validation |
| Baselines intra-dataset | À réaliser |
| Évaluation inter-datasets | À réaliser |
| Audit des caractéristiques et ablations | À réaliser |
| Évaluation temporelle | Conditionnelle à la disponibilité de données temporelles exploitables |

Ce tableau sera mis à jour à mesure que les expériences seront validées.

## 11. Auteurs et contexte académique

Projet réalisé dans le cadre du Master **Systèmes Distribués et Intelligence Artificielle (SDIA)** à l'ENSET Mohammedia.

**Thématique :** Cybersécurité, détection d'intrusion, apprentissage automatique et généralisation inter-jeux de données.