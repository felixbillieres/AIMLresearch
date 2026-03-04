# Perceptron — Cheat Sheet

**Idée centrale :** La brique de base d'un réseau de neurones. Un perceptron prend des inputs, les pondère, les somme, et décide d'un output via une fonction d'activation.

> Ex : Décider de jouer au tennis selon la météo — chaque condition météo est un input avec un poids qui reflète son importance.

---

## Structure

```
Inputs (x1, x2, ...) × Poids (w1, w2, ...)
        ↓
   Somme pondérée : Σ(wi × xi)
        ↓
   + Biais (b)
        ↓
   Fonction d'activation f(x)
        ↓
   Output (y)
```

- **Poids** — L'importance de chaque input. Positif = renforce, négatif = inhibe.
- **Biais** — Permet au neurone de s'activer même si tous les inputs sont à 0. Décale le seuil.
- **Activation function** — Introduit la non-linéarité et détermine si le neurone "tire" ou non.

---

## Exemple concret — Jouer au tennis ?

Inputs : Outlook (0.3), Temperature (0.2), Humidity (-0.4), Wind (-0.2), Bias = 0.1

Jour ensoleillé, température douce, humidité faible, vent faible :

```
(0.3×0) + (0.2×1) + (-0.4×0) + (-0.2×0) + 0.1 = 0.3
f(0.3) = 1 → Jouer !
```

---

## Limites du perceptron simple

Un perceptron ne peut apprendre que des **frontières linéaires** — il ne peut pas résoudre des problèmes non-linéairement séparables.

L'exemple classique : le **problème XOR**. Impossible de séparer ses outputs avec une seule droite.

C'est pourquoi on empile plusieurs perceptrons en couches → **réseau de neurones multicouche**, capable de modéliser des patterns non-linéaires.