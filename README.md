# Distributech - Suivi des commandes des revendeurs  

![Python](https://img.shields.io/badge/python-3.9+-blue) ![SQLite](https://img.shields.io/badge/SQLite-database-lightgrey) ![ETL](https://img.shields.io/badge/ETL-automatisation-orange) ![Dropbox](https://img.shields.io/badge/Dropbox-integration-0061ff) ![License MIT](https://img.shields.io/badge/license-MIT-green)  

---
## Créateurs

- [Mathieu Laronce](https://github.com/MathieuLaronce)
- [Simon Brouard](https://github.com/TheBretonDuke)
- [Lucas Henneuse](https://github.com/lucasHENNEUSE)


## 📑 Table des matières  
1. [À propos](#-à-propos)  
2. [Fonctionnalités](#-fonctionnalités)  
3. [Prérequis](#-prérequis)  
4. [Technologies](#-technologies)  
5. [Utilisation](#-utilisation)  
6. [Développement](#-développement)  
7. [Architecture](#-architecture)  
8. [Licence](#-licence)  
9. [Créateurs](#-créateurs)  

---

## 📌 À propos  
**Distributech** est un projet interne destiné à centraliser et automatiser le suivi des **commandes** et des **stocks** des revendeurs régionaux d’équipements électroniques.  

Le système repose sur :  
- des **fichiers CSV hebdomadaires** déposés par les revendeurs sur **Dropbox**,  
- une **base SQLite** (stocks et catalogue produits).  

Un pipeline **ETL (Extract – Transform – Load)** en Python permet d’intégrer et de fiabiliser les données afin de fournir un suivi logistique et commercial complet.  

Les fichiers d’**état des stocks** générés automatiquement sont également déposés sur **Dropbox** pour être accessibles à tous les acteurs concernés.  

---

## ⚡ Fonctionnalités  
- 📥 Centralisation des **commandes des revendeurs** (CSV sur Dropbox).  
- 🗄️ Intégration des **stocks** depuis une base SQLite locale.  
- 🔄 **Pipeline ETL hebdomadaire** :  
  - **Extract** → récupération automatique des CSV depuis Dropbox + lecture SQLite,  
  - **Transform** → nettoyage, validation et harmonisation des données,  
  - **Load** → insertion dans une base SQL relationnelle.  
- 📊 Génération d’un **CSV de l’état des stocks** et **envoi automatique sur Dropbox**.  
- ⏳ Historisation des **mouvements de stock** (commandes, réceptions).  
- 🗂️ Base SQL structurée pour le suivi des **revendeurs, régions, produits, commandes et stocks**.  

---

## 🛠️ Prérequis  
- Python >= 3.9  
- SQLite  
- PostgreSQL ou MySQL (base centrale cible)  
- Docker *(optionnel pour déploiement et administration de la base)*  
- Compte **Dropbox** + clé API pour l’intégration  
- Bibliothèques Python listées dans `requirements.txt`  

---

## 🧰 Technologies  
- **Langage** : Python  
- **Bases de données** : SQLite (source), PostgreSQL/MySQL (cible)  
- **ETL** : Scripts Python (pandas, sqlite3, SQLAlchemy)  
- **Cloud** : Dropbox (dépôt et récupération automatique des fichiers)  
- **Conteneurisation** : Docker *(optionnel)*  
- **Export** : CSV (état des stocks)  

---

## 🚀 Utilisation  
1. Les revendeurs déposent leurs fichiers **CSV** dans le dossier **Dropbox** partagé.  
2. Lancer le pipeline ETL principal :  
   ```bash
   ## 📂 Scripts et fichiers du projet  

```bash
├── create_schema.py      # Script de création de la base SQL (tables revendeurs, produits, commandes, stocks)
├── extract.py            # Module d'extraction des données (CSV depuis Dropbox + lecture SQLite)
├── transform.py          # Module de transformation (nettoyage, validation, cohérence des données)
├── load.py               # Module de chargement (insertion dans la base SQL relationnelle)
├── etl_pipeline.py       # Orchestrateur ETL (appelle extract, transform et load)
├── requirements.txt      # Dépendances Python (pandas, sqlalchemy, dropbox, sqlite3, etc.)
├── distributech.sql      # Export complet de la base SQL (structure + données)
├── export_stocks.csv     # État des stocks généré automatiquement (puis uploadé sur Dropbox)
└── README.md             # Documentation du projet '''

---

## 👨‍💻 Développement  

Le projet est structuré autour de plusieurs composants principaux :  

### 📌 Base SQL  
- Créée via le script `create_schema.py`  
- Contient les tables principales :  
  - `regions` → zones géographiques  
  - `revendeurs` → partenaires commerciaux associés à une région  
  - `produits` → catalogue unique avec identifiant et coût unitaire  
  - `commandes` → commandes passées par les revendeurs  
  - `lignes_commandes` → détail des produits commandés (quantité, prix)  
  - `mouvements_stock` → suivi des entrées/sorties de stock  

---

### 📌 Pipeline ETL  
Le pipeline est découpé en 3 étapes principales, orchestrées par `etl_pipeline.py` :  

1. **Extract (`extract.py`)**  
   - Télécharge les fichiers **CSV** de commandes depuis **Dropbox**  
   - Lit la base **SQLite** pour récupérer les stocks actuels et les informations des revendeurs  

2. **Transform (`transform.py`)**  
   - Nettoyage et validation des données  
   - Conversion et uniformisation des formats de date  
   - Suppression des doublons et cohérence des données  

3. **Load (`load.py`)**  
   - Insertion des commandes, produits et mouve
