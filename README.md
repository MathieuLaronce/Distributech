1 Table des matières:

Contexte
Objectifs
Sources de données
Fonctionnalités principales
Architecture et schéma de la base
ETL de pipelines
Scripts Python
Installation et utilisation
Livrables
Licence
Contexte : Distributech est un projet de gestion des stocks et des commandes pour un grossiste en équipements électroniques collaborant avec un réseau de revendeurs régionaux.
L'objectif est de centraliser les données provenant de plusieurs sources afin de suivre l'évolution des stocks et des commandes de manière fiable.

2 Objectifs :

Mettre en place une base SQL relationnelle pour modéliser :
Les revendeurs et leurs régions
Le catalogue des produits
Les commandes passées
L'évolution des stocks dans le temps
Développer un pipeline ETL en Python pour :
Extraire les données depuis une base SQLite et des fichiers CSV
Transformer les données (contrôles de cohérence, nettoyage, suppression des doubles)
Charger les données dans une base SQL centralisée
Générer un CSV d'état des stocks par produit pour le suivi logistique et commercial
Sources de données :

Fichiers CSV : commandes hebdomadaires envoyées par les revendeurs
Base SQLite locale : état du stock global, informations sur les produits et les revendeurs
Fonctionnalités principales :

Création et initialisation de la base SQL
Importation automatique des commandes des revendeurs
Mise à jour des stocks en fonction des réceptions et des commandes
Export de l'état du stock par produit au format CSV
Scripts Python modulaires ( etl.py, analyse_stock.py, db_stock.py, etc.)
Architecture et schéma de la base : (Insérer ici un diagramme ou schéma de la base SQL si disponible)

ETL de pipeline :

Extraction : SQLite et CSV
Transformation : nettoyage, contrôle de cohérence, suppression des doublons
Chargement : insertion dans la base SQL centralisée
Export : génération du fichieretat_stock_par_produit.csv
Scripts Python :

etl.py: pipeline ETL terminé
analyse_stock.py: analyser et exporter des stocks
db_stock.py: fonctions d'accès à la base
main.py: script principal de lancement
schema.py: création de tables SQL
seed_data.py: insertion de données d'exemple
exporte_sql.py: exportation de la base SQL
Installation et utilisation :


Cloner le projet depuis GitHub :
git clone https://github.com/tonpseudo/Distributech.git
cd Distributech
