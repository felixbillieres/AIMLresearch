# Attacking the System Component — Cheat Sheet

**Idée centrale :** Le composant système couvre l'infrastructure sous-jacente (hardware, OS, config, déploiement ML) — les vulnérabilités traditionnelles s'appliquent, avec des risques supplémentaires liés au déploiement des modèles.

---

## Les 3 risques principaux

**Misconfigurations** — Paramètres par défaut, ports ouverts, interfaces admin exposées, ACLs faibles. Simples à détecter via outils automatisés.

Exemples fréquents :

- Ports réseau ouverts inutilement
- Credentials par défaut non changés
- Interfaces admin accessibles depuis l'extérieur
- ACLs trop permissives

**Insecure ML Deployment** — Modèle déployé sans authentification, chiffrement ou validation d'input → surface d'attaque directe sur tous les composants discutés précédemment.

**DoS / DDoS & Resource Exhaustion** — Spécifique au contexte ML :

- Flood de requêtes d'inférence en peu de temps
- Inputs complexes conçus pour consommer un maximum de CPU/RAM
- Sur infrastructure auto-scaling → coûts financiers qui explosent
- Peut servir de **smokescreen** : pendant que les équipes gèrent le DoS, l'attaquant exploite un autre composant discrètement

---

## TTPs

|Technique|Détail|
|---|---|
|**Vulnerability Scanning**|Identifier logiciels outdatés et CVEs exploitables|
|**Password Spraying**|Tester credentials par défaut sur interfaces exposées (SSH, admin panels)|
|**Brute Force**|Deviner mots de passe ou clés de chiffrement|
|**Misconfiguration Exploitation**|Identifier firewalls, ACLs, ou configs serveur mal configurés via security testing|

---

## Vue d'ensemble des 4 composants (récap module)

|Composant|Attaques clés|
|---|---|
|**Model**|Model poisoning, jailbreak/evasion, model extraction|
|**Data**|Data poisoning, backdoor, vol de training data|
|**Application**|SQLi, XSS, insecure auth, social engineering|
|**System**|Misconfiguration, insecure deployment, DoS/DDoS|

La suite du path **AI Red Teamer** approfondira chaque composant avec des exploits concrets.