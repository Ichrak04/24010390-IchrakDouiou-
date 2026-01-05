# Ichrak Douiou

**Numéro d'étudiant** : 24010390

**Classe** : CAC1


<img src="ichrak.jpg" style="height:464px;margin-right:432px"/>    <img src="encgsettat.jpg" style="height:464px;margin-right:432px"/>

<br clear="left"/>

---
📘 GRAND GUIDE : ANATOMIE D'UN PROJET DATA SCIENCE
Ce document décortique chaque étape du cycle de vie d'un projet de Machine Learning appliqué au jeu de données “Diabetes” fourni dans le notebook joint. Il est conçu pour passer du niveau "débutant qui copie du code" au niveau "ingénieur qui comprend les mécanismes internes".


1. Le Contexte Métier et la Mission
Le Problème (Business Case)
Dans le domaine de la santé, le dépistage précoce du diabète permet de réduire les complications graves (cardiopathie, insuffisance rénale, amputations) et d'orienter les patients vers des interventions préventives.

Objectif : Construire un modèle de prédiction capable de classer un patient comme diabétique ou non à partir de mesures cliniques présentes dans la base (ex. Age, BMI, Insulin Levels, etc.).

L'Enjeu critique : La matrice des coûts d'erreur est asymétrique :

Dire à un patient sain qu’il est diabétique (Faux Positif) entraîne stress, examens et coûts supplémentaires.

Dire à un patient diabétique qu’il est sain (Faux Négatif) peut retarder la prise en charge et aggraver le pronostic. Le modèle doit donc privilégier la sensibilité (Recall) pour limiter les faux négatifs.

2. Les Données (L'Input)
Le notebook lit un fichier CSV nommé "bdd diabet.csv" et affiche les premières lignes, la structure et des statistiques descriptives.

X (Features) : Colonnes observées et utilisées incluent notamment Age, BMI, Insulin Levels et d’autres attributs cliniques présents dans le fichier CSV.

y (Target) : Colonne Target binaire indiquant la présence ou l'absence de diabète.
Le script effectue des visualisations élémentaires (histogrammes pour Age, BMI, Insulin Levels et un countplot pour la Target) afin d’évaluer la distribution des variables et le déséquilibre éventuel des classes.

3. Le Code Python (Laboratoire)
Le notebook contient des cellules d’importation (pandas, seaborn, matplotlib), de chargement du fichier CSV, d’inspection (head, columns, info, describe, isnull().sum()) et de visualisation (histplots et countplot).
Le code prépare les étapes d’EDA et permet d’identifier les valeurs manquantes et la répartition des classes, constituant la base pour le nettoyage et la modélisation ultérieure.

4. Analyse Approfondie : Nettoyage (Data Wrangling)
Le notebook montre le comptage des valeurs manquantes (df.isnull().sum()) mais n’applique pas de stratégie avancée d’imputation dans les cellules visibles de l’extrait. Les bonnes pratiques applicables ici sont :

Séparer d’abord Train/Test puis appliquer l’imputation en s’appuyant uniquement sur les statistiques du Train pour éviter la fuite de données (data leakage).

Traiter les outliers et vérifier les unités/valeurs aberrantes (par ex. insuline à 0 ou BMI impossibles).

Encodage et normalisation/standardisation selon les algorithmes choisis.

5. Analyse Approfondie : Exploration (EDA)
Le notebook produit des histogrammes pour Age, BMI et Insulin Levels et un countplot de la Target pour visualiser le déséquilibre de classes. À réaliser ensuite :

Calculer corrélations (heatmap) pour détecter multicolinéarité.

Étudier les statistiques groupées par Target (moyennes, médianes) pour identifier features discriminantes.

Vérifier skewness et appliquer transformations (log, Box-Cox) si nécessaire pour variables fortement asymétriques.

6. Méthodologie Expérimentale (Split & Protocol)
Le notebook prépare l’EDA ; implémenter ce protocole est recommandé :

Séparer les données en Train/Test (ex. 80/20) avec stratification sur la Target si classes déséquilibrées.

Utiliser validation croisée (StratifiedKFold) pour une évaluation robuste des modèles.

Définir métriques cliniquement pertinentes : Recall (prioritaire), Precision, F1-score, AUC-ROC et matrice de confusion.

7. Algorithmes pour l'Apprentissage
Le projet peut tester plusieurs modèles et baseline : régression logistique (interprétable), arbres de décision, forêts aléatoires, XGBoost pour la performance, et Naïve Bayes comme baseline rapide. Le choix final doit équilibrer performance (Recall/AUC) et explicabilité pour un usage médical.

8. Évaluation (L'Heure de Vérité)
La matrice de confusion et les métriques dérivées sont essentielles :

Privilégier Recall pour réduire les Faux Négatifs.

Contrôler Precision pour limiter les Faux Positifs et coûts induits.

Utiliser AUC-ROC pour comparer discriminations globales.
Rapports à produire : classification_report, courbe ROC, matrice de confusion annotée et tableau récapitulatif des métriques par modèle.

9. Livrables et Recommandations Opérationnelles
Notebook reproduisant l’EDA, le prétraitement, l’entraînement et l’évaluation (avec seeds pour reproductibilité).

Modèle(s) sauvegardé(s) (pickle / joblib).

Rapport Markdown (ce document) et visualisations prêtes pour présentation.

Recommandations pour production : validation externe sur une population indépendante, protocole d’éthique et de confidentialité, seuil de décision calibré pour maximiser Recall tout en gardant un taux acceptable de FP.

10. Points d'Attention / Risques
Data Leakage si imputation ou scaling est faite avant le split.

Biais du dataset (si provenance limitée — ex. population spécifique) pouvant limiter la généralisation.

Exigences réglementaires et éthiques en santé (consentement, anonymisation).

Nécessité d’une validation clinique avant tout déploiement.

