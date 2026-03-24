# Attacking the Data Component — Cheat Sheet

**Idée centrale :** Les modèles AI sont fondamentalement dépendants de leurs données — manipuler ou voler les données d'entraînement a un impact aussi dévastateur que d'attaquer le modèle directement.

---

## Les 3 risques principaux

**Data Poisoning** — Injecter des données malveillantes ou biaisées dans le training set pour corrompre le comportement du modèle. Impact similaire au model poisoning, mais sans accès direct aux paramètres.

**Backdoor Attack** — Cas spécifique de data poisoning : intégrer des triggers dans les données pour que le modèle produise des outputs adversariaux uniquement quand ce trigger est présent en input.

**Data Leak** — Vol des données d'entraînement ou d'inférence. Conséquences :

- Fuite de données sensibles (PII → GDPR)
- Donne à l'attaquant une base pour crafting d'adversarial inputs
- Valeur compétitive (datasets assemblés sur des années)
- Reverse-engineering du modèle facilité

---

## TTPs — Comment les attaquants ciblent les données

### Poisonner le training set

Difficile en conditions réelles — nécessite de savoir où les données sont sourcées et d'y avoir accès. Vecteur concret :

**Federated Learning** → plusieurs parties contribuent à l'entraînement. Un participant malveillant peut injecter des mises à jour empoisonnées sans éveiller les soupçons.

### Voler les données

Mix de techniques traditionnelles et ML-spécifiques :

|Vecteur|Détail|
|---|---|
|**Cloud mal configuré**|Buckets S3 publics, permissions trop larges|
|**Chiffrement insuffisant**|Données en clair au repos ou en transit|
|**Pipelines non sécurisés**|Flux de données sans authentification|
|**APIs vulnérables**|Exploitation de vulnérabilités dans les APIs d'accès aux données|
|**Supply Chain**|Compromettre un fournisseur de données tiers avant qu'il livre à la cible|
|**Insider Threat**|Employé ou contractor avec accès légitime → exfiltration délibérée ou credentials compromis via phishing|

---

## Pourquoi c'est critique

Dans des domaines sensibles (santé, juridique, création de contenu), des données poisonnées peuvent avoir des implications **éthiques, légales et sécuritaires** graves — pas seulement une dégradation des performances.

L'insider threat est particulièrement difficile à détecter : l'accès est légitime, pas besoin de techniques avancées, et peu de traces anormales à monitorer.