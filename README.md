# 📍 AMDM Project 2026 - Analyzing Human Activity and Mobility

![Python](https://img.shields.io/badge/Python-3.9%2B-blue)
![MovingPandas](https://img.shields.io/badge/Library-MovingPandas-orange)
![GeoPandas](https://img.shields.io/badge/Library-GeoPandas-green)
![Jupyter](https://img.shields.io/badge/Environment-Jupyter-F37626)
![UVSQ](https://img.shields.io/badge/UVSQ-M2%20Datascale-blueviolet)

> **Projet AMDM - Partie 1 : GPS Trajectory Analytics**
> **Enseignante :** Karine Zeitouni
> **Université Paris-Saclay / UVSQ - Campus de Versailles**
> *Janvier 2026*

## 📖 Description

Ce projet porte sur l'analyse de traces GPS (Human Activity and Mobility) collectées en continu par un utilisateur unique sur une semaine. L'objectif est de transformer des données géospatiales brutes en informations sémantiques intelligibles.

Nous utilisons la bibliothèque **MovingPandas** pour segmenter les trajectoires, nettoyer les données et identifier des modèles de mobilité. Le projet inclut une validation croisée avec un fichier d'auto-déclaration ("Self-report") pour vérifier la précision des algorithmes de détection.

## 🎯 Objectifs (Partie 1)

1.  **Pré-traitement :** Chargement et nettoyage des logs GPS bruts, segmentation temporelle par jour.
2.  **Analyse de Trajectoire :** Utilisation de **MovingPandas** pour visualiser les parcours et détecter les anomalies.
3.  **Sémantique :** Segmentation des traces en **Arrêts** (Stops) et **Déplacements** (Moves), et classement des segments.
4.  **Inférence de Lieux :** Algorithme pour identifier automatiquement le "Domicile" et le "Travail" et calcul de statistiques temporelles.
5.  **Validation :** Comparaison des résultats algorithmiques avec la vérité terrain (Self-report).

## 🏗 Architecture du Projet

Le projet est structuré pour séparer les données brutes, le code d'analyse et les résultats exportés :

```text
AMDM_Project_Part1/
│
├── 📂 data/                  # Données du projet
│   ├── 📂 raw/
│   │   ├── gps_log.csv       # Log GPS brut (Latitude, Longitude, Time)
│   │   └── self_report.csv   # Vérité terrain (Activités déclarées)
│
├── 📂 screenshots_report/    # Captures d'écran pour le rapport PDF
│
├── 📂 output/                # Résultats générés
│   └── trajectories.mfjson   # Export final au format MF-JSON
│
├── AMDM_Part1_Analysis.ipynb # Notebook unique contenant toute l'analyse
├── requirements.txt          # Dépendances Python
└── README.md                 # Documentation du projet
```

## 📦 Dépendances et Rôles Techniques

Ce projet repose sur un écosystème Python spécialisé dans l'analyse de données géospatiales. Voici le rôle précis de chaque bibliothèque dans le pipeline de traitement de la **Partie 1** :

| Bibliothèque | Rôle Technique dans le Projet |
| :--- | :--- |
| **`movingpandas`** | **Cœur de l'analyse.** Utilisée pour transformer les points GPS en objets `Trajectory`, segmenter les données (Stop/Move detection), nettoyer le bruit (filtre de Kalman) et exporter les résultats au format **MF-JSON**. |
| **`geopandas`** | Gestion des structures de données géospatiales (`GeoDataFrame`). Permet de manipuler la colonne `geometry` (Points) et de projeter les coordonnées (CRS) pour des calculs de distance précis en mètres. |
| **`pandas`** | Chargement des fichiers CSV bruts (`gps_log.csv`, `self_report.csv`), manipulation des index temporels (`DatetimeIndex`) et jointures de données. |
| **`hvplot`** / **`holoviews`** | Moteur de visualisation interactif utilisé par MovingPandas pour explorer les trajectoires sur des fonds de carte (OSM, CartoDB) et inspecter les arrêts. |
| **`shapely`** | Librairie de bas niveau pour la manipulation géométrique pure. Utilisée implicitement pour créer les objets `Point` à partir des coordonnées Latitude/Longitude. |
| **`sqlalchemy`** | Fournit l'interface SQL pour interagir avec des bases de données si nécessaire, ou pour exécuter des requêtes structurées sur les données. |


## 🚀 Guide d'Installation et d'Exécution

Suivez ces étapes pour reproduire l'environnement de développement et lancer l'analyse des données GPS.

### 1. Cloner le dépôt
Récupérez le code source du projet sur votre machine locale :

```bash
git clone https://github.com/Ciscom224/projet_AMDM_M2
cd AMDM_Project_Part1
```
### 2. Créer un environnement virtuel

Il est fortement recommandé d'utiliser un environnement virtuel pour isoler les dépendances du projet et éviter les conflits avec votre installation Python globale.

**Sous Windows :**
```bash
python -m venv venv
.\venv\Scripts\activate
```
**Sous Mac / Linux :**
```bash
python3 -m venv venv
source venv/bin/activate
```
### 🔧 Installation Rapide
Toutes ces dépendances sont installables via le fichier `requirements.txt` fourni :

```bash
pip install -r requirements.txt
```