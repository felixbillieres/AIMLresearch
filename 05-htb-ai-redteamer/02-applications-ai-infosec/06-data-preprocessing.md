# Data Preprocessing — Cheat Sheet

**Idée centrale :** Transformer les données brutes en un format propre et exploitable avant d'entraîner un modèle. Les données invalides ou manquantes biaiseront les résultats.

---

## Les 4 étapes du preprocessing

|Étape|Actions|
|---|---|
|**Cleaning**|Gérer les valeurs manquantes, supprimer les doublons, lisser le bruit|
|**Transformation**|Normaliser, encoder, scaler, réduire la dimensionnalité|
|**Integration**|Fusionner des données provenant de sources multiples|
|**Formatting**|Convertir les types, reshaper les structures|

---

## Détecter les valeurs invalides

```python
import re

# IP invalides
def is_valid_ip(ip):
    pattern = re.compile(r'^((25[0-5]|2[0-4][0-9]|[01]?\d?\d)\.){3}(25[0-5]|2[0-4]\d|[01]?\d?\d)$')
    return bool(pattern.match(str(ip)))

# Ports invalides (0–65535)
def is_valid_port(port):
    try: return 0 <= int(port) <= 65535
    except: return False

# Protocoles valides
valid_protocols = ['TCP', 'TLS', 'SSH', 'DNS', 'HTTP', 'HTTPS', 'FTP', 'SMTP', 'UDP', 'POP3']
invalid_protocols = data[~data['protocol'].isin(valid_protocols)]

# Valeurs numériques non-négatives
def is_valid_bytes(b):
    try: return int(b) >= 0
    except: return False
```

---

## 2 stratégies pour gérer les invalides

### Option A — Supprimer

Rapide, garantit des données propres. Risqué si le dataset est petit.

```python
data = data.drop(invalid_ips.index, errors='ignore')
data = data.drop(invalid_ports.index, errors='ignore')
# etc.
```

### Option B — Imputer (conserver et corriger)

Remplace les invalides par des valeurs estimées. Préserve plus de données.

**Étape 1 : Standardiser tous les invalides en NaN**

```python
import numpy as np

invalid_tags = ['INVALID_IP', 'MISSING_IP', 'STRING_PORT', 'NON_NUMERIC', '?']
df.replace(invalid_tags, np.nan, inplace=True)
df['destination_port'] = pd.to_numeric(df['destination_port'], errors='coerce')
df['bytes_transferred'] = pd.to_numeric(df['bytes_transferred'], errors='coerce')
```

**Étape 2 : Imputer**

```python
from sklearn.impute import SimpleImputer, KNNImputer

# Simple — médiane pour le numérique, mode pour le catégoriel
num_imputer = SimpleImputer(strategy='median')
cat_imputer = SimpleImputer(strategy='most_frequent')

# Avancé — KNN (tient compte des relations entre features)
knn_imputer = KNNImputer(n_neighbors=5)
df[numeric_cols] = knn_imputer.fit_transform(df[numeric_cols])
```

**Étape 3 : Appliquer la logique métier**

```python
df['source_ip'] = df['source_ip'].fillna('0.0.0.0')
df['destination_port'] = df['destination_port'].clip(lower=0, upper=65535)
df.loc[~df['protocol'].isin(valid_protocols), 'protocol'] = df['protocol'].mode()[0]
```

---

## Vérification finale

```python
print(df.describe(include='all'))   # distributions + valeurs uniques par colonne
print(df.isnull().sum())            # confirmer qu'il ne reste plus de NaN
```

---

## Quand supprimer vs imputer ?

**Supprimer** quand la précision des données est critique et que la perte de quelques lignes est acceptable.

**Imputer** quand le dataset est petit, ou quand les invalides représentent une part significative des données.