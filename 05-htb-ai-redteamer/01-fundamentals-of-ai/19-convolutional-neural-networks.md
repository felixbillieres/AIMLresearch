# Convolutional Neural Networks (CNN) — Cheat Sheet

**Idée centrale :** Des réseaux de neurones spécialisés pour les données en grille (images, vidéos), qui apprennent des features de manière hiérarchique — des détails simples vers des concepts complexes.

> Ex : Reconnaître un chat → couche 1 détecte des bords, couche 2 des formes, couche 3 des oreilles et un museau.

---

## Les 3 types de couches

**Convolutional Layer** — Le cœur du CNN. Un filtre glisse sur l'image et calcule un produit scalaire à chaque position → produit une **feature map** qui indique où et à quel degré une feature est présente. Plusieurs filtres = plusieurs features détectées en parallèle.

**Pooling Layer** — Réduit la dimension des feature maps en gardant l'essentiel (max ou moyenne dans une petite fenêtre). Moins coûteux à calculer, plus robuste aux petites variations dans l'image.

**Fully Connected Layer** — Comme un MLP classique. Placé en fin de réseau, il combine toutes les features extraites pour faire la prédiction finale.

```
[Conv] → [Pool] → [Conv] → [Pool] → ... → [Flatten] → [Fully Connected] → Output
```

---

## Hiérarchie des features

| Profondeur             | Ce que la couche apprend                  |
| ---------------------- | ----------------------------------------- |
| Couches initiales      | Features simples : bords, textures, coins |
| Couches intermédiaires | Patterns : courbes, formes géométriques   |
| Couches profondes      | Concepts : roues, visages, objets entiers |

Chaque couche s'appuie sur ce qu'a appris la précédente. C'est cette accumulation qui donne aux CNNs leur puissance.

---

## Principes clés qui font fonctionner les CNNs

**Localité** — Les pixels voisins sont plus corrélés que des pixels distants. Les filtres ne regardent qu'une petite région à la fois (receptive field).

**Stationnarité** — Un bord vertical est un bord vertical, qu'il soit à gauche ou à droite de l'image. Le même filtre est appliqué partout → **weight sharing** → moins de paramètres, plus efficace.

**Hiérarchie spatiale** — Les features se construisent du simple vers le complexe, couche après couche.

---

## Hypothèses & prérequis

- **Données en grille** — Images (H × W × canaux), vidéos (H × W × temps × canaux)
- **Beaucoup de données** — Les CNNs sont gourmands en données labellisées, sinon overfitting
- **Input normalisé** — Pixels ramenés entre [0,1] ou [-1,1] pour un entraînement stable