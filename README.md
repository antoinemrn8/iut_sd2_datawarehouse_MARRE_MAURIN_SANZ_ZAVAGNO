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
* **Lien :** [Formula 1 World Championship (1950-2020)](https://www.canva.com/design/DAHArW4maSc/Z1LiJy4RqfNhdi0O4NKEow/edit)
* **Format :** Fichiers CSV multiples (drivers, circuits, results, constructors, lap_times, etc.).
* **Volume :** Environ 14 tables couvrant plus de 70 ans d'histoire de la F1.
