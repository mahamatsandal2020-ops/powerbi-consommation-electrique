# Tableau de bord Power BI : consommation électrique de campus

Tableau de bord Power BI sur la consommation électrique horaire de 1 636 bâtiments répartis dans 19 sites, sur les années 2016 et 2017. Les données proviennent du Building Data Genome Project 2 (BDG2), un jeu de données ouvert publié en 2020.

## Indicateurs principaux

- Consommation totale : 3,65 milliards de kWh (3 652,8 GWh)
- Moyenne journalière : environ 5 000 MWh par jour
- Pic horaire : 312,5 MWh, après nettoyage des anomalies
- Bâtiments actifs : 1 572 sur 1 636

## Tâches réalisées

1. **Analyse exploratoire :** structure des fichiers, taux de valeurs manquantes (8,9 % en moyenne), détection des pics aberrants (12 compteurs, 23 heures), profils horaires et mensuels.
2. **Nettoyage avec Power Query :** passage du format large (une colonne par bâtiment) au format long, suppression des valeurs vides, filtrage des anomalies (seuil de 20 000 kWh par heure), renommage et typage des colonnes, remplacement des usages absents par « Non renseigné ».
3. **Agrégation :** regroupement par heure, usage et site, soit environ 2 millions de lignes dans la table de faits.
4. **Modèle en étoile :** une table de faits (Fait_Horaire), trois dimensions (Dim_Batiments, Dim_Site, Dim_Usage) et une table Calendrier, reliées en un-à-plusieurs avec filtre unidirectionnel.
5. **Mesures DAX :** Total GWh, Nb jours, Moyenne journalière, Pic horaire, Moyenne horaire, Nb bâtiments actifs, Part du total.
6. **Visualisations :** quatre cartes KPI, trois graphiques (évolution journalière, répartition par usage, journée type), quatre segments (année, type de jour, usage, site).
7. **Info-bulles :** deux pages, l'une affichant le profil horaire du jour survolé, l'autre la répartition par site d'un usage.
8. **Documentation :** guide PDF pas à pas (`docs/`), description du thème visuel (`docs/theme.md`).

## Démonstration

[Voir la vidéo de démonstration](LIEN_DE_VOTRE_PUBLICATION_LINKEDIN) (à remplacer après publication)

## Structure du dépôt

```
.
├── README.md
├── powerbi/     fichier .pbix du tableau de bord
├── docs/        guide PDF et description du thème
└── data/        métadonnées des bâtiments (le fichier de consommation est trop volumineux, voir ci-dessous)
```

## Données

- `data/metadata.csv` : une ligne par bâtiment (usage, site, surface).
- Le fichier de consommation horaire (`electricity_cleaned.csv`, environ 175 Mo) dépasse la limite de GitHub. Il est disponible à partir de la publication source ci-dessous.

## Limites connues

- Le seuil d'anomalie est fixe (20 000 kWh par heure). Une méthode fondée sur le 99e percentile de chaque bâtiment serait plus robuste.
- Les fuseaux horaires des horodatages ne sont pas documentés : les heures de pointe doivent être interprétées avec prudence.
- Les noms de sites et de bâtiments sont des pseudonymes du jeu de données. Seul le site Panther a été rattaché à une localisation, par ses coordonnées.

## Source des données

Miller, C. et al. (2020). The Building Data Genome Project 2, energy meter data from the ASHRAE Great Energy Predictor III competition. *Scientific Data*, 7, 368. https://doi.org/10.1038/s41597-020-00712-x
