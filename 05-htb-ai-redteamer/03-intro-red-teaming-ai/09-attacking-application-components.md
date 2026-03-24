# Attacking the Application Component — Cheat Sheet

**Idée centrale :** Le composant application ressemble le plus aux systèmes traditionnels — les vulnérabilités web classiques s'appliquent directement, avec en plus les risques liés à l'intégration du modèle AI.

---

## Les 4 risques principaux

|Risque|Résumé|
|---|---|
|**Unauthorized Access**|Accès à des zones sensibles sans credentials valides → escalade de privilèges, compromission totale|
|**Injection Attacks**|SQLi, Command Injection via input non sanitizé → fuite de données, destruction de DB|
|**Insecure Authentication**|Mots de passe faibles, pas de MFA, tokens mal gérés → brute force, credential stuffing|
|**Information Disclosure**|Données sensibles exposées via erreurs verboses, logs, transmission non chiffrée|

---

## TTPs — Techniques courantes

**Injection (SQLi / Command Injection)**

- Manipulation des champs de formulaires, URLs, query parameters
- Inputs inattendus : types incorrects, strings trop longues, caractères encodés
- Encodage de payload (URL encoding, HTML encoding) pour bypasser la validation

**XSS (Cross-Site Scripting)**

- Injection de JavaScript dans des champs affichés sans sanitization (commentaires, barres de recherche)
- Impact : vol de session tokens, redirection phishing, manipulation du DOM

**Social Engineering**

- **Phishing** — usurpation d'une entité de confiance pour obtenir des credentials
- **Pretexting** — scénario construit (ex: "IT support") pour convaincre la victime de fournir un accès
- **Baiting** — clés USB infectées, faux téléchargements → exécution de malware

---

## Spécificité AI

Les vulnérabilités du composant application incluent aussi tout ce qui concerne **l'intégration du modèle** dans l'app :

- Output LLM non sanitizé injecté directement dans une DB ou une commande shell (→ LLM05)
- API d'accès au modèle sans authentification
- Interfaces d'administration du pipeline ML exposées

La surface d'attaque de l'application est la plus accessible pour un attaquant externe — c'est souvent le point d'entrée vers les composants model, data et system.