# Anomaly Detection — Cheat Sheet

**Idée centrale :** Identifier les points qui dévient significativement du comportement normal, sans labels prédéfinis.

> Ex : Un système de sécurité qui apprend les horaires normaux d'un bâtiment et sonne l'alarme si quelqu'un entre à 3h du matin.

---

## 3 types d'anomalies

| Type           | Description                                                         | Exemple                                                   |
| -------------- | ------------------------------------------------------------------- | --------------------------------------------------------- |
| **Point**      | Un point isolé qui sort de la norme                                 | Transaction bancaire 10x plus élevée que d'habitude       |
| **Contextuel** | Normal en soi, mais anormal dans son contexte                       | 30°C → normal en été, anomalie en hiver                   |
| **Collectif**  | Un groupe de points normaux individuellement, mais anormal ensemble | Vague de tentatives de connexion depuis des IPs inconnues |

---

## 3 familles de méthodes

| Famille              | Principe                                                                        | Exemples                             |
| -------------------- | ------------------------------------------------------------------------------- | ------------------------------------ |
| **Statistique**      | Les points normaux suivent une distribution connue → les outliers s'en écartent | Z-score, boxplot                     |
| **Clustering**       | Les outliers n'appartiennent à aucun cluster ou à un cluster très petit         | K-Means, DBSCAN                      |
| **Machine Learning** | Apprendre les patterns normaux, flaguer ce qui ne correspond pas                | One-Class SVM, Isolation Forest, LOF |

---

## Algorithmes ML clés

### One-Class SVM

Trace une frontière autour des données normales → tout ce qui est en dehors = anomalie. Supporte les relations non-linéaires via des kernels (comme les SVM classiques).

> Analogie : une clôture autour d'un troupeau — tout mouton hors de la clôture est suspect.

---

### Isolation Forest

Isole les points en partitionnant aléatoirement les données. Les anomalies sont isolées **plus rapidement** (chemin plus court dans l'arbre).

```
score(x) = 2^( -E(h(x)) / c(n) )
```

- Score proche de **1** → probablement une anomalie
- Score proche de **0.5** → probablement normal

> Analogie : "20 questions" — si tu identifies un objet en 2 questions, c'est qu'il est très différent des autres.

---

### Local Outlier Factor (LOF)

Compare la **densité locale** d'un point à celle de ses voisins. Un point dans une zone beaucoup moins dense que ses voisins est un outlier.

```
LOF(p) = densité moyenne des k voisins / densité de p
```

- Score **élevé** → densité locale faible par rapport aux voisins → outlier
- Score **proche de 1** → densité similaire aux voisins → normal

> Analogie : une maison isolée dans une zone peu habitée, entourée de quartiers denses — elle ressort immédiatement.

---

## Hypothèses à garder en tête

| Hypothèse                             | Détail                                                                       |
| ------------------------------------- | ---------------------------------------------------------------------------- |
| **Distribution des données normales** | Certaines méthodes (z-score) supposent une distribution gaussienne           |
| **Choix des features**                | Des features non pertinentes dégradent fortement les résultats               |
| **Données labellisées**               | Certaines méthodes ML supervisées en ont besoin — les méthodes ci-dessus non |