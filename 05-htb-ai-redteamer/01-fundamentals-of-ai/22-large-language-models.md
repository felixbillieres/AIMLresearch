# Large Language Models (LLMs) — Cheat Sheet

**Idée centrale :** Des modèles entraînés sur des quantités massives de texte pour comprendre et générer du langage humain — basés sur l'architecture Transformer et son mécanisme d'attention.

---

## Ce qui distingue les LLMs

**Massive Scale** — Des milliards de paramètres, ce qui leur permet de capturer les nuances du langage.

**Few-Shot Learning** — Capables d'apprendre une nouvelle tâche à partir de quelques exemples seulement, sans réentraînement.

**Contextual Understanding** — Comprennent le contexte d'une conversation ou d'un texte pour générer des réponses cohérentes.

---

## Du texte brut à la prédiction — le pipeline

```
Texte brut
   ↓
Tokenization  →  "I love AI"  →  ["I", "love", "AI"]
   ↓
Embeddings    →  Chaque token devient un vecteur numérique
                 (mots similaires = vecteurs proches)
   ↓
Transformer   →  Encoder + Self-Attention + Decoder
   ↓
Output        →  Texte généré token par token
```

---

## L'architecture Transformer

Contrairement aux RNNs qui lisent le texte mot par mot, le Transformer traite **toute la séquence en parallèle** — plus rapide, et capable de capturer des dépendances entre mots distants.

**Self-Attention** — Le mécanisme clé. Pour chaque mot, il calcule un score d'attention avec tous les autres mots de la séquence.

> Ex : Dans "The cat sat on the mat, which was blue", self-attention comprend que "which" se réfère à "mat" malgré la distance.

**Encoder** — Lit et comprend le texte d'entrée, capture les relations entre les mots.

**Decoder** — Génère le texte de sortie en s'appuyant sur ce que l'encodeur a compris.

---

## Entraînement

Les LLMs sont entraînés en **unsupervised learning** sur des volumes massifs de texte. Le modèle apprend à prédire le mot suivant, et ses paramètres sont ajustés via gradient descent pour minimiser l'erreur de prédiction. Cela nécessite du hardware spécialisé (GPUs, TPUs) et des semaines de calcul.

---

## Concepts clés en résumé

|Concept|En une ligne|
|---|---|
|**Tokenization**|Découper le texte en unités (mots, sous-mots, caractères)|
|**Embeddings**|Représentation vectorielle des tokens — mots similaires = vecteurs proches|
|**Self-Attention**|Permet au modèle de pondérer l'importance de chaque mot par rapport aux autres|
|**Encoder**|Comprend l'input|
|**Decoder**|Génère l'output|