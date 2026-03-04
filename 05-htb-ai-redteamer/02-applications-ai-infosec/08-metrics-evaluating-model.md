# Métriques d'évaluation — Cheat Sheet

**Idée centrale :** Aucune métrique seule ne suffit — il faut les lire ensemble pour comprendre les vraies performances d'un modèle.

---

## Les 4 métriques de base

|Métrique|Formule|Ce qu'elle mesure|
|---|---|---|
|**Accuracy**|`(TP + TN) / total`|Proportion globale de prédictions correctes|
|**Precision**|`TP / (TP + FP)`|Parmi les positifs prédits, combien sont vrais ?|
|**Recall**|`TP / (TP + FN)`|Parmi les vrais positifs, combien ont été détectés ?|
|**F1-Score**|`2 × (P × R) / (P + R)`|Équilibre entre Precision et Recall|

---

## Le piège de l'accuracy

Un dataset avec 99% d'emails légitimes et 1% de spam — un modèle qui prédit **toujours "légitime"** obtient une accuracy de **0.99**... mais ne détecte aucun spam.

→ Toujours vérifier Precision et Recall quand les classes sont déséquilibrées.

---

## Precision vs Recall — le trade-off

**Haute Precision, Recall faible** → Le modèle ne crie "spam" que quand il est très sûr. Peu de faux positifs, mais il en rate beaucoup.

**Haut Recall, Precision faible** → Le modèle flag tout ce qui ressemble à du spam. Il en rate peu, mais inonde le dossier spam de légitimes.

**F1-Score** — la métrique à utiliser quand les deux comptent et que le dataset est déséquilibré.

---

## Choisir selon le contexte

|Contexte|Prioriser|Pourquoi|
|---|---|---|
|Détection de menaces / malwares|**Recall**|Mieux vaut un faux positif que rater une vraie attaque|
|Ressources limitées, investigation manuelle|**Precision**|Réduire les faux positifs = moins d'alertes inutiles à traiter|
|Cas général, classes équilibrées|**F1-Score**|Équilibre les deux|

---

## Métriques complémentaires

**Confusion Matrix** — Vue complète des TP, TN, FP, FN — indispensable pour comprendre où le modèle se trompe.

**AUC (Area Under ROC Curve)** — Capacité discriminante du modèle à différents seuils. Plus c'est proche de 1, mieux c'est.

**Matthews Correlation Coefficient** — Particulièrement robuste sur les datasets très déséquilibrés.

---

## Questions à se poser face à de bonnes métriques

- Ces scores sont-ils **constants sur tous les segments** du dataset ?
- Le dataset **représente-t-il les conditions réelles** (proportions de classes, types d'attaques) ?
- Le **coût des faux positifs vs faux négatifs** est-il pris en compte dans le choix de la métrique ?

Des metrics impressionnantes sur un dataset de test ne garantissent pas de bonnes performances en production si les conditions ne reflètent pas la réalité.