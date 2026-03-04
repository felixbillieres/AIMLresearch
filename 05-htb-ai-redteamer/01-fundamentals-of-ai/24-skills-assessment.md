# Quiz — Questions & Réponses

---

## Q1 — Quel algorithme probabiliste basé sur le théorème de Bayes est couramment utilisé pour la classification (spam, sentiment) ?

**Naive Bayes**

Naive Bayes applique le théorème de Bayes pour calculer la probabilité qu'un point appartienne à une classe donnée ses features :

```
P(A|B) = [P(B|A) × P(A)] / P(B)
```

Il est dit "naive" car il suppose que toutes les features sont **indépendantes** entre elles — hypothèse rarement vraie en pratique, mais qui fonctionne étonnamment bien. Sa simplicité et sa rapidité en font un choix populaire pour le filtrage de spam (fréquence de mots) et l'analyse de sentiment.

---

## Q2 — Quelle technique de réduction de dimensionnalité transforme des données en haute dimension en une représentation plus compacte tout en préservant le maximum d'information ?

**PCA — Principal Component Analysis**

PCA identifie les **directions de variance maximale** dans les données (appelées composantes principales) et projette les données sur un sous-espace de dimension inférieure défini par ces directions.

Le processus : standardiser → calculer la matrice de covariance → extraire les eigenvectors/eigenvalues → sélectionner les k composantes avec les eigenvalues les plus élevées → projeter (`Y = X × V`).

Utilisé pour la visualisation de données, l'extraction de features, et la réduction du bruit. Requiert que les données soient standardisées et que les relations entre features soient linéaires.

---

## Q3 — Quel algorithme RL model-free apprend une politique optimale en estimant la Q-value — le gain cumulé attendu pour une action donnée dans un état donné ?

**Q-Learning**

Q-Learning maintient une **Q-table** (état × action) et met à jour les Q-values via la formule de Bellman :

```
Q(s, a) = Q(s, a) + α × [r + γ × max Q(s', a') - Q(s, a)]
```

L'agent apprend par essais/erreurs sans modèle de l'environnement. Il choisit ses actions via une stratégie **epsilon-greedy** (exploration vs exploitation) et converge vers la politique optimale. C'est un algorithme **off-policy** : il apprend la valeur de la politique optimale indépendamment de ses actions actuelles.

---

## Q4 — Quelle est l'unité computationnelle fondamentale d'un réseau de neurones qui peut utiliser différentes fonctions d'activation (sigmoid, ReLU, tanh) — contrairement au perceptron limité à une step function ?

**Le Neurone (dans un MLP)**

Un neurone reçoit des inputs, calcule une somme pondérée, ajoute un biais, et applique une fonction d'activation :

```
output = f(Σ(wᵢ × xᵢ) + b)
```

Contrairement au perceptron (output binaire 0/1), un neurone peut utiliser **ReLU** (le plus courant), **sigmoid** (output entre 0 et 1), ou **tanh** (output entre -1 et 1), ce qui lui permet de modéliser des relations non-linéaires et de produire des outputs continus.

---

## Q5 — Quelle architecture deep learning, capable de capturer des dépendances à longue portée via le self-attention, est à la base des LLMs ?

**Le Transformer**

Contrairement aux RNNs qui lisent le texte séquentiellement, le Transformer traite **toute la séquence en parallèle**. Son mécanisme clé, le **self-attention**, calcule un score d'importance entre chaque paire de mots — permettant de comprendre des dépendances distantes ("which" → "mat" dans "the mat, which was blue").

Structure : Tokenization → Embeddings → Encoder (comprend l'input) → Decoder (génère l'output). Les LLMs (GPT, Claude, etc.) sont des Transformers entraînés sur des volumes massifs de texte pour des tâches comme la traduction, la synthèse, les Q&A et l'écriture créative.