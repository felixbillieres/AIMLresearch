# Datasets — Cheat Sheet

**Idée centrale :** La qualité des données détermine directement la qualité du modèle. Garbage in, garbage out.

---

## Types de datasets

|Type|Description|Exemple|
|---|---|---|
|**Tabular**|Lignes × colonnes, comme un tableur|Logs réseau, données clients|
|**Image**|Arrays de pixels|Photos, byteplots de malwares|
|**Text**|Données non structurées|SMS, articles, tweets|
|**Time Series**|Points séquentiels dans le temps|Trafic réseau, prix d'actions|

---

## Ce qui fait un bon dataset

| Attribut               | Ce qu'il signifie                                                                                                   |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------- |
| **Relevance**          | Les données sont liées au problème — du texte de tweets pour analyser le sentiment, pas des cours boursiers         |
| **Completeness**       | Peu de valeurs manquantes — les gérer par imputation si nécessaire                                                  |
| **Consistency**        | Formats uniformes — ex : toutes les dates en `YYYY-MM-DD`                                                           |
| **Quality**            | Données exactes, sans erreurs de saisie ou transmission                                                             |
| **Representativeness** | Couvre bien la diversité de la population réelle — un dataset facial doit inclure différentes ethnies, âges, genres |
| **Balance**            | Classes équilibrées pour la classification — sinon le modèle ignore les classes minoritaires                        |
| **Size**               | Assez grand pour capturer la complexité du problème                                                                 |

---

## Exploration d'un dataset avec pandas

```python
import pandas as pd

data = pd.read_csv("./dataset.csv")   # charger

data.head()                           # voir les premières lignes
data.info()                           # types de colonnes + nb de non-null
data.isnull().sum()                   # compter les valeurs manquantes par colonne
```

**Workflow de base :**

1. `head()` → premier aperçu, détecte les problèmes évidents
2. `info()` → types de données, colonnes incomplètes
3. `isnull().sum()` → prioriser le nettoyage

---

## Challenges courants à anticiper

- **Mix numérique / catégoriel** → encoder les catégories avant entraînement
- **Valeurs manquantes** → imputation (mean, median) ou suppression
- **Strings dans colonnes numériques** → convertir ou supprimer
- **Labels invalides** → ex : `?` ou `-1` dans une colonne cible → standardiser

Identifier ces problèmes **avant** d'entraîner — les corriger après est bien plus coûteux.