# Introduction au Deep Learning — Cheat Sheet

**Idée centrale :** Sous-domaine du ML qui utilise des réseaux de neurones à plusieurs couches pour apprendre automatiquement des patterns complexes depuis des données brutes — sans feature engineering manuel.

> Ex : Reconnaître un chat dans une photo sans avoir à définir manuellement ce qu'est une oreille, une moustache, ou une fourrure.

---

## Pourquoi le Deep Learning ?

**Problèmes complexes** — Les algos traditionnels plafonnent sur la reconnaissance d'images, la voix, le langage naturel. Le DL les résout en apprenant des représentations hiérarchiques des données.

**Inspiration du cerveau humain** — Les réseaux de neurones artificiels imitent les connexions neuronales du cerveau : l'information est traitée couche par couche, du plus simple au plus abstrait.

---

## Structure d'un réseau de neurones

```
[Input Layer] → [Hidden Layer 1] → [Hidden Layer 2] → ... → [Output Layer]
```

- **Input Layer** — Reçoit les données brutes (pixels, mots, chiffres...)
- **Hidden Layers** — Extraient des features de plus en plus abstraites à chaque couche
- **Output Layer** — Produit la prédiction finale (classe, valeur, probabilité...)

Plus il y a de couches cachées → plus le réseau est "profond" → plus il peut modéliser des patterns complexes.

---

## Concepts clés

|Concept|Rôle|
|---|---|
|**Poids (Weights)**|Force de chaque connexion entre neurones — c'est ce que le réseau apprend|
|**Activation Function**|Introduit de la non-linéarité pour capturer des patterns complexes|
|**Loss Function**|Mesure l'écart entre prédiction et réalité — l'objectif est de la minimiser|
|**Backpropagation**|Calcule comment ajuster chaque poids pour réduire la loss|
|**Optimizer**|Décide comment appliquer ces ajustements|
|**Hyperparameters**|Paramètres fixés avant l'entraînement (learning rate, nb de couches...)|

---

## Fonctions d'activation

Chaque neurone applique une fonction d'activation à son entrée pour décider si et comment il "s'active".

- **Sigmoid** → output entre 0 et 1 — utile pour les probabilités
- **ReLU** → 0 si négatif, sinon la valeur telle quelle — le plus utilisé en pratique, rapide et efficace
- **Tanh** → output entre -1 et 1 — version centrée de la sigmoid

---

## Comment un réseau apprend

1. Les données passent de l'input à l'output _(forward pass)_
2. La **loss function** mesure l'erreur
3. La **backpropagation** calcule le gradient de chaque poids
4. L'**optimizer** met à jour les poids pour réduire l'erreur
5. On répète jusqu'à convergence

Les optimizers courants : **SGD** (simple, robuste), **Adam** (adaptatif, très utilisé), **RMSprop** (bon pour les données séquentielles).