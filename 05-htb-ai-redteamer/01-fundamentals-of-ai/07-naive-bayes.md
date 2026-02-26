# Naive Bayes — Cheat Sheet

**Idée centrale :** Classifier en calculant la probabilité qu'un point appartienne à une classe, en se basant sur ses features et des probabilités connues à l'avance.

> Ex : Si un email contient "gratuit" et "urgent", quelle est la probabilité que ce soit un spam ?

---

## Bayes' Theorem

```
P(A|B) = [P(B|A) * P(A)] / P(B)
```

| Terme     | Nom            | Signification                                                                   |
| --------- | -------------- | ------------------------------------------------------------------------------- |
| `P(A\|B)` | **Posterior**  | Proba de A sachant que B s'est produit → ce qu'on cherche                       |
| `P(B\|A)` | **Likelihood** | Proba d'observer B si A est vrai → ex: proba de tester positif si malade        |
| `P(A)`    | **Prior**      | Proba de base de A avant toute observation → ex: 1% de la population est malade |
| `P(B)`    | **Evidence**   | Proba globale d'observer B → sert à normaliser le résultat                      |

> Exemple concret : test médical à 95% de précision, maladie rare à 1% → un test positif ne donne que ~16% de chance d'être réellement malade. Le prior faible "dilue" la précision du test.

---

## Comment ça marche

| Étape             | Action                                                                                             |
| ----------------- | -------------------------------------------------------------------------------------------------- |
| 1. **Prior**      | Calculer la proba de base de chaque classe → ex: 20% des emails sont des spams                     |
| 2. **Likelihood** | Pour chaque feature, calculer sa proba selon la classe → ex: "gratuit" apparaît dans 80% des spams |
| 3. **Bayes**      | Combiner prior + likelihoods pour obtenir la proba de chaque classe                                |
| 4. **Prédiction** | Assigner la classe avec la proba la plus haute                                                     |

**Hypothèse "naive" :** Les features sont supposées indépendantes entre elles. En réalité c'est rarement vrai, mais le modèle fonctionne quand même bien en pratique.

---

## Types de Naive Bayes

| Type            | Features                        | Exemple d'usage                                              |
| --------------- | ------------------------------- | ------------------------------------------------------------ |
| **Gaussian**    | Continues, distribution normale | Prédire un achat selon âge + revenu                          |
| **Multinomial** | Discrètes (fréquences)          | Filtrage spam → fréquence de mots comme "gratuit", "argent"  |
| **Bernoulli**   | Binaires (présent / absent)     | Classification de documents → le mot est-il présent ou non ? |

---

## Hypothèses

|Hypothèse|Détail|
|---|---|
|**Indépendance des features**|Hypothèse centrale — rarement vraie mais tolérée|
|**Distribution des données**|Choisir le bon type (Gaussian / Multinomial / Bernoulli) selon la nature des features|
|**Données suffisantes**|Nécessaire pour estimer des probabilités fiables|