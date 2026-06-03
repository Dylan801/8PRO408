# Analyse du catalogue Netflix

Projet de session — 8PRO408 Outils de programmation pour la science des données (UQAC, été 2026)

## Objectif

Explorer le catalogue Netflix pour identifier des corrélations entre les métadonnées des contenus (durée, genre, pays, année) et leur réception (note IMDB, popularité TMDB). On cherche à savoir si on peut prédire la note ou la popularité d'un contenu à partir de ses caractéristiques.

## Dataset

Source : [Netflix Movies and TV Shows Data Analysis](https://www.kaggle.com/datasets/nalisha/netflix-movies-and-tv-shows-data-analysis) (Kaggle)

- ~8800 films et séries
- 12 à 15 colonnes : type, titre, réalisateur, cast, pays, date d'ajout, année, rating, durée, genres, score IMDB, popularité TMDB
- Données manquantes sur director, cast, country (~30%)

## Structure du projet

```
projet/
├── README.md
├── data/
│   └── netflix.csv
├── notebook.ipynb          # notebook principal
└── rapport/
    └── fiches_individuelles.pdf
```

## Répartition du travail

| Membre | Rôle |
|--------|------|
| Personne 1 | Nettoyage et préparation des données |
| Personne 2 | Exploration et statistiques descriptives |
| Personne 3 | Matrice de corrélation et analyse |
| Personne 4 | Régression et prédiction |

## Questions de recherche

1. La durée d'un film est-elle corrélée à sa note IMDB ?
2. Les films récents sont-ils mieux notés que les anciens ?
3. Les contenus pour adultes (TV-MA) sont-ils mieux notés ?
4. Peut-on prédire la note IMDB à partir de la durée, l'année et le genre ?
5. Quels genres dominent le catalogue par décennie ?
6. Quels pays produisent le contenu le mieux noté ?

## Outils

- Python 3.14
- NumPy, Pandas, Matplotlib, SciPy, Scikit-learn

## Lancer le notebook

```bash
pip install numpy pandas matplotlib scipy scikit-learn jupyter
jupyter notebook notebook.ipynb
```

## Équipe

Projet réalisé dans le cadre du cours 8PRO408, session été 2026, UQAC.
