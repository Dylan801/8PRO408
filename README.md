# Analyse du catalogue Netflix

Projet de session — 8PRO408 Outils de programmation pour la science des données (UQAC, été 2026)

## Objectif

On se met dans la peau de l'équipe Data de Netflix. À partir des métadonnées des films
(genre, langue, année, résumé), on cherche à comprendre ce qui fait le **succès** d'un contenu
— à la fois sa popularité et sa note — pour aider à décider quoi produire.

Le projet déroule le pipeline complet vu en cours : nettoyage → exploration → corrélation →
réduction de dimension → modèles → évaluation.

## Dataset

Source : `mymoviedb` (TMDB) — ~9000 films.

Colonnes principales : `Title`, `Release_Date`, `Overview`, `Genre`, `Original_Language`,
`Popularity`, `Vote_Count`, `Vote_Average`.

À noter : certaines lignes sont mal formatées dans la colonne `Overview` (gérées au chargement),
et `Vote_Count` / `Vote_Average` doivent être reconvertis en nombres.

## Structure du projet

```
projet/
├── README.md
├── data/
│   └── netflix.csv          # le dataset (non versionné, voir .gitignore)
├── notebook.ipynb           # notebook principal
└── rapport/
    └── fiches_individuelles.pdf
```

## Contenu du notebook

| Section | Contenu | Notion de cours |
|---------|---------|-----------------|
| 1-2 | Nettoyage, préparation, exploration (EDA) | préparation / découverte |
| 3-4 | Corrélations + régression linéaire | corrélation (C7, C9) |
| 5 | Skewness, kurtosis, boxplot par genre | Cours 7 |
| 6 | PCA (réduction de dimensionnalité) | Cours 9 |
| 7 | Arbre de décision + évaluation (confusion, ROC, F1) | Cours 8 |
| 8-9 | K-means (clustering) + analyse de texte (NLP) | Cours 10 |

## Répartition du travail

Chaque membre est responsable de ses sections : il les code, les commente et prépare la
partie orale correspondante. On ne modifie pas les sections d'un autre sans le prévenir.

| Membre | Sections | Notion principale |
|--------|----------|-------------------|
| Personne 1 | 1, 2, 6 | Nettoyage + PCA (Cours 9) |
| Personne 2 | 3, 4, 5 | Corrélation + statistiques de forme (Cours 7) |
| Personne 3 | 7 | Arbre de décision + évaluation (Cours 8) |
| Personne 4 | 8, 9 | K-means + NLP (Cours 10) |

## Questions de recherche

1. Comment se répartissent les notes et la popularité des contenus ?
2. Un film populaire est-il forcément bien noté ? (le paradoxe popularité / note)
3. Le nombre de votes influence-t-il la note ?
4. Quels genres et quelles langues réussissent le mieux ?
5. Combien de "vraies dimensions" se cachent derrière nos variables ? (PCA)
6. Peut-on prédire si un film sera un succès à partir de ses caractéristiques ?
7. Existe-t-il des familles naturelles de films ? (clustering)
8. Quels mots reviennent dans les résumés des films à succès ?

## Outils

- Python 3
- NumPy, Pandas, Matplotlib, Scikit-learn
- WordCloud (optionnel, pour le nuage de mots)

> Le projet n'utilise pas SciPy : la régression linéaire repose sur une fonction NumPy maison.

## Lancer le notebook

```bash
pip install numpy pandas matplotlib scikit-learn wordcloud jupyter
jupyter notebook notebook.ipynb
```

---

## Méthode de développement (Git)

On travaille avec **une branche par modification**, nommée selon le versionnage sémantique
`vX.Y.Z` :
- `X` : refonte majeure
- `Y` : nouvelle section / fonctionnalité
- `Z` : correction mineure

### À chaque nouvelle tâche

```bash
# 1. Toujours partir de la dernière version de main
git checkout main
git pull origin main

# 2. Créer sa branche de version
git checkout -b v0.3.0-pca-p1        # ex : P1 ajoute la PCA

# 3. Coder, puis (notebook : Restart & Clear Output d'abord, voir ci-dessous)
git add notebook.ipynb
git commit -m "v0.3.0 : ajout section PCA (cours 9)"

# 4. Pousser sa branche
git push origin v0.3.0-pca-p1
```

### Fusionner

Ouvrir une **Pull Request** vers `main` sur GitHub, un autre membre relit, puis on merge.
On ne pousse jamais directement sur `main`. Récupérer ensuite le travail des autres :

```bash
git checkout main
git pull origin main
```

Conseil : des PR **petites et fréquentes** (une section = une PR). Plus une branche vit
longtemps, plus les conflits sur le notebook sont pénibles.

---

## Conventions de code et bonnes pratiques notebook

Un notebook partagé à 4 est fragile : son état dépend de **l'ordre d'exécution**, pas de la
position des cellules. Pour éviter bugs et conflits :

1. **Avant chaque commit : `Kernel → Restart & Run All`.** Si le notebook ne tourne pas de
   bout en bout, on ne commit pas. Règle la plus importante.
2. **Videz les sorties avant de commit** (`Kernel → Restart & Clear Output`). Les images
   encodées en base64 polluent les diffs Git et créent des conflits ingérables.
3. **Le `df` global est défini une seule fois (section 1).** Ne refiltrez pas `df` ailleurs ;
   si une section a besoin d'un sous-ensemble, faites une **copie locale**
   (`dfc = df.dropna(subset=[...]).copy()`).
4. **Préfixez vos variables** par section pour éviter les collisions (`s6_pca`, `s7_clf`,
   `s8_km`...). Évitez les noms génériques partagés (`x`, `data`, `clean`).
5. **Commentaires en minuscules, sans accents**, comme le reste du notebook, pour rester homogène.

### Conflits sur un `.ipynb`

Un notebook est un gros fichier JSON que Git ne fusionne pas bien. En plus de vider les sorties,
on peut installer [`nbdime`](https://nbdime.readthedocs.io/) qui diff/merge les notebooks
cellule par cellule :

```bash
pip install nbdime
nbdime config-git --enable
```

---

## Équipe

Projet réalisé dans le cadre du cours 8PRO408, session été 2026, UQAC.