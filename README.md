# Anti-Money-Laundering-Detection
End-to-end Anti-Money Laundering (AML) detection on massive transactional data (5M+ transactions, 68K+ active accounts): SQL feature engineering in PostgreSQL, unsupervised anomaly detection (HDBSCAN, Isolation Forest, PCA) in Python, and interactive compliance BI in Power BI. 

 # 🕵️ Détection du Blanchiment d'Argent (AML) & Dashboard de Conformité

![PostgreSQL](https://img.shields.io/badge/Database-PostgreSQL-316192)
![Python](https://img.shields.io/badge/Python-3.9%2B-blue)
![Jupyter](https://img.shields.io/badge/Notebook-Jupyter-F37626)
![Machine Learning](https://img.shields.io/badge/ML-HDBSCAN%20%7C%20Isolation%20Forest-orange)
![Power BI](https://img.shields.io/badge/BI-Power%20BI-F2C811)

## 📌 Contexte et Objectif
La lutte contre le blanchiment d'argent (Anti-Money Laundering) exige d'identifier des comportements financiers atypiques au sein de volumes massifs de transactions, sans disposer d'étiquettes de fraude préalables. Ce projet met en place une architecture complète — de la base de données jusqu'à la restitution métier — sur le jeu de données **IBM Transactions for AML** (**68 955 comptes actifs**).

## 🏗️ Architecture du Pipeline
1. **Ingénierie des données (`sql/`) :** Agrégation des flux transactionnels sous **PostgreSQL** pour construire des indicateurs comportementaux par compte (volumes envoyés/reçus, fréquence des opérations, nombre de bénéficiaires distincts).
2. **Détection d'anomalies (`notebooks/`) :** Notebook **Jupyter** appliquant une normalisation robuste (`RobustScaler`), une réduction de dimension (**PCA**) et deux algorithmes complémentaires d'apprentissage non supervisé (**HDBSCAN** et **Isolation Forest**) pour scorer le risque de chaque compte.
3. **Restitution & Investigation (`dashboard/`) :** Tableau de bord interactif sous **Power BI** connecté à PostgreSQL permettant aux analystes conformité de filtrer les alertes critiques et de visualiser les clusters.

## 🧠 Justification des Choix Techniques
* **`RobustScaler` vs StandardScaler :** Utilisation de la médiane et de l'écart interquartile (IQR) pour éviter que les virements extrêmes (outliers de plusieurs milliards) ne faussent la mise à l'échelle.
* **`HDBSCAN` & `Isolation Forest` vs K-Means :** Contrairement à K-Means qui force chaque point dans un cluster et reste sensible aux moyennes, HDBSCAN isole naturellement les comportements aberrants (cluster `-1`) selon la densité des transactions, complété par le score d'isolement d'Isolation Forest.

## 📊 Aperçu du Tableau de Bord (Power BI)
![Vue Globale Dashboard AML](assets/dashboard_overview.png)
![Projection PCA des Anomalies](assets/pca_scatter_plot.png)

## 🚀 Installation et Exécution

1. **Cloner le dépôt :**
```bash
git clone https://github.com/HachimMohamed/Anti-Money-Laundering-Detection.git
cd Anti-Money-Laundering-Detection
```

2. **Installer les dépendances Python :**
```bash
pip install -r requirements.txt
```

3. **Exécuter le pipeline :**
* Importer les données brutes dans **PostgreSQL** et exécuter le script `sql/aggregation_comptes.sql`.
* Lancer Jupyter (`jupyter notebook`), ouvrir le fichier dans `notebooks/`, renseigner vos identifiants PostgreSQL et exécuter les cellules pour générer la table `analytics.resultats_aml_final`.
* Ouvrir `dashboard/aml_compliance_dashboard.pbix` avec **Power BI Desktop** et actualiser la source de données.
 
