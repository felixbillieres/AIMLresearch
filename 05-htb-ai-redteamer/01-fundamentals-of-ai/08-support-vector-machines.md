# Support Vector Machines (SVM) — Cheat Sheet

**Idée centrale :** Trouver la frontière qui sépare les classes avec le **maximum d'espace** des deux côtés.

> Ex : Classifier des emails spam/non-spam en trouvant la ligne qui s'éloigne le plus possible des deux groupes.

---

## Concepts clés

|Concept|Description|
|---|---|
|**Hyperplane**|La frontière de décision : une ligne en 2D, un plan en 3D, un hyperplan en nD — définie par `w * x + b = 0`|
|**Margin**|Distance entre l'hyperplan et les points les plus proches de chaque classe → on veut la **maximiser**|
|**Support Vectors**|Les points les plus proches de l'hyperplan → ce sont eux qui définissent et "supportent" la frontière|

> Plus la marge est grande, plus le modèle est robuste au bruit et généralise bien.

---

## Linear vs Non-Linear SVM

|Linear SVM|Non-Linear SVM|
|---|---|---|
|**Quand l'utiliser**|Données séparables par une droite|Patterns complexes, données mélangées|
|**Frontière**|Droite / hyperplan|Courbe, forme complexe|
|**Technique**|Optimisation directe|Kernel trick|

---

## Kernel Trick

Quand les données ne sont pas séparables en 2D, on les projette dans un espace de dimension supérieure où elles **deviennent** séparables.

> Analogie : des billes rouges/bleues mélangées sur une table → si on en soulève certaines (3D), on peut passer un plan entre les deux groupes.

|Kernel|Principe|Idéal pour|
|---|---|---|
|**Polynomial**|Ajoute des termes x², x³... → courbe la frontière|Relations modérément non-linéaires|
|**RBF (Gaussian)**|Fonction gaussienne → capture des patterns très complexes|Usage général, très populaire|
|**Sigmoid**|Similaire à la fonction logistique|Cas proches de la régression logistique|

---

## Optimisation

```
Minimiser : 1/2 ||w||²
Contrainte : yi(w * xi + b) >= 1 pour tout i
```

→ Minimiser `||w||` = maximiser la marge, tout en classifiant correctement chaque point.

---

## Points forts vs autres algos

||SVM|Decision Tree|Logistic Regression|
|---|---|---|---|
|Données haute dimension|Excellent|Moyen|Moyen|
|Relations non-linéaires|Oui (kernel)|Oui|Non|
|Sensible aux outliers|Peu|Peu|Plus sensible|
|Distribution requise|Aucune|Aucune|Quelques hypothèses|