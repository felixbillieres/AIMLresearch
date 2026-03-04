# Data Transformation — Cheat Sheet

**Idée centrale :** Convertir les données dans un format que les algos ML peuvent exploiter efficacement — encoder les catégories, corriger les distributions skewed, et diviser proprement le dataset.

---

## Encoding — catégoriel → numérique

|Méthode|Quand l'utiliser|Attention|
|---|---|---|
|**OneHotEncoder**|Catégories sans ordre naturel (ex: protocole réseau)|Augmente le nb de features|
|**LabelEncoder**|Catégories avec ordre implicite|Peut introduire un ordre artificiel|
|**HashingEncoder**|Très haute cardinalité (beaucoup de valeurs uniques)|Perte d'interprétabilité|

**One-Hot Encoding en pratique :**

```python
from sklearn.preprocessing import OneHotEncoder

encoder = OneHotEncoder(handle_unknown='ignore', sparse_output=False)
encoded = encoder.fit_transform(df[['protocol']])

encoded_df = pd.DataFrame(encoded, columns=encoder.get_feature_names_out(['protocol']))
df = pd.concat([df.drop('protocol', axis=1), encoded_df], axis=1)
```

→ La colonne `protocol` avec valeurs `TCP/HTTP/SSH` devient 3 colonnes binaires `protocol_TCP`, `protocol_HTTP`, `protocol_SSH`.

---

## Gérer les distributions skewed

Quand une feature a quelques valeurs extrêmes qui écrasent le reste, les modèles peinent à capturer les patterns des valeurs normales.

**Solution : log transform**

```python
import numpy as np

df["bytes_transferred"] = np.log1p(df["bytes_transferred"])  # +1 pour éviter log(0)
```

`log1p` compresse les grandes valeurs plus que les petites → distribution plus équilibrée, modèle moins sensible aux outliers.

---

## Data Splitting — les 3 subsets

|Subset|Usage|Proportion typique|
|---|---|---|
|**Train**|Entraîner le modèle|60–80%|
|**Validation**|Tuner les hyperparamètres, comparer des modèles|10–20%|
|**Test**|Évaluation finale — ne jamais toucher avant la fin|10–20%|

```python
from sklearn.model_selection import train_test_split

X = df.drop("threat_level", axis=1)
y = df["threat_level"]

# Split 1 : 80% train+val / 20% test
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=1337)

# Split 2 : sur les 80%, garder 75% train / 25% val
# → 0.8 × 0.75 = 60% train final, 0.8 × 0.25 = 20% val
X_train, X_val, y_train, y_val = train_test_split(X_train, y_train, test_size=0.25, random_state=1337)
```

**Workflow :**

1. Entraîner sur `X_train`
2. Tuner sur `X_val`
3. Évaluer une seule fois sur `X_test`

> Ne jamais utiliser le test set pendant le développement — il doit rester "invisible" pour simuler des données réelles inédites.