# Projet Time Series : Monthly Airline Passengers

## Contexte
Ce projet analyse la série temporelle mensuelle du nombre de passagers aériens de 1949 à 1960. L’objectif est de modéliser le trafic aérien, d’évaluer la saisonnalité et la tendance, puis de produire des prévisions fiables pour l’année 1960.

## Contenu du projet
- `projet_timeseries_p.ipynb` : notebook principal contenant l’analyse exploratoire, les transformations, les tests de stationnarité, la modélisation AR/MA/ARIMA/SARIMA et l’évaluation.
- `airline_passengers.csv` : jeu de données des passagers mensuels.
- `rapport.pdf` : rapport du projet détaillant la méthodologie et les résultats.

## Données
- Période : janvier 1949 à décembre 1960
- Fréquence : mensuelle
- Variable cible : nombre de passagers aériens

## Méthodologie
1. Importation et prétraitement
   - Lecture du fichier CSV
   - Conversion de la date en index temporel
   - Inférence de la fréquence mensuelle

2. Analyse exploratoire
   - Statistiques descriptives
   - Visualisation de la série brute
   - Analyse de la saisonnalité mensuelle
   - Décomposition additive/multiplicative

3. Transformations et stationnarité
   - Test ADF et KPSS sur la série brute
   - Transformation logarithmique pour stabiliser la variance
   - Différenciation ordinaire et saisonnière
   - ACF/PACF pour identifier les ordres de modèle

4. Modélisation
   - Baselines : naïf et moyenne mobile (MA(12))
   - AR(p) construit manuellement par OLS
   - MA(q) construit manuellement par optimisation
   - Recherche de grille ARIMA(p,0,q) sur l’espace log
   - SARIMA(1,1,1)(1,1,1)[12] sur la série logarithmique
   - Recherche de grille SARIMA(p,1,q)(1,1,1)[12]

5. Évaluation
   - Métriques : MSE, RMSE, MAE, MAPE
   - Comparaison des modèles sur la période de test (1960)
   - Visualisation des prévisions en espace log et original
   - Analyse des résidus et test de Ljung-Box
   - Validation walk-forward avec fenêtre expansive

## Résultats clés
- L’analyse confirme une tendance croissante forte et une saisonnalité annuelle marquée.
- La série présente un comportement multiplicatif : la variance augmente avec le niveau.
- La transformation logarithmique est utilisée pour stabiliser la variance avant modélisation.
- Le modèle SARIMA capture explicitement la saisonnalité d’ordre 12 et donne les meilleures prévisions.
- La MAPE finale sur les passagers en espace original est proche de 2,3 %, ce qui est satisfaisant pour ce type de série.

## Instructions
1. Ouvrir `projet_timeseries_p.ipynb` avec Jupyter Notebook ou JupyterLab.
2. Exécuter les cellules dans l’ordre : import, chargement des données, analyse, transformation, modélisation et évaluation.
3. Vérifier les sections `Modélisation` et `Évaluation` pour comparer les performances et diagnostiquer les résidus.

## Recommandations
- Tester d’autres ordres SARIMA (par exemple SARIMA(1,1,2) ou SARIMA(2,1,1)).
- Expérimenter avec des modèles SARIMAX si des variables exogènes sont disponibles.
- Comparer avec des approches modernes comme Prophet, LSTM ou N-BEATS.

## Remarques
- Le respect de l’ordre chronologique est impératif : le jeu de données ne doit pas être mélangé avant la modélisation.
- Le train/test utilisé dans le notebook est : 132 observations pour l’entraînement (1949–1959) et 12 observations pour le test (1960).
