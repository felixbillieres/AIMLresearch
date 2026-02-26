# Logistic Regression — Cheat Sheet

**Idée centrale :** Malgré son nom, c'est un algorithme de **classification**, pas de régression. Il prédit la **probabilité** qu'un point appartienne à une classe (0 ou 1).

> Ex : est-ce que cet email est un spam ? Est-ce que ce client va cliquer ?

---

## Linear vs Logistic Regression
| Linear Regression | Logistic Regression            |                               |
| ----------------- | ------------------------------ | ----------------------------- |
| **Output**        | Valeur continue (ex: 450 000€) | Probabilité entre 0 et 1      |
| **But**           | Prédire un nombre              | Classifier dans une catégorie |
| **Fonction**      | Droite `y = mx + c`            | Courbe S (sigmoid)            |

---

## Fonction Sigmoid

Transforme n'importe quelle valeur en probabilité entre 0 et 1.

```
P(x) = 1 / (1 + e^-z)
```

- `z` = combinaison linéaire des features : `m1x1 + m2x2 + ... + c`
- Résultat proche de 0 → classe négative
- Résultat proche de 1 → classe positive

---

## Decision Boundary & Threshold

| Concept               | Description                             | Exemple                                |
| --------------------- | --------------------------------------- | -------------------------------------- |
| **Threshold**         | Seuil de décision (défaut = 0.5)        | P > 0.5 → spam                         |
| **Decision Boundary** | Ligne/plan séparant les deux classes    | Frontière spam / pas spam              |
| **Hyperplane**        | Version n-dimensionnelle de la boundary | Avec 10 features → hyperplan à 10 dims |

> Ajuster le threshold selon le contexte : un filtre médical préférera moins de faux négatifs → threshold plus bas.

---

## Hypothèses à vérifier

|Hypothèse|Ce que ça signifie|
|---|---|
|**Binary outcome**|La cible n'a que 2 valeurs possibles (0/1)|
|**Linéarité des log-odds**|Relation linéaire entre les features et le log des probabilités|
|**Pas de multicolinéarité**|Les features ne doivent pas être trop corrélées entre elles|
|**Large dataset**|Plus de données = estimation des paramètres plus fiable|