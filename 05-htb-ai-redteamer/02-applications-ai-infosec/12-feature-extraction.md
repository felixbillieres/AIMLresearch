# Feature Extraction (Text → Vecteurs) — Cheat Sheet

**Idée centrale :** Les modèles ML ne peuvent pas lire du texte — on le convertit en matrice numérique via un **bag-of-words** : chaque message devient un vecteur de comptage de termes.

---

## CountVectorizer — le code

```python
from sklearn.feature_extraction.text import CountVectorizer

vectorizer = CountVectorizer(
    min_df=1,           # terme doit apparaître dans au moins 1 doc
    max_df=0.9,         # exclure les termes dans >90% des docs (trop communs)
    ngram_range=(1, 2)  # unigrams + bigrams
)

X = vectorizer.fit_transform(df["message"])          # matrice features
y = df["label"].apply(lambda x: 1 if x == "spam" else 0)  # labels numériques
```

---

## Comment ça marche — 3 étapes

**1. Tokenisation** → découpe le texte selon `ngram_range`

- `(1,1)` → mots individuels : `["free", "prize"]`
- `(1,2)` → mots + paires : `["free", "prize", "free prize"]`

**2. Construction du vocabulaire** → filtrage via `min_df` / `max_df`

- Trop rare (`min_df`) → bruit, pas représentatif
- Trop fréquent (`max_df`) → pas discriminant (ex: "the" dans 95% des docs → supprimé)

**3. Vectorisation** → chaque message = vecteur de comptages

```
"free prize" → [0, 0, 1, 1, 0, ...]
                         ↑  ↑
                      free  prize
```

---

## Unigrams vs Bigrams — pourquoi les deux ?

| Unigrams seuls            | + Bigrams        |             |
| ------------------------- | ---------------- | ----------- |
| "free" dans un spam       | ✓ détecté        | ✓ détecté   |
| "free prize" (combo spam) | ✗ contexte perdu | ✓ capturé   |
| Taille du vocabulaire     | Petite           | Plus grande |

Le bigram `free prize` est bien plus discriminant que `free` seul — un message légitime peut contenir "free" sans être du spam.

---

## Ce que CountVectorizer ne préserve pas

L'ordre global des mots est perdu — `"I won a prize"` et `"a prize I won"` produisent le même vecteur. Seules les paires locales (bigrams) donnent un peu de contexte d'ordre.

Pour préserver l'ordre complet → TF-IDF ou embeddings (Word2Vec, BERT).