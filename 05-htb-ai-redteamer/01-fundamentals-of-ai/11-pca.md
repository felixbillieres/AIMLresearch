# Principal Component Analysis (PCA) — Cheat Sheet

**Idée centrale :** Réduire le nombre de dimensions d'un dataset en trouvant les "directions" qui capturent le maximum de variance.

> Ex : Des milliers de pixels d'une image → quelques composantes qui capturent l'essentiel (formes, textures, contours).

---

## 3 concepts clés

|Concept|Rôle dans PCA|
|---|---|
|**Variance**|Ce qu'on veut maximiser — les composantes capturent les directions où les données sont le plus dispersées|
|**Covariance**|Mesure la relation entre deux features — PCA l'utilise pour identifier les directions de variance maximale|
|**Eigenvectors / Eigenvalues**|Eigenvectors = directions des composantes principales. Eigenvalues = quantité de variance expliquée par chaque composante → plus la valeur est grande, plus la composante est importante|

---

## Algorithme — 6 étapes

|Étape|Action|
|---|---|
|1. **Standardiser**|Centrer et réduire chaque feature `(x - mean) / std` — indispensable pour que toutes les features aient le même poids|
|2. **Matrice de covariance**|Calculer les relations entre toutes les paires de features|
|3. **Eigenvectors & Eigenvalues**|Décomposer la matrice de covariance → obtenir les directions + leur importance|
|4. **Trier**|Classer les eigenvectors par eigenvalue décroissante|
|5. **Sélectionner k composantes**|Garder les k premières (celles qui expliquent le plus de variance)|
|6. **Transformer**|Projeter les données sur le nouvel espace : `Y = X * V`|

---

## Choisir le nombre de composantes k

Tracer le **explained variance ratio** cumulatif en fonction du nombre de composantes. → Choisir k tel que la variance cumulée atteigne un seuil acceptable (ex: **95%**).

> Compromis : moins de dimensions = moins d'info, mais modèle plus rapide et plus simple.

---

## Hypothèses & Limites

| Hypothèse       | Détail                                                      |
| --------------- | ----------------------------------------------------------- |
| **Linéarité**   | PCA ne capture que des relations linéaires entre features   |
| **Corrélation** | Fonctionne mieux si les features sont corrélées entre elles |
| **Scale**       | Très sensible à l'échelle → toujours standardiser avant     |
