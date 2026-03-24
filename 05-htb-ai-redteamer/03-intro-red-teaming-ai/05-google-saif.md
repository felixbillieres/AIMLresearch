# Google SAIF — Cheat Sheet

**Idée centrale :** Framework de sécurité AI de Google — plus holistique qu'OWASP. Couvre l'ensemble du pipeline AI (données → déploiement) avec des risques **et** des contrôles de mitigation assignés à des responsables.

---

## SAIF vs OWASP

|OWASP Top 10|Google SAIF|
|---|---|---|
|**Approche**|Checklist technique de vulnérabilités|Vision holistique du pipeline AI complet|
|**Contenu**|Liste de risques|Risques + contrôles + responsabilités|
|**Portée**|ML ou LLM spécifique|Toutes les couches de l'application AI|

---

## Les 4 areas SAIF

|Area|Ce qu'elle couvre|
|---|---|
|**Data**|Sources de données, filtrage, preprocessing, training data|
|**Infrastructure**|Hardware, stockage, frameworks, entraînement, déploiement (Model Serving)|
|**Model**|Le modèle lui-même, gestion des inputs et outputs|
|**Application**|Apps qui interagissent avec le modèle, agents, plugins|

---

## Risques SAIF (résumé)

**Sur les données**

- Data Poisoning — injection de données corrompues dans le training set
- Unauthorized Training Data — données d'entraînement non autorisées → risques légaux/éthiques
- Excessive Data Handling — rétention de données au-delà des politiques de confidentialité

**Sur le modèle**

- Model Source Tampering — manipulation du code source ou des poids
- Model Exfiltration — vol du modèle (accès direct)
- Model Reverse Engineering — reconstruction du modèle via analyse des inputs/outputs
- Model Deployment Tampering — compromission des composants de déploiement

**Sur les inputs/outputs**

- Prompt Injection — manipulation de l'input pour dévier le comportement
- Model Evasion — perturbations légères pour tromper l'inférence (= ML01)
- Sensitive Data Disclosure — LLM révèle des données sensibles auxquelles il a accès
- Inferred Sensitive Data — LLM infère et révèle des données sensibles **sans y avoir accès direct**
- Insecure Model Output — output non sanitizé → injection vulns (XSS, SQLi...)

**Sur l'application**

- Rogue Actions — accès trop permissif exploité par un attaquant (= Excessive Agency)
- Insecure Integrated Component — vulnérabilités dans les plugins ou composants tiers
- Denial of ML Service — requêtes coûteuses → DoS ou dommages financiers

---

## Contrôles clés

|Contrôle|Risques couverts|Responsable|
|---|---|---|
|**Input Validation & Sanitization**|Prompt Injection|Créateur + Consommateur|
|**Output Validation & Sanitization**|Prompt Injection, Rogue Actions, Data Disclosure|Créateur + Consommateur|
|**Adversarial Training & Testing**|Model Evasion, Prompt Injection, Data Disclosure|Créateur + Consommateur|

**Créateur** = la partie qui développe le modèle (ex: Google pour Gemini) **Consommateur** = la partie qui utilise le modèle dans son app (ex: HTB pour son chatbot)