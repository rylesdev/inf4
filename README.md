# INF4 - Python Workshop for Data Analysis

Projet réalisé dans le cadre du **M1 MIAGE SBI à Paris 1 Panthéon-Sorbonne**.

## Groupe G12

- Ryles AIT-MOHAMMED
- Aliou DIALLO
- Meryem BERRAMOU
- Rita HDIDOU
- Shirel MARCIANO

## Rendu de la séance 5, mini-projet Data Integration Case Study

Le notebook `notebooks/05-Data-Integration-Case-Study.ipynb` traite le cas Campus Tech. On y nettoie trois sources de données, on les relie entre elles, on calcule des indicateurs fiables par magasin et on évalue l'affirmation du responsable selon laquelle le magasin qui a le plus gros chiffre d'affaires total est le plus performant.

Le notebook suit les sept étapes de l'énoncé.

1. Audit des trois fichiers (taille, valeurs manquantes, doublons exacts, clés).
2. Nettoyage et validation, avec la table `sales_review` qui garde les lignes rejetées et leurs motifs.
3. Jointures contrôlées (`validate="many_to_one"`, indicateur, nombre de lignes vérifié) et tableau de réconciliation, du fichier brut jusqu'à la population analysée.
4. Indicateurs par magasin, par catégorie de produit et par jour, avec la vérification des totaux.
5. Les trois figures demandées et leur interprétation.
6. La note de synthèse destinée au responsable, avec les limites de l'analyse et les recommandations.
7. L'export des tableaux et des figures, puis les vérifications de reproductibilité.

Chaque cellule de code est expliquée en français, au-dessus (ce qu'elle fait et pourquoi ce choix) et en dessous (comment lire le résultat).

### Principaux résultats

- Sur les 241 commandes valides du 1er au 28 avril 2025, Paris Est (S2) a le plus gros chiffre d'affaires total, avec 10 529 € HT (38 % du total) pour 70 commandes.
- Lille Centre (S4) a le montant par commande le plus élevé (moyenne 190,42 €, médiane 158,50 €) avec seulement 30 commandes, et Paris Centre (S1) a le plus de commandes (91) pour la moyenne la plus faible (71,24 €).
- L'affirmation du responsable n'est donc pas confirmée, car le classement dépend de l'indicateur choisi. L'extrait ne permet pas non plus de parler de rentabilité, faute de données sur les coûts.

## Contributions

Nous avons fait tous les exercices des notebooks 01 à 05 ensemble, à cinq, sur l'ordinateur de l'un d'entre nous, pour que chacun comprenne bien les notions du cours et puisse expliquer chaque traitement. Pour chaque notebook, c'est en général une seule personne qui faisait ensuite le push, donc l'historique Git ne reflète pas le travail de chacun.

| Membre | Contributions |
|---|---|
| Ryles AIT-MOHAMMED | tous les exercices avec le groupe, création du dépôt et du README, mise en ligne des notebooks 01 et 05, des données et d'une partie des notebooks 03 et 04 |
| Aliou DIALLO | tous les exercices avec le groupe, mise en ligne du notebook 02 |
| Meryem BERRAMOU | tous les exercices avec le groupe |
| Rita HDIDOU | tous les exercices avec le groupe, mise en ligne du notebook 03 |
| Shirel MARCIANO | tous les exercices avec le groupe, mise en ligne du notebook 04 |

## Instructions d'exécution

1. Récupérer le dépôt.

   ```bash
   git clone https://github.com/rylesdev/inf4.git
   cd inf4
   ```

2. Installer les dépendances (Python 3.9 ou plus récent).

   ```bash
   python -m venv .venv
   source .venv/bin/activate        # sous Windows, .venv\Scripts\activate
   pip install -r requirements.txt
   ```

3. Vérifier que les trois fichiers de données du cas sont bien dans `data/`, à savoir `case_sales.csv`, `case_stores.csv` et `case_products.csv`.

4. Lancer Jupyter depuis la racine du dépôt, puis ouvrir `notebooks/05-Data-Integration-Case-Study.ipynb`.

   ```bash
   jupyter notebook
   ```

5. Redémarrer le noyau et exécuter toutes les cellules dans l'ordre (menu **Kernel**, puis **Restart Kernel and Run All Cells**). Le notebook s'exécute de haut en bas sans aucune intervention.

   On peut aussi l'exécuter en ligne de commande.

   ```bash
   jupyter nbconvert --to notebook --execute --inplace notebooks/05-Data-Integration-Case-Study.ipynb
   ```

6. Les tableaux et les figures sont enregistrés dans `notebooks/case_study_outputs/`.

Les fichiers bruts de `data/` ne sont jamais modifiés. Le notebook calcule l'empreinte SHA-256 de chaque fichier au début et la revérifie à la fin.

Le code a été testé avec Python 3.9 (pandas 2.2, NumPy 1.26, Matplotlib 3.8) et avec Python 3.13 (pandas 3.0, NumPy 2.5, Matplotlib 3.11).

## Fichiers produits par le notebook 05

| Fichier | Contenu |
|---|---|
| `store_summary.csv` | indicateurs par magasin (commandes, unités, chiffre d'affaires total, moyenne et médiane par commande) |
| `category_summary.csv` | chiffre d'affaires par catégorie de produit |
| `reconciliation.csv` | passage du fichier brut à la population analysée, étape par étape |
| `sales_review.csv` | lignes de ventes rejetées, avec le texte d'origine et les motifs du rejet |
| `integration_review.csv` | commandes valides dont le magasin ou le produit est inconnu |
| `fig1_total_revenue_by_store.png` | figure 1, chiffre d'affaires total et nombre de commandes par magasin |
| `fig2_order_revenue_distribution.png` | figure 2, distribution du chiffre d'affaires par commande |
| `fig3_daily_revenue_by_store.png` | figure 3, chiffre d'affaires journalier de chaque magasin |
| `unusual_price_orders.csv` | commandes valides vendues à un prix différent du prix habituel de leur produit, gardées et signalées |
| `daily_store_revenue.csv` et `reference_review.csv` | fichiers complémentaires (chiffre d'affaires par jour et par magasin, lignes des références en conflit, vide quand il n'y en a aucune) |
| `fig4_product_mix_heatmap.png` et `store_category_revenue_share.csv` | partie optionnelle sur le mix produit |

## Notebooks des séances

### `01-Python-NumPy.ipynb`

Premier notebook, sur les bases de Python et NumPy.

- listes, dictionnaires, conditions, boucles et fonctions
- tableaux NumPy
- slicing et indexation
- masques booléens
- calculs et statistiques avec NumPy
- première utilisation de pandas

### `02-Pandas-Manipulation-S2.ipynb`

Notebook consacré principalement à pandas.

- DataFrame et Series
- sélection de colonnes
- filtres
- `.loc` et `.iloc`
- tri des données
- création de nouvelles colonnes
- statistiques
- `groupby()`
- lecture et export de fichiers CSV

### `03-Data-Cleaning-S3.ipynb`

Notebook de la troisième séance, consacré au nettoyage des données (valeurs manquantes, types, doublons, conversions et règles de validité).

### `04-EDA-Visualization-S4.ipynb`

Notebook de la quatrième séance, consacré à l'exploration et à la visualisation des données, ainsi qu'à la jointure de deux tables sans perdre ni multiplier de lignes.

### `05-Data-Integration-Case-Study.ipynb`

Mini-projet de synthèse de la séance 5, décrit plus haut.

## Données

Les fichiers CSV sont dans le dossier `data`.

| Fichier | Utilisé dans |
|---|---|
| `homelessness.csv` | notebooks 01 et 02 |
| `sales_subset.csv` | notebooks 01 et 02 |
| `temperatures.csv` | notebooks 03 et 04 |
| `support_tickets.csv` et `support_sites.csv` | notebook 04 |
| `case_sales.csv`, `case_stores.csv` et `case_products.csv` | notebook 05 |

Toutes les données du cas Campus Tech sont synthétiques et fournies pour l'exercice. Les résultats décrivent cet extrait et non une entreprise réelle.

## Structure du projet

```text
inf4/
├── data/
│   ├── case_products.csv
│   ├── case_sales.csv
│   ├── case_stores.csv
│   ├── homelessness.csv
│   ├── sales_subset.csv
│   ├── support_sites.csv
│   ├── support_tickets.csv
│   └── temperatures.csv
│
├── notebooks/
│   ├── 01-Python-NumPy.ipynb
│   ├── 02-Pandas-Manipulation-S2.ipynb
│   ├── 03-Data-Cleaning-S3.ipynb
│   ├── 04-EDA-Visualization-S4.ipynb
│   ├── 05-Data-Integration-Case-Study.ipynb
│   ├── sales_by_type.csv          (créé par le notebook 02)
│   ├── cleaned/                   (créé par le notebook 03)
│   ├── figures/                   (créé par le notebook 04)
│   └── case_study_outputs/        (créé par le notebook 05)
│
├── requirements.txt
└── README.md
```

## Outils utilisés

- Python
- NumPy
- pandas
- Matplotlib
- Jupyter Notebook
