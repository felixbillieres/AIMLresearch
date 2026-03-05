# Spam Dataset — Cheat Sheet

**Dataset :** SMS Spam Collection — 5 574 SMS annotés `ham` (légitime) ou `spam`. Format TSV.

---

## Pipeline complet

### 1. Télécharger et extraire

```python
import requests, zipfile, io, os

url = "https://archive.ics.uci.edu/static/public/228/sms+spam+collection.zip"
response = requests.get(url)

with zipfile.ZipFile(io.BytesIO(response.content)) as z:
    z.extractall("sms_spam_collection")

print(os.listdir("sms_spam_collection"))   # vérifier l'extraction
```

### 2. Charger

```python
import pandas as pd

df = pd.read_csv(
    "sms_spam_collection/SMSSpamCollection",
    sep="\t",           # fichier tab-séparé
    header=None,        # pas de ligne d'en-tête
    names=["label", "message"]
)
```

### 3. Inspecter

```python
df.head()              # premières lignes
df.describe()          # statistiques descriptives
df.info()              # types + nb non-null par colonne
df.isnull().sum()      # valeurs manquantes
df.duplicated().sum()  # doublons
```

### 4. Nettoyer

```python
df = df.drop_duplicates()
```

---

## Points clés du dataset

- **ham** = messages légitimes (contacts, newsletters utiles)
- **spam** = contenu non sollicité, potentiellement malveillant
- Dataset **déséquilibré** — vérifier la proportion ham/spam avant d'entraîner
- Pas de header dans le fichier → spécifier `header=None` et `names=[...]`

```
 @felix  python3 spamdetection.py        
['readme', 'SMSSpamCollection']
-------------------------------
<class 'pandas.DataFrame'>
RangeIndex: 5572 entries, 0 to 5571
Data columns (total 2 columns):
 #   Column   Non-Null Count  Dtype
---  ------   --------------  -----
 0   label    5572 non-null   str  
 1   message  5572 non-null   str  
dtypes: str(2)
memory usage: 87.2 KB
(venv)
```