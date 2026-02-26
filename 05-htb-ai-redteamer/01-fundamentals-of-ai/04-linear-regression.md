# Linear Regression — Cheat Sheet

**Idée centrale :** Tracer la droite qui prédit le mieux une valeur continue à partir d'une ou plusieurs variables.

> Ex : plus une maison est grande → plus son prix est élevé. La régression linéaire quantifie cette relation.
---
## Formules

|Type|Équation|Quand l'utiliser|
|---|---|---|
|Simple (1 variable)|`y = mx + c`|Prix d'une maison selon sa taille uniquement|
|Multiple (n variables)|`y = b0 + b1x1 + b2x2 + ... + bnxn`|Prix selon taille + localisation + âge|

- `m` / `b1..n` = poids de chaque variable (ex: chaque m² supplémentaire vaut +500€)
- `c` / `b0` = valeur de base quand toutes les variables = 0
- `y` is the predicted target variable
- `x` is the predictor variable
- `m` is the slope of the line (representing the relationship between x and y)
- `c` is the y-intercept (the value of y when x is 0)
---
## OLS — Ordinary Least Squares

Méthode pour trouver les meilleurs coefficients en **minimisant la somme des erreurs au carré (RSS)**.

> Visuellement : la droite qui minimise l'aire des carrés formés entre chaque point et la droite.

| Étape        | Action                     | Pourquoi                                       |
| ------------ | -------------------------- | ---------------------------------------------- |
| 1. Résidu    | `y_réel - y_prédit`        | Mesure l'écart pour chaque point               |
| 2. Carré     | `résidu²`                  | Élimine les négatifs, pénalise les gros écarts |
| 3. RSS       | Somme de tous les résidus² | Une seule valeur représentant l'erreur globale |
| 4. Minimiser | Ajuster les coefficients   | Trouver la droite la plus précise possible     |

---
## Hypothèses à vérifier avant d'appliquer le modèle

|Hypothèse|Ce que ça signifie|Si violée|
|---|---|---|
|**Linéarité**|La relation X → y est bien une droite|Le modèle rate des patterns non-linéaires|
|**Indépendance**|Les observations ne s'influencent pas entre elles|Ex: données météo jour par jour sont liées → problème|
|**Homoscédasticité**|L'erreur est constante sur toute la plage de valeurs|Le modèle sera moins fiable sur certaines zones|
|**Normalité**|Les erreurs suivent une distribution normale|Les inférences sur les coefficients deviennent invalides|
