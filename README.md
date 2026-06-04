# Data Mining — Stratégies de Clustering

> Exploration et comparaison de techniques de clustering appliquées à des jeux de données réels.
> Projet universitaire — Module Data Mining · 2024–2025

---

## Aperçu du projet

Ce projet couvre deux algorithmes de clustering fondamentaux, implémentés sur des données réelles :

| Algorithme | Dataset | Approche |
|---|---|---|
| **K-Means** | `aligned_data.csv` — Intérêts utilisateurs (6 340 × 217) | Custom from scratch + scikit-learn |
| **Clustering Hiérarchique** | `data-Clustering-Hiérarchique.csv` — COVID-19 Europe (28 729 × 11, 30 pays) | Agglomératif Ward (Bottom-Up) + Divisif (Top-Down) |

Un rapport HTML interactif (`rapport.html`) documente l'ensemble du projet : panorama de **toutes** les stratégies de clustering connues, code annoté, résultats visualisés, conseils pratiques et métriques d'évaluation.

---

## Structure du dépôt

```
Data_Maining/
├── Clustering_hierarchique.ipynb   # Notebook clustering hiérarchique (COVID-19)
├── tpKMeans.ipynb                  # Notebook K-Means (Kaggle Interests)
├── rapport.html                    # Rapport complet (ouvrir dans un navigateur)
├── screenshots/                    # Captures des visualisations produites
│   ├── Screenshot 2025-01-23 ...   # Visualisations K-Means (jan. 23)
│   ├── Screenshot 2025-01-24 ...   # Visualisations Hiérarchique (jan. 24)
│   └── ...
└── projet_data_mining/             # Dossiers sources originaux (ignorés par git)
```

---

## Contenu du rapport

Le rapport (`rapport.html`) est organisé en 4 parties :

**Partie I — Panorama des stratégies de clustering**
- Taxonomie complète : partitionnement, hiérarchique, densité, modèles, spectral
- Tableau comparatif de 9 algorithmes (complexité, forme des clusters, scalabilité)
- Guide de sélection selon le type de données

**Partie II — K-Means Clustering**
- Dataset : 6 340 utilisateurs × 217 intérêts binaires (Kaggle)
- Implémentation from scratch avec NumPy broadcasting
- Comparaison custom vs scikit-learn pour K=3 et K=5
- Visualisation PCA 2D des clusters et centroïdes

**Partie III — Clustering Hiérarchique**
- Dataset : données COVID-19 journalières pour 30 pays européens (2020–2022)
- Alignement temporel, normalisation Min-Max, agrégation par pays
- Dendrogramme agglomératif Ward (Bottom-Up) avec seuil automatique
- Approche divisive Top-Down via `cut_tree`

**Partie IV — Conseils pratiques**
- Méthode du coude (Elbow) et score de silhouette pour choisir K
- Pièges courants : normalisation, haute dimensionnalité, confusion cluster/classe
- Pipeline de validation complet
- Métriques d'évaluation interne (Silhouette, Davies-Bouldin, Calinski-Harabasz)

---

## Technologies utilisées

- **Python 3** · pandas · NumPy · scikit-learn · SciPy · matplotlib · seaborn
- `scipy.cluster.hierarchy` : `linkage`, `dendrogram`, `fcluster`, `cut_tree`
- `sklearn.cluster.KMeans` · `sklearn.decomposition.PCA`
- `sklearn.preprocessing.MinMaxScaler`

---

## Lancer les notebooks

```bash
# Cloner le dépôt
git clone <repo-url>
cd Data_Maining

# Installer les dépendances
pip install pandas numpy scikit-learn scipy matplotlib seaborn jupyter

# Lancer Jupyter
jupyter notebook
```

> Les deux datasets sont inclus dans le dépôt :
> - `aligned_data.csv` → utilisé par `tpKMeans.ipynb`
> - `data-Clustering-Hiérarchique.csv` → utilisé par `Clustering_hierarchique.ipynb`

---

## Résultats clés

### K-Means
- K=3 et K=5 testés avec deux implémentations (custom + sklearn)
- Clusters bien séparés dans l'espace PCA 2D ; implémentation custom valide vs sklearn
- Limite identifiée : K-Means sur données binaires — K-Modes serait plus approprié

### Clustering Hiérarchique
- Plage d'analyse alignée : 2020-03-14 → 2022-10-12 (commune aux 30 pays)
- 3 métriques testées : `cases_deaths_sum`, `total_cases`, `total_deaths`
- Groupes identifiés : pays à forte incidence (DE, FR, IT) vs petits pays (LI, IS, CY)

---

*Réalisé par **Manel Morsli** — Année universitaire 2024–2025*
