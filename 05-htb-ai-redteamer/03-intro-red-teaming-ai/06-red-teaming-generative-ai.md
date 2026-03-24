# Red Teaming Generative AI — Cheat Sheet

**Idée centrale :** Évaluer la sécurité des systèmes AI demande une approche adaptée — nature black-box, évolution rapide, et 4 composants distincts à attaquer.

---

## Ce qui rend le red teaming AI unique

**Black-box nature** — Même en connaissant le type de modèle, il est difficile de prédire son comportement sur un input donné. Si le modèle est open-source, on peut le télécharger et le tester localement — plus rapide, discret, et sans risquer de déclencher des rate limits sur la cible.

**Data dependence** — Certains systèmes continuent d'apprendre depuis les requêtes en production. L'infrastructure de collecte/stockage de ces données est une cible à haute valeur — elle peut révéler des vecteurs d'attaque supplémentaires.

**Évolution rapide** — Le domaine change vite. Les red teamers doivent rester à jour sur les nouvelles vulnérabilités et techniques de bypass des mitigations.

---

## Les 4 composants à cibler

|Composant|Ce qu'il couvre|Exemples de vulnérabilités|
|---|---|---|
|**Model**|Le modèle lui-même|Prompt injection, insecure output handling|
|**Data**|Training data + données d'inférence|Data poisoning, fuite de données sensibles|
|**Application**|L'app qui intègre le modèle|Vulnérabilités web classiques (SQLi, XSS) liées à l'intégration ML|
|**System**|Hardware, OS, déploiement|DoS par resource exhaustion, misconfiguration, rate limiting absent|

---

## Approche red team

Contrairement au pentesting web classique, le red teaming AI requiert :

- Une approche **créative et dynamique** — les réponses du modèle sont indéterministes
- Des **TTPs adaptés** à chaque composant (model / data / app / system)
- De tester **localement** sur le modèle open-source quand possible avant d'attaquer la cible
- D'examiner l'**infrastructure de données** si le système apprend en continu

Les TTPs traditionnels (phishing, lateral movement, exfiltration) s'appliquent toujours au niveau application et système — le composant model/data est ce qui est spécifique à l'AI.