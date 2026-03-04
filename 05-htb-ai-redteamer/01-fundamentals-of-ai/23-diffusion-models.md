# Diffusion Models — Cheat Sheet

**Idée centrale :** Générer des images en apprenant à inverser un processus de dégradation — on ajoute du bruit progressivement jusqu'à obtenir du bruit pur, puis on entraîne le modèle à faire le chemin inverse.

> Ex : Partir d'une photo nette, la brouiller en 100 étapes jusqu'au bruit total, puis apprendre à reconstruire une image depuis ce bruit.

---

## Les deux processus

**Forward (bruitage)** — On ajoute progressivement du bruit gaussien à l'image originale jusqu'à obtenir du bruit pur. C'est déterministe et ne s'entraîne pas.

```
Image nette (x₀) → bruit partiel (x₁) → ... → bruit pur (xT)
```

**Reverse (débruitage)** — Un réseau de neurones apprend à prédire le bruit ajouté à chaque étape, pour pouvoir remonter de xT vers x₀.

```
Bruit pur (xT) → débruitage progressif → ... → image générée (x₀)
```

---

## Ce que le modèle apprend

Le réseau de débruitage (CNN ou Transformer) reçoit une image bruitée `x_t` et prédit le bruit `ε` qui a été ajouté. L'objectif d'entraînement est simple :

```
L = E[ || ε - ε_pred ||² ]
```

→ Minimiser l'écart entre le bruit réel et le bruit prédit, à chaque étape.

---

## Génération depuis un prompt texte

Pour conditionner la génération sur du texte (ex : "un chat avec un chapeau") :

1. **Text Encoding** — Le prompt est encodé en vecteur via un Transformer ou CLIP
2. **Conditioning** — Ce vecteur guide le réseau de débruitage à chaque étape
3. **Sampling** — On part de bruit pur, et on débruite en tenant compte du texte
4. **Output** — Après T étapes, l'image finale correspond au prompt

---

## Noise Schedule

Détermine combien de bruit est ajouté à chaque étape. Un schedule linéaire typique :

```
β_t = β_min + (t / T) × (β_max - β_min)
```

Un bon schedule est crucial — trop de bruit trop vite et le modèle ne peut pas apprendre à débruiter proprement.

---

## Diffusion vs autres modèles génératifs

| GAN                        | VAE                          | Diffusion                          |                                |
| -------------------------- | ---------------------------- | ---------------------------------- | ------------------------------ |
| **Principe**               | Générateur vs Discriminateur | Encodage → Latent space → Décodage | Bruitage → Débruitage itératif |
| **Qualité d'image**        | Très bonne                   | Correcte                           | État de l'art                  |
| **Stabilité entraînement** | Instable (mode collapse)     | Stable                             | Stable                         |
| **Vitesse de génération**  | Rapide                       | Rapide                             | Lent (T étapes)                |

---

## Hypothèses clés

**Markov Property** — Chaque étape ne dépend que de l'étape précédente, pas de tout l'historique.

**Distribution statique** — Le dataset d'entraînement est fixe, la distribution ne change pas pendant l'entraînement.

**Smoothness** — De petits changements dans l'input produisent de petits changements dans l'output — facilite l'apprentissage de la structure des données.