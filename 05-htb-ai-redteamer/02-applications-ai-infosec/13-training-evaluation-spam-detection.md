# Spam Classifier — Training & Evaluation

---

## Pipeline + GridSearchCV

```python
from sklearn.pipeline import Pipeline
from sklearn.naive_bayes import MultinomialNB
from sklearn.model_selection import GridSearchCV

# Pipeline : vectorisation → classification en une seule étape
pipeline = Pipeline([
    ("vectorizer", vectorizer),
    ("classifier", MultinomialNB())
])

# GridSearch : trouver le meilleur alpha (smoothing factor)
# alpha évite les probabilités nulles pour les mots jamais vus
param_grid = {"classifier__alpha": [0.01, 0.1, 0.15, 0.2, 0.25, 0.5, 0.75, 1.0]}

grid_search = GridSearchCV(pipeline, param_grid, cv=5, scoring="f1")
grid_search.fit(df["message"], y)

best_model = grid_search.best_estimator_
print("Best params:", grid_search.best_params_)
```

**Pourquoi F1 comme scoring ?** — Le dataset est déséquilibré (plus de ham que spam) → l'accuracy seule serait trompeuse.

---

## Évaluation sur nouveaux messages

```python
# 1. Préprocesser avec la même fonction qu'à l'entraînement
def preprocess_message(message):
    message = message.lower()
    message = re.sub(r"[^a-z\s$!]", "", message)
    tokens = word_tokenize(message)
    tokens = [w for w in tokens if w not in stop_words]
    tokens = [stemmer.stem(w) for w in tokens]
    return " ".join(tokens)

processed_messages = [preprocess_message(msg) for msg in new_messages]

# 2. Vectoriser avec le même vectorizer que l'entraînement
X_new = best_model.named_steps["vectorizer"].transform(processed_messages)

# 3. Prédire
predictions = best_model.named_steps["classifier"].predict(X_new)
probas = best_model.named_steps["classifier"].predict_proba(X_new)

# 4. Afficher
for i, msg in enumerate(new_messages):
    label = "Spam" if predictions[i] == 1 else "Not-Spam"
    print(f"Message: {msg}")
    print(f"Prediction: {label} | Spam: {probas[i][1]:.2f} | Ham: {probas[i][0]:.2f}")
    print("-" * 50)
```

**Règle critique :** Toujours appliquer **exactement** le même preprocessing et le même vectorizer sur les nouvelles données — sinon les features ne correspondent plus au modèle entraîné.

---

## Sauvegarder et recharger le modèle

```python
import joblib

# Sauvegarder
joblib.dump(best_model, 'spam_detection_model.joblib')

# Recharger et prédire
loaded_model = joblib.load('spam_detection_model.joblib')
predictions = loaded_model.predict([preprocess_message(msg) for msg in new_messages])
```

`joblib` sérialise l'objet complet (paramètres appris + config) → pas besoin de réentraîner à chaque redémarrage.

---

## Résumé du workflow complet

```
SMS brut
  → preprocess_message()       # lowercase, nettoyage, tokenisation, stemming
  → CountVectorizer             # texte → matrice de counts
  → MultinomialNB               # prédiction + probabilités
  → "Spam" / "Not-Spam"
```