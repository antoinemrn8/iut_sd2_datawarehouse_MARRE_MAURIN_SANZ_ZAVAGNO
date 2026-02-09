# SAE Intégration de données dans un datawarehouse

**Participants :** MARRE Ewann / MAURIN Antoine / SANZ Rafaël / ZAVAGNO Quentin

## Présentation du Projet
Ce projet s'inscrit dans le cadre de la SAÉ 302 de l'IUT Lumière Lyon 2 (Année 2025-2026). L'objectif est de mettre en œuvre un pipeline décisionnel complet — de l'extraction des données brutes jusqu'à la visualisation — appliqué au monde de la Formule 1.

## Objectifs Décisionnels
L'analyse vise à répondre à plusieurs problématiques métiers pour une écurie ou un analyste sportif :
* **Performance Historique :** Quels sont les circuits où un pilote ou un constructeur spécifique performe le mieux ?
* **Évolution Technologique :** Comment les temps au tour ont-ils évolué sur un même circuit au fil des décennies ?
* **Fiabilité :** Quel est le taux d'abandon par constructeur et par type de problème mécanique ?
* **Analyse de Carrière :** Corrélation entre la position de départ (qualifications) et le résultat final en course.

## Source des Données
Les données utilisées proviennent de la plateforme Kaggle :
* **Lien :** [Formula 1 World Championship (1950-2020)](https://www.kaggle.com/datasets/rohanrao/formula-1-world-championship-1950-2020)
* **Format :** Fichiers CSV multiples (drivers, circuits, results, constructors, lap_times, etc.).
* **Volume :** Environ 14 tables couvrant plus de 70 ans d'histoire de la F1.

## Pipeline BI (Architecture)
Le projet suit le flux de travail suivant :

1. **Sources :** Données brutes de Kaggle (CSV).
2. **ETL (Extract, Transform, Load) :**
 * Nettoyage des données (gestion des valeurs manquantes \N, suppression des doublons).
 * Harmonisation des noms de pays et formats de dates.
3. Data Warehouse : Stockage structuré pour l'analyse.
4. Reporting : Création de tableaux de bord interactifs.

## Modélisation (Schéma en Étoile)
Afin d'optimiser les performances des requêtes décisionnelles, nous avons choisi une modélisation en étoile :
* **Table de Fait :** `Fact_Results` (contient les mesures : points, position, rang, temps).
* **Dimensions :**
  * `Dim_Drivers` (Nom, nationalité, date de naissance).
  * `Dim_Constructors` (Nom, nationalité).
  * `Dim_Circuits` (Localisation, altitude, nom).
  * `Dim_Time` (Saison, année).

## Installation et Utilisation
1. **Prérequis :** (Ex: PDI, PostgreSQL, Power BI).
2. **Clonage du dépôt :**
 ```
git clone https://github.com/votre-repo/sae-302-f1.git
```
4. **Exécution de l'ETL :** (Précisez la commande pour lancer votre script de nettoyage).


