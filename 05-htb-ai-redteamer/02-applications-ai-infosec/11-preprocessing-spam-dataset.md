# Spam Dataset — Preprocessing Pipeline

**Objectif :** Transformer les SMS bruts en texte normalisé et vectorisable pour Naive Bayes.

---

## Pipeline complet — 6 étapes

```python
import re, nltk
from nltk.tokenize import word_tokenize
from nltk.corpus import stopwords
from nltk.stem import PorterStemmer

nltk.download("punkt")
nltk.download("punkt_tab")
nltk.download("stopwords")
```

### 1. Lowercase

```python
df["message"] = df["message"].str.lower()
```

→ "FREE" et "free" = même token. Réduit la dimensionnalité.

### 2. Supprimer ponctuation & chiffres

```python
df["message"] = df["message"].apply(lambda x: re.sub(r"[^a-z\s$!]", "", x))
```

→ On garde `$` et `!` — pertinents pour détecter le spam ("WIN $1000!!!").

### 3. Tokenisation

```python
df["message"] = df["message"].apply(word_tokenize)
```

→ `"free money"` → `["free", "money"]`

### 4. Supprimer les stop words

```python
stop_words = set(stopwords.words("english"))
df["message"] = df["message"].apply(lambda x: [w for w in x if w not in stop_words])
```

→ Supprime "the", "is", "and"... — mots sans valeur discriminante.

### 5. Stemming

```python
stemmer = PorterStemmer()
df["message"] = df["message"].apply(lambda x: [stemmer.stem(w) for w in x])
```

→ "running", "runs", "runner" → "run". Réduit le vocabulaire.

### 6. Rejoindre en string

```python
df["message"] = df["message"].apply(lambda x: " ".join(x))
```

→ Requis pour TF-IDF et CountVectorizer qui attendent du texte brut.

---

## Pourquoi chaque étape ?

|Étape|Problème résolu|
|---|---|
|Lowercase|Évite les doublons "Free" / "free"|
|Nettoyage|Réduit le bruit, garde les symboles utiles|
|Tokenisation|Prépare pour les opérations mot par mot|
|Stop words|Élimine les mots sans pouvoir discriminant|
|Stemming|Consolide les variantes d'un même mot|
|Rejoin|Compatible avec les vectorizers scikit-learn|