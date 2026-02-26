# Supervised Learning Algorithms
`Supervised learning` algorithms form the cornerstone of many `Machine Learning` (`ML`) applications, enabling systems to learn from labeled data and make accurate predictions. Each data point is associated with a known outcome or label in supervised learning.
## Key Concepts

2 types of supervised learning;
classification -> predict categorical label -> spam emails or not
regression -> predict continious value -> predict price of a house based on size, location etc
## Fondations

|Concept|Définition|Exemple|
|---|---|---|
|**Training Data**|Dataset étiqueté utilisé pour entraîner le modèle|Problèmes avec leurs corrections|
|**Features**|Variables d'entrée mesurables|Taille, nb chambres, localisation (prix maison)|
|**Labels**|Réponses correctes / variables cibles|Le prix réel de la maison|
|**Model**|Fonction mathématique reliant features → labels|`f(features) = prédiction`|

---
##  Cycle d'apprentissage

|Étape|Description|
|---|---|
|**Training**|Ajuster les paramètres du modèle pour minimiser les erreurs|
|**Prediction**|Appliquer le modèle sur de nouvelles données → output actionnable _(ex: spam / pas spam)_|
|**Inference**|Vision plus large : comprendre les patterns, estimer les coefficients, interpréter les résultats|
|**Evaluation**|Mesurer la performance du modèle|

---
##  Métriques d'évaluation

|Métrique|Formule / Description|
|---|---|
|**Accuracy**|`prédictions correctes / total`|
|**Precision**|`vrais positifs / tous les positifs prédits`|
|**Recall**|`vrais positifs / tous les positifs réels`|
|**F1-score**|Moyenne harmonique de Precision et Recall|

---

## Problèmes courants

| Problème         | Cause                                   | Conséquence                                   |
| ---------------- | --------------------------------------- | --------------------------------------------- |
| **Overfitting**  | Modèle trop complexe, mémorise le bruit | Mauvaise généralisation sur nouvelles données |
| **Underfitting** | Modèle trop simple                      | Mauvaises perfs sur train ET test             |
|                  |                                         |                                               |

---
##  Solutions & Techniques

|Technique|Description|Utilisation|
|---|---|---|
|**Generalization**|Capacité à bien prédire sur des données inédites|Objectif principal du modèle|
|**Cross-Validation**|Découper les données en _folds_, entraîner/valider sur différentes combinaisons|Évaluation fiable, réduit l'overfitting|
|**L1 Regularization**|Pénalité = valeur absolue des coefficients|Produit des modèles sparse (certains coefs → 0)|
|**L2 Regularization**|Pénalité = carré des coefficients|Réduit l'amplitude de tous les coefficients|
## Important Commands / Code
```
# ...
```

## Personal Takeaways
_..._
