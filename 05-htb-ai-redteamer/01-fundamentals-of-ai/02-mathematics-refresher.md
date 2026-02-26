# Maths Refresher — AI

##  Opérations de base

|Symbole|Nom|Exemple|
|---|---|---|
|`*`|Multiplication|`3 * 4 = 12`|
|`/`|Division|`10 / 2 = 5`|
|`+`|Addition|`5 + 3 = 8`|
|`-`|Soustraction|`9 - 4 = 5`|

---

##  Notations algébriques

|Symbole|Nom|Description|Exemple|
|---|---|---|---|
|`x_t`|Indice|Variable à l'instant _t_|`x_t = q(x_t \| x_{t-1})`|
|`x^n`|Exposant|Puissance|`x^2 = x * x`|
|`\|v\|`|Norme L2|Longueur d'un vecteur|`sqrt(v₁² + v₂² + ... + vₙ²)`|
|`\|v\|₁`|Norme L1|Distance Manhattan|`\|v₁\| + \|v₂\| + ... + \|vₙ\|`|
|`\|v\|∞`|Norme L∞|Valeur absolue max|`max(\|v₁\|, ..., \|vₙ\|)`|
|`Σ`|Somme|Somme d'une séquence|`Σᵢ₌₁ⁿ aᵢ = a₁ + a₂ + ... + aₙ`|

---

##  Logarithmes & Exponentielles

|Symbole|Nom|Base|Exemple|
|---|---|---|---|
|`log₂(x)`|Log base 2|2|`log₂(8) = 3`|
|`ln(x)`|Log naturel|_e_|`ln(e²) = 2`|
|`eˣ`|Exponentielle|_e_ ≈ 2.718|`e² ≈ 7.389`|
|`2ˣ`|Exponentielle base 2|2|`2³ = 8`|

---

##  Matrices & Vecteurs

|Symbole|Nom|Description|Exemple|
|---|---|---|---|
|`A * v`|Produit matrice-vecteur|Transformation d'un vecteur|`[[1,2],[3,4]] * [5,6] = [17,39]`|
|`A * B`|Produit matrice-matrice|Composition de transformations|`[[1,2],[3,4]] * [[5,6],[7,8]] = [[19,22],[43,50]]`|
|`Aᵀ`|Transposée|Échange lignes ↔ colonnes|`[[1,2],[3,4]]ᵀ = [[1,3],[2,4]]`|
|`A⁻¹`|Inverse|`A * A⁻¹ = I`|`[[1,2],[3,4]]⁻¹ = [[-2,1],[1.5,-0.5]]`|
|`det(A)`|Déterminant|Scalaire, indique l'inversibilité|`det([[1,2],[3,4]]) = -2`|
|`tr(A)`|Trace|Somme de la diagonale|`tr([[1,2],[3,4]]) = 5`|

---

##  Théorie des ensembles

|Symbole|Nom|Description|Exemple|
|---|---|---|---|
|`\|S\|`|Cardinalité|Nombre d'éléments|`\|{1,2,3,4,5}\| = 5`|
|`A ∪ B`|Union|Éléments dans A **ou** B|`{1,2,3} ∪ {3,4,5} = {1,2,3,4,5}`|
|`A ∩ B`|Intersection|Éléments dans A **et** B|`{1,2,3} ∩ {3,4,5} = {3}`|
|`Aᶜ`|Complémentaire|Éléments **hors** de A|`U={1..5}, A={1,2,3} → Aᶜ={4,5}`|

---

##  Opérateurs de comparaison

|Symbole|Signification|
|---|---|
|`>=`|Supérieur ou égal|
|`<=`|Inférieur ou égal|
|`==`|Égalité|
|`!=`|Différent|

---

##  Valeurs propres (Eigenvalues)

|Symbole|Nom|Description|
|---|---|---|
|`λ`|Valeur propre|Scalaire tel que `A * v = λ * v`|
|`v`|Vecteur propre|Vecteur non-nul associé à `λ`|

> Utilisés dans PCA, réduction dimensionnelle, transformations linéaires.

---

##  Probabilités & Statistiques

|Symbole|Nom|Formule|Usage|
|---|---|---|---|
|`P(x \| y)`|Proba conditionnelle|`P(Output \| Input)`|Inférence bayésienne|
|`E[X]`|Espérance|`Σ xᵢ P(xᵢ)`|Valeur moyenne|
|`Var(X)`|Variance|`E[(X - E[X])²]`|Dispersion|
|`σ(X)`|Écart-type|`sqrt(Var(X))`|Dispersion (même unité)|
|`Cov(X,Y)`|Covariance|`E[(X-E[X])(Y-E[Y])]`|Relation entre deux variables|
|`ρ(X,Y)`|Corrélation|`Cov(X,Y) / (σ(X) * σ(Y))`|Relation linéaire normalisée ∈ [-1, 1]|

---

## Fonctions utilitaires

|Symbole|Nom|Exemple|
|---|---|---|
|`max(...)`|Maximum|`max(4,7,2) = 7`|
|`min(...)`|Minimum|`min(4,7,2) = 2`|
|`1/x`|Réciproque|`1/5 = 0.2`|
|`f(x)`|Notation fonctionnelle|`f(x) = x² + 2x + 1`|
|`...`|Ellipse|Continuation d'une séquence|
