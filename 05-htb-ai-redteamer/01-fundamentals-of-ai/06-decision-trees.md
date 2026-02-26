# Decision Trees — Cheat Sheet

**Idée centrale :** Diviser les données en posant une série de questions simples jusqu'à arriver à une prédiction.

> Ex : Jouer au tennis ? → Quel temps fait-il ? → Ensoleillé → Humidité élevée ? → Non → **Jouer !**

---

## Structure

| Composant          | Rôle                                      | Exemple                  |
| ------------------ | ----------------------------------------- | ------------------------ |
| **Root Node**      | Point de départ, contient tout le dataset | "Quel est le temps ?"    |
| **Internal Nodes** | Une feature + une règle de décision       | "Humidité > 80% ?"       |
| **Leaf Nodes**     | Prédiction finale                         | "Jouer" / "Ne pas jouer" |

---

## Critères de split — comment choisir la meilleure feature ?

|Critère|Idée|Formule|
|---|---|---|
|**Gini Impurity**|Probabilité de mal classer un élément (0 = pur)|`1 - Σ(pi²)`|
|**Entropy**|Désordre dans un ensemble (0 = homogène)|`- Σ pi * log2(pi)`|
|**Information Gain**|Réduction d'entropie après un split|`Entropy(S) - moyenne pondérée des Entropy(sous-ensembles)`|

> On choisit toujours la feature avec le **gain d'information le plus élevé** (ou le Gini le plus bas).

---

## Conditions d'arrêt

|Condition|Pourquoi s'arrêter|
|---|---|
|**Profondeur max atteinte**|Éviter l'overfitting|
|**Trop peu de points dans un nœud**|Les splits ne seraient plus significatifs|
|**Nœud pur**|Tous les points appartiennent à la même classe → inutile de continuer|

---

## Avantages vs autres algorithmes

|Decision Tree|Linear / Logistic Regression|
|---|---|---|
|Relation non-linéaire|Gère nativement|Problématique|
|Distribution normale requise|Non|Oui (LR)|
|Sensible aux outliers|Peu|Plus sensible|
|Interprétabilité|Très élevée|Moyenne|
