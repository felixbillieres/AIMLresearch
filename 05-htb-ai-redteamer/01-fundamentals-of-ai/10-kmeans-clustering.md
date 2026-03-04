# K-Means Clustering — Cheat Sheet

**Idée centrale :** Partitionner un dataset en K groupes, en minimisant la distance des points à leur centre de cluster.

> Ex : Segmenter des clients en groupes selon leur comportement d'achat pour du marketing ciblé.

---

## Algorithme — 4 étapes

|Étape|Action|
|---|---|
|1. **Init**|Choisir K points aléatoires comme centres initiaux (centroids)|
|2. **Assign**|Chaque point rejoint le centroid le plus proche (distance euclidienne)|
|3. **Update**|Recalculer chaque centroid = moyenne de tous les points du cluster|
|4. **Itérer**|Répéter 2 et 3 jusqu'à ce que les centroids ne bougent plus|

---

## Distance Euclidienne

```
d(x, y) = sqrt(Σ (xi - yi)²)
```

→ Distance en ligne droite entre deux points dans un espace à n dimensions.

---

## Choisir le bon K

|Méthode|Comment ça marche|Lire le résultat|
|---|---|---|
|**Elbow Method**|Tracer WCSS (variance intra-cluster) en fonction de K → chercher le "coude" où la courbe s'aplatit|Le coude = bon compromis entre précision et complexité|
|**Silhouette Analysis**|Pour chaque point, score entre -1 et 1 selon s'il est bien placé dans son cluster|Score proche de 1 = bien placé, 0 = frontière, -1 = mal classé → choisir le K avec le score moyen le plus élevé|

> En pratique, combiner les deux méthodes + le contexte métier (ex: combien de segments marketing peut-on gérer ?).

---

## Hypothèses & Limites

|Hypothèse|Conséquence si violée|
|---|---|
|**Clusters sphériques et taille similaire**|Mauvaises performances sur des formes complexes ou des clusters très inégaux|
|**Features à la même échelle**|Une feature avec de grandes valeurs domine → toujours standardiser avant|
|**Pas d'outliers**|Les outliers tirent les centroids vers eux et faussent les clusters|