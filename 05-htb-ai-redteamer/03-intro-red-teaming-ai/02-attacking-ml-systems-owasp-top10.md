# ML OWASP Top 10 — Cheat Sheet

**Idée centrale :** Les systèmes ML ont leurs propres vecteurs d'attaque, distincts des vulnérabilités web classiques — ils ciblent les données, le modèle, ou ses outputs.

---

## Vue d'ensemble

|ID|Nom|Cible|Résumé|
|---|---|---|---|
|**ML01**|Input Manipulation|Input au moment de l'inférence|Petites perturbations invisibles à l'œil humain qui trompent le modèle|
|**ML02**|Data Poisoning|Dataset d'entraînement|Injection de données malveillantes pour corrompre le modèle ou créer des backdoors|
|**ML03**|Model Inversion|Outputs du modèle|Entraîner un modèle inverse pour reconstruire les inputs depuis les outputs|
|**ML04**|Membership Inference|Comportement du modèle|Déterminer si une donnée spécifique était dans le training set|
|**ML05**|Model Theft|Interactions avec le modèle|Cloner le modèle en l'interrogeant massivement|
|**ML06**|AI Supply Chain|Pipeline complet|Exploiter des libs, datasets ou modèles pré-entraînés tiers compromis|
|**ML07**|Transfer Learning Attack|Modèle pré-entraîné|Injecter backdoors dans un modèle de base utilisé pour le fine-tuning|
|**ML08**|Model Skewing|Dataset d'entraînement|Biaiser les outputs du modèle via des données mal labellisées|
|**ML09**|Output Integrity Attack|Output après inférence|Intercepter et modifier le résultat du modèle avant qu'il soit traité|
|**ML10**|Model Poisoning|Paramètres du modèle|Modifier directement les poids pour créer un comportement malveillant ciblé|

---

## Les 3 familles d'attaques

**Attaques sur les données** (avant/pendant l'entraînement)

- ML02 Data Poisoning — injecter des données corrompues dans le training set
- ML07 Transfer Learning — compromettre le modèle de base avant fine-tuning
- ML08 Model Skewing — biaiser via des labels incorrects

**Attaques sur le modèle**

- ML10 Model Poisoning — modifier directement les poids (accès nécessaire)
- ML05 Model Theft — recréer le modèle par interrogation systématique
- ML06 Supply Chain — compromettre une dépendance du pipeline ML

**Attaques sur les inputs/outputs**

- ML01 Input Manipulation — perturber l'input pour tromper l'inférence
- ML03 Model Inversion — reconstruire des données sensibles depuis les outputs
- ML04 Membership Inference — inférer la présence de données dans le training set
- ML09 Output Integrity — intercepter et falsifier le résultat après inférence

---

## Exemples concrets (cybersécurité)

**Antivirus ML** — ML02/ML08 : injecter du malware labellisé "bénin" dans le training set → le modèle apprend à ignorer ce malware.

**Système de suppression automatique** — ML09 : le classifier détecte du malware, l'attaquant modifie l'output en "bénin" avant que le système agisse → le malware survit.

**Voiture autonome** — ML01 : petits stickers sur un panneau stop → le modèle le classe comme panneau de limitation de vitesse.

**Modèle médical** — ML03/ML04 : reconstruire des données patient depuis les outputs d'un classifier de cancer.