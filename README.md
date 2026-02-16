# SAÉ 302 : Intégration de données dans un Data Warehouse (Formule 1)

**Année :** 2025-2026  
**Établissement :** IUT Lumière Lyon 2  
**Département :** Science des Données

## 👥 Équipe Projet
* **MARRE Ewann**
* **MAURIN Antoine**
* **SANZ Rafaël**
* **ZAVAGNO Quentin**

---

## 🏎️ Présentation du Projet
Ce projet s'inscrit dans le cadre de la SAÉ 302. L'objectif est de concevoir et mettre en œuvre un pipeline décisionnel complet (BI) — de l'extraction des données brutes jusqu'à la visualisation — appliqué à l'historique du championnat du monde de **Formule 1**.

Nous avons transformé des fichiers plats hétérogènes en un système d'information décisionnel performant permettant d'analyser plus de 70 ans de courses.

## 🎯 Objectifs Décisionnels
L'analyse vise à répondre aux questions clés que les fans ou les analystes sportifs se posent :
* **Performance Historique :** Quels sont les pilotes et constructeurs les plus titrés de l'histoire ?
* **Évolution Technologique :** Comment les temps au tour et les vitesses ont-ils évolué sur un même circuit au fil des décennies ?
* **Fiabilité :** Quel est le taux d'abandon (panne moteur, accident) par constructeur ?
* **Analyse de Carrière :** Quel pilote a la meilleure position d'arrivée moyenne ?
* **Géographie :** Répartition mondiale des Grands Prix.

---

## 📂 Architecture et Pipeline BI
Le projet suit une architecture en couches classiques, orchestrée par **Pentaho Data Integration (PDI)** :

1.  **Sources de Données (CSV) :**
    * Données brutes issues de Kaggle (Rohan Rao Dataset).
    * Contenu : Pilotes, résultats, temps au tour, arrêts aux stands, qualifications, etc.
    * *Volume :* ~14 tables couvrant la période 1950-2023.

2.  **Zone RAW (PostgreSQL) :**
    * Ingestion des fichiers CSV "tels quels" dans le schéma `raw`.
    * Script : `job_raw.kjb`.

3.  **Zone SAS - Storage Area System (PostgreSQL) :**
    * Nettoyage et typage des données.
    * Traitement des valeurs nulles (gestion du caractère `\N`).
    * Harmonisation des formats de dates et des noms de pays.
    * Script : `job_sas.kjb`.

4.  **Data Warehouse (PostgreSQL) :**
    * Stockage structuré en **Schéma en Étoile** dans le schéma `dwh`.
    * Génération des clés techniques (Surrogate Keys).

5.  **Reporting (Power BI) :**
    * Tableau de bord interactif (`PB_F1.pbix`) connecté au DWH.

---

## 📐 Modélisation (Schéma en Étoile)
Afin d'optimiser les performances des requêtes analytiques, nous avons modélisé les données comme suit :

### Tables de Faits
* **`fact_results`** : Table centrale (granularité : pilote/course). Contient les points, le rang, le temps de course en millisecondes et la vitesse.
* **`fact_lap_times`** : Détail des temps au tour pour des analyses de performance fine.

### Dimensions
* **`dim_drivers`** : Informations sur les pilotes (Nom, nationalité, date de naissance).
* **`dim_constructeurs`** : Écuries (Ferrari, McLaren, etc.) et nationalités.
* **`dim_circuits`** : Géolocalisation (Lat/Long), altitude et pays.
* **`dim_races`** : Informations sur l'événement (Nom du GP, année).
* **`dim_saisons`** & **`dim_calendrier`** : Axe temporel.
* **`dim_status`** : Référentiel des causes de fin de course (Fini, Accident, Panne...).

---

## 🛠️ Installation et Utilisation

### Prérequis
* **SGBD :** PostgreSQL
* **ETL :** Pentaho Data Integration (Spoon) 9.x ou supérieur
* **Dataviz :** Microsoft Power BI Desktop

### Instructions de déploiement

1.  **Clonage du dépôt :**
    ```bash
    git clone [https://github.com/votre-repo/dwh_marre_maurin_sanz_zavagno_5.git](https://github.com/votre-repo/dwh_marre_maurin_sanz_zavagno_5.git)
    ```

2.  **Préparation de la Base de Données :**
    * Exécuter les scripts SQL situés dans `dataframe/DATABASES/` pour créer les schémas et les tables :
        1.  `raw_f1.sql`
        2.  `sas_f1.sql`
        3.  `dwh_f1.sql`

3.  **Configuration de l'ETL :**
    * Ouvrir Pentaho (Spoon).
    * Configurer la connexion à votre base PostgreSQL (`db_f1`) dans le fichier `database.properties` ou directement dans les connexions du projet.
    * Mettre à jour les chemins d'accès aux fichiers CSV dans les transformations du dossier `_SOURCES`.

4.  **Exécution des flux :**
    Lancer les Jobs dans l'ordre suivant :
    * `_TRANSFORMATIONS/job_raw.kjb` (Chargement des CSV)
    * `_TRANSFORMATIONS/job_sas.kjb` (Nettoyage)
    * Exécuter ensuite les transformations de chargement du DWH (Dimensions puis Faits).

5.  **Visualisation :**
    * Ouvrir le fichier `PB_F1.pbix`.
    * Actualiser les données (nécessite de pointer vers votre instance locale PostgreSQL).

---

## 📂 Structure du projet

```text
📦 dwh_marre_maurin_sanz_zavagno_5
 ┣ 📂 dataframe
 ┃ ┣ 📂 DATABASES          # Scripts SQL de création des tables (DDL)
 ┃ ┣ 📂 _SOURCES           # Fichiers CSV bruts
 ┃ ┗ 📂 _TRANSFORMATIONS   # Flux ETL Pentaho (.ktr, .kjb)
 ┃   ┣ 📂 _RAW             # Injections brutes
 ┃   ┣ 📂 T_SAS            # Transformations de nettoyage
 ┃   ┣ 📂 T_DIM            # Chargement des dimensions
 ┃   ┗ 📂 T_FACT           # Chargement des faits
 ┣ 📜 PB_F1.pbix           # Rapport Power BI
 ┗ 📜 README.md
```
## 🔗 Liens utiles
* [Lien du tableau de bord](https://github.com/antoinemrn8/DWH_MARRE_MAURIN_SANZ_ZAVAGNO_5/blob/main/PB_F1.pbix)
* [Lien du rapport](https://github.com/antoinemrn8/DWH_MARRE_MAURIN_SANZ_ZAVAGNO_5/blob/main/DWH-MARRE-MAURIN-SANZ-ZAVAGNO-5.pdf)
* [Lien vers les transformations](https://github.com/antoinemrn8/DWH_MARRE_MAURIN_SANZ_ZAVAGNO_5/tree/main/dataframe/_TRANSFORMATIONS)
