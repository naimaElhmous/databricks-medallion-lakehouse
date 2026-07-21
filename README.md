# databricks-medallion-lakehouse

 Un Data Lakehouse complet, construit de A à Z sur **Databricks**, en suivant l'**architecture Médaillon** (Bronze / Silver / Gold) — de l'ingestion brute à un modèle en étoile prêt pour la BI.

## 🎯 Aperçu du projet

Ce projet consiste à construire un **Data Lakehouse complet** à partir de données brutes provenant de deux systèmes source (**CRM** et **ERP**), en les transformant progressivement en jeux de données **propres, fiables et prêts pour l'analyse**.

L'objectif n'est pas seulement d'écrire du code, mais de :

- **Concevoir une architecture** de données robuste et évolutive
- **Améliorer la qualité des données** à chaque étape
- **Modéliser les données** pour l'analytique (schéma en étoile)
- **Automatiser** l'ensemble du pipeline avec des jobs Databricks

Le résultat final est un Lakehouse de style production, réutilisable et présentable dans un portfolio.

---

## 🏗️ Architecture

Le projet suit l'**architecture Médaillon**, un pattern standard de l'industrie qui organise les données en trois couches de qualité croissante.

![Architecture Médaillon](mg1-medallion.png)

| Couche | Rôle | Détails |
|---|---|---|
| 🥉 **Bronze** | Ingestion brute | Copie fidèle des fichiers sources (CRM, ERP) en tables Delta, sans transformation |
| 🥈 **Silver** | Nettoyage & standardisation | Suppression des doublons, validation des types, standardisation des clés métier |
| 🥇 **Gold** | Modélisation métier | Modèle dimensionnel (faits/dimensions) prêt pour le reporting et la BI |

**Flux global :**

```
CRM/ERP CSV  →  Bronze (raw Delta)  →  Silver (clean & validated)  →  Gold (star schema)  →  BI / Analytics

```

---

## 📁 Structure du dépôt

```
databricks_bike_lakehouse/
│
├── bronze/
│   └── bronze_ingestion.ipynb          # Ingestion des 6 fichiers CSV bruts
│
├── silver/
│   ├── crm/
│   │   ├── silver_crm_cust_info.ipynb
│   │   ├── silver_crm_prd_info.ipynb
│   │   └── silver_crm_sales_details.ipynb
│   └── erp/
│       ├── silver_erp_cust_az12.ipynb
│       ├── silver_erp_loc_a101.ipynb
│       └── silver_erp_px_cat_g1v2.ipynb
│
├── gold/
│   ├── gold_dim_customers.ipynb
│   ├── gold_dim_products.ipynb
│   └── gold_fact_sales.ipynb
│
├── orchestration/
│   ├── silver_orchestration.ipynb      # Déclenche tous les notebooks Silver
│   └── gold_orchestration.ipynb        # Déclenche tous les notebooks Gold
│
└── README.md
```

---

## 🛠️ Technologies utilisées

- **Databricks** — plateforme Lakehouse (compute, notebooks, jobs)
- **Apache Spark** — traitement distribué des données
- **PySpark** — transformations en Python
- **Spark SQL** — requêtes et transformations SQL
- **Delta Lake** — format de table transactionnel (ACID)
- **Unity Catalog** — gouvernance, schémas et volumes
- **Databricks Jobs & Pipelines** — orchestration et planification
- **Git / GitHub** — versioning intégré via Databricks Git Folders

---

## ✅ Prérequis

- Bases en **SQL**, **Python** et **PySpark**
- Aucune expérience préalable avec Databricks n'est requise
- Un espace de travail Databricks (Community Edition ou Workspace complet)
- Un compte GitHub pour versionner le projet

---

## 🗂️ Jeux de données

| Système | Fichiers | Contenu |
|---|---|---|
| **CRM** | `cust_info.csv`, `prd_info.csv`, `sales_details.csv` | Informations clients, produits et ventes |
| **ERP** | `cust_az12.csv`, `loc_a101.csv`, `px_cat_g1v2.csv` | Données clients enrichies, localisation, catégories produits |

Les 6 fichiers CSV sont déposés dans un volume Unity Catalog dédié : `bronze.raw_sources`.

---

## 🗺️ Feuille de route du projet

### 🏗️ Phase 1 — Initialisation

**Objectif :** préparer l'environnement avant de construire le Lakehouse.

**Résultat :** l'environnement est prêt pour construire les couches Bronze, Silver et Gold.

---

### 🥉 Phase 2 — Couche Bronze

**Objectif :** ingérer tous les fichiers CSV bruts en tables Delta, sans aucune transformation.

**Résultat :** les 6 fichiers sources sont ingérés dans des tables Bronze dédiées, sans transformation.

---

### 🥈 Phase 3 — Couche Silver

**Objectif :** nettoyer et transformer les données Bronze pour produire des jeux de données fiables (étape la plus longue du projet).

**Résultat :** toutes les tables Bronze sont transformées en tables Silver validées et standardisées.

---

### 🥇 Phase 4 — Couche Gold

**Objectif :** construire un modèle dimensionnel (schéma en étoile) découplé des systèmes sources, prêt pour la BI.

**Résultat :** les tables Silver sont transformées en tables Gold prêtes pour l'analytique et le reporting.

---

### 🚀 Phase 5 — Pipeline & Orchestration

**Objectif :** automatiser le flux Bronze → Silver → Gold de bout en bout.

**Configuration :** 1 notebook Bronze · 6 notebooks Silver · 3 notebooks Gold

**Résultat :** un pipeline automatisé, planifié et fiable, du Bronze au Gold.

---

## 📊 Modèle de données (Gold)

Le modèle final suit un **schéma en étoile** :

- **`fact_sales`** : table de faits contenant les transactions de vente
- **`dim_customers`** : dimension client (fusion CRM + ERP)
- **`dim_products`** : dimension produit (fusion CRM + ERP)

---

