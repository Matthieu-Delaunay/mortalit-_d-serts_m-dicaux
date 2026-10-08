# Mortalité et accessibilité aux soins par zone d'emploi

Analyse statistique réalisée en **R** dans le cadre de mon mémoire de magistère. Le projet étudie le lien entre le taux de mortalité et l'accessibilité aux soins de proximité dans les zones d'emploi françaises.

## Question de recherche

Comment les déserts médicaux influencent le taux de mortalité annuel moyen au sein des zones d’emploi en France ?

## Données

Le jeu de données regroupe, pour chacune des 306 zones d'emploi, les indicateurs suivants :

| Indicateur | Variable dans le code | Période |
|---|---|---|
| Taux de mortalité annuel moyen | `Mortalite` | 2016-2022 |
| APL des médecins généralistes | `Medecin` | 2023 |
| Densité des pharmacies pour 10 000 habitants | `Pharmacie` | 2024 |
| APL des infirmiers (65 ans et moins) | `Infirmiers` | 2023 |
| APL des chirurgiens-dentistes (65 ans et moins) | `Dentistes` | 2023 |

L'**APL** (accessibilité potentielle localisée) est un indicateur qui mesure l'adéquation entre l'offre de soins et la demande de la population d'un territoire.

Les fichiers attendus dans le dossier `data/` sont :

| Fichier | Contenu |
|---|---|
| `Morta_zone_emploi.csv` | Mortalité et population par zone d'emploi |
| `DesMed_Zone_Emploi.csv` | Médecins généralistes |
| `pharmacie_zoneEmploi.csv` | Pharmacies |
| `infirmier_zoneEmploi.csv` | Infirmiers |
| `dentiste_zoneEmploi.csv` | Chirurgiens-dentistes |


## Structure du dépôt

```
.
├── data/                           # Fichiers CSV (voir ci-dessus)
├── memoire_mortalite_soins.Rmd     # Analyse complète (R Markdown)
├── .gitignore
└── README.md
```

## Méthode

1. **Préparation** : lecture des cinq fichiers CSV, conversion des colonnes en numérique.
2. **Jeu d'analyse** : regroupement des indicateurs par zone d'emploi et suppression des zones comportant des valeurs manquantes.
3. **Corrélations** : matrice de corrélation entre la mortalité et les quatre indicateurs d'accessibilité, représentée avec `ggcorrplot`.
4. **Régressions linéaires simples** : mortalité en fonction de chaque indicateur, avec résumé du modèle, graphiques de diagnostic et nuage de points avec droite de régression.
5. **Résumé descriptif** des variables avec `gtExtras`.

## Résultats

Concernant la profession des médecins généralistes, nous pouvons valider l’hypothèse selon laquelle les déserts médicaux sont centrés dans les milieux ruraux et les banlieues ; 
L’hypothèse selon laquelle les déserts médicaux d’infirmiers sont centrés dans les milieux ruraux et les banlieues peut être considérée comme valide ;  
L’hypothèse selon laquelle les déserts médicaux de chirurgiens-dentistes sont centrés dans les milieux ruraux et les banlieues peut être considérée comme valide ; 
On ne peut pas valider l’hypothèse selon laquelle les déserts médicaux concernant les pharmacies sont centrés dans les milieux ruraux et les banlieues.
On observe, dans nos données, un lien significatif et négatif entre l’APL des médecins généralistes et le taux de mortalité annuel moyen. Toutefois, la validité du modèle peut être questionnée notamment à cause d’un possible biais dans les résidus ou d’une possible non-linéarité ;
On constate l’existence d’un lien significatif entre l’APL des infirmiers et le taux de mortalité annuel moyen, toutefois lui aussi questionnable à cause d’un possible biais dans les résidus ou d’une possible non-linéarité ; 
On observe un lien significatif et négatif entre l’APL des dentistes et le taux de mortalité annuel moyen ; 
On observe un lien significatif et positif entre la densité des pharmacies et le taux de mortalité annuel moyen. Toutefois, la validité du modèle peut être questionnée notamment à cause d’un possible biais dans les résidus ou d’une possible non-linéarité.
Il est cependant à noter que certains territoires viennent biaiser avec des valeurs extrêmes nos modèles, notamment les territoires de  la Guyane et la Réunion.

## Installation et utilisation

### Prérequis

- [R](https://www.r-project.org/) (version 4.1 ou supérieure) et [RStudio](https://posit.co/download/rstudio-desktop/) (conseillé)
- Packages R : `ggplot2`, `ggcorrplot`, `gtExtras` (avec `rmarkdown` et `knitr` pour générer le rapport)

```r
install.packages(c("ggplot2", "ggcorrplot", "gtExtras", "rmarkdown"))
```

### Exécution

1. Cloner le dépôt :
   ```bash
   git clone https://github.com/Matthieu-Delaunay/NOM-DU-DEPOT.git
   ```
2. Placer les fichiers CSV dans le dossier `data/`.
3. Ouvrir `memoire_mortalite_soins.Rmd` dans RStudio, définir le dossier du projet comme répertoire de travail, puis cliquer sur **Knit** pour générer le rapport HTML.

## Limites

- Les régressions sont des **régressions simples** (un indicateur à la fois) : elles ne tiennent pas compte des autres facteurs pouvant influencer la mortalité (âge de la population, niveau de vie, etc.).
- Une corrélation ne prouve pas un lien de cause à effet.
- Le code suppose que les cinq fichiers listent les zones d'emploi dans le même ordre.

## Auteur

**Matthieu Delaunay**
