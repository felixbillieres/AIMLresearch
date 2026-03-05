# Spam Classification — Cheat Sheet

**Idée centrale :** Appliquer Naive Bayes pour calculer la probabilité qu'un email soit spam en se basant sur ses features (mots, phrases...).

---

## La formule appliquée au spam

```
P(Spam | Features) = [P(Features | Spam) × P(Spam)] / P(Features)
```

|Terme|Signification|
|---|---|
|`P(Spam \| Features)`|Proba que l'email soit spam étant donné ses features → ce qu'on cherche|
|`P(Features \| Spam)`|Proba d'observer ces features dans un spam|
|`P(Spam)`|Proba de base qu'un email soit spam (ex: 30% des emails reçus)|
|`P(Features)`|Proba totale d'observer ces features (spam + non-spam)|

---

## L'hypothèse "naive"

On suppose que chaque feature est **indépendante** des autres. Ce qui simplifie le calcul :

```
P(F1, F2, ... | Spam) = P(F1|Spam) × P(F2|Spam) × ... × P(FN|Spam)
```

---

## Exemple complet

Email avec features F1 et F2. Données connues :

- `P(Spam) = 0.3` / `P(Not Spam) = 0.7`
- `P(F1|Spam) = 0.4` / `P(F2|Spam) = 0.5`
- `P(F1|Not Spam) = 0.2` / `P(F2|Not Spam) = 0.3`

**Étape 1 — Likelihoods :**

```
P(F1,F2 | Spam)     = 0.4 × 0.5 = 0.20
P(F1,F2 | Not Spam) = 0.2 × 0.3 = 0.06
```

**Étape 2 — Evidence (loi des probabilités totales) :**

```
P(F1,F2) = (0.20 × 0.3) + (0.06 × 0.7) = 0.06 + 0.042 = 0.102
```

**Étape 3 — Posteriors :**

```
P(Spam     | F1,F2) = (0.20 × 0.3) / 0.102 ≈ 0.588
P(Not Spam | F1,F2) = (0.06 × 0.7) / 0.102 ≈ 0.412
```

**Décision : 0.588 > 0.412 → Spam ✓**

---

## À retenir

On ne compare pas directement les features — on compare les **probabilités postérieures** des deux classes. La classe avec la probabilité la plus haute gagne.

En pratique avec scikit-learn, tout ce calcul est fait automatiquement par `MultinomialNB` ou `BernoulliNB` — mais comprendre la mécanique permet de debugger et d'interpréter les résultats.