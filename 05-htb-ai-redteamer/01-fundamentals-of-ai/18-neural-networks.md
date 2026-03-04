# Neural Networks (MLP) — Cheat Sheet

**Idée centrale :** Empiler plusieurs couches de neurones pour apprendre des patterns non-linéaires complexes — là où le perceptron simple échoue.

---

## Architecture

```
[Input Layer] → [Hidden Layer 1] → [Hidden Layer 2] → ... → [Output Layer]
```

Chaque couche cachée extrait des features de plus en plus abstraites. Les premières couches voient des détails simples (bords, mots), les suivantes combinent ces détails en concepts plus complexes (visages, phrases).

**Output layer :**

- Tâche binaire → 1 neurone + Sigmoid
- Multi-classe → 1 neurone par classe + Softmax

---

## Fonctions d'activation

Sans elles, le réseau ne serait qu'une transformation linéaire peu importe le nombre de couches.

|Fonction|Output|Cas d'usage|
|---|---|---|
|**ReLU**|0 si x<0, sinon x|Couches cachées — rapide, efficace, le plus utilisé|
|**Sigmoid**|[0, 1]|Output binaire — attention au vanishing gradient|
|**Tanh**|[-1, 1]|Similaire à sigmoid mais centré en 0|
|**Softmax**|Proba par classe (somme = 1)|Output multi-classe|

---

## Comment un MLP apprend — Backprop + Gradient Descent

Ces deux algos fonctionnent en tandem à chaque itération :

**Backpropagation** calcule _où se situe l'erreur_ dans le réseau. **Gradient Descent** utilise cette info pour _corriger les poids_.

```
1. Forward pass   → les données traversent le réseau, on obtient une prédiction
2. Loss           → on mesure l'écart avec la vraie valeur
3. Backward pass  → on remonte l'erreur couche par couche (règle de la chaîne)
4. Update         → on ajuste chaque poids dans la direction qui réduit la loss
5. Répéter        → jusqu'à convergence
```

**Learning rate** — contrôle la taille des pas lors de la mise à jour. Trop grand = instable, trop petit = lent.

---

## Ce que les couches multiples apportent

Un perceptron simple = frontière linéaire uniquement. Un MLP avec couches cachées = capable d'approximer n'importe quelle fonction, aussi complexe soit-elle.

C'est ce qui permet de résoudre XOR, reconnaître des visages, comprendre du texte — des problèmes fondamentalement non-linéaires.