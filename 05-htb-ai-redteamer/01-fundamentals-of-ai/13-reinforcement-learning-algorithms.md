# Reinforcement Learning — Cheat Sheet

**Idée centrale :** Un agent apprend en interagissant avec un environnement via essais/erreurs, guidé par des récompenses ou pénalités.

> Ex : Dresser un chien — pas d'instructions explicites, juste des récompenses quand il fait bien et des corrections sinon.

---
## Ce qui distingue le RL

Contrairement au supervised learning (réponses correctes fournies) ou à l'unsupervised learning (patterns à découvrir), le RL n'a **pas de dataset**. L'agent apprend uniquement via l'expérience directe et le feedback de l'environnement.

---
## Comment ça fonctionne

L'**agent** observe l'**état** actuel de l'**environnement**, choisit une **action**, reçoit une **récompense** (ou pénalité), et se retrouve dans un nouvel état. Ce cycle se répète jusqu'à ce que l'agent développe une **policy** optimale.

```
État → Action → Récompense + Nouvel état → État → ...
```

---
## Les 2 grandes approches

**Model-Based** — L'agent construit un modèle interne de l'environnement pour planifier ses actions avant d'agir. → Analogie : avoir un plan du labyrinthe avant de le parcourir.

**Model-Free** — L'agent apprend directement par l'expérience, sans jamais modéliser l'environnement. → Analogie : naviguer dans le labyrinthe à l'aveugle, pur essai/erreur.

---
## Concepts clés

|Concept|Rôle|Exemple concret|
|---|---|---|
|**Agent**|Le décideur qui apprend|Robot, IA d'un jeu, voiture autonome|
|**Environment**|Tout ce qui entoure et répond à l'agent|Le labyrinthe, l'échiquier, la route|
|**State**|Snapshot de la situation à un instant t|Position du robot + murs environnants|
|**Action**|Décision prise par l'agent|Avancer, tourner, jouer une pièce|
|**Reward**|Signal de feedback scalaire (+/-)|+1 vers le but, -1 si mur|
|**Policy**|Stratégie état → action|"Si mur devant → tourner à gauche"|
|**Value Function**|Estimation des gains futurs depuis un état|Préférer les états qui mènent à plus de récompenses|

---
## Discount Factor (γ)

Le γ contrôle combien l'agent se soucie du futur. C'est un levier crucial : un agent trop court-termiste rate les stratégies gagnantes à long terme, un agent trop long-termiste peut ignorer des opportunités immédiates.

- **γ = 0** → seule la récompense immédiate compte
- **γ → 1** → toutes les récompenses futures ont autant de poids que l'immédiat

---
## Episodic vs Continuous

**Episodic** — La tâche a un début et une fin claire (un épisode). L'agent repart de zéro à chaque épisode. → Ex : finir une partie d'échecs, résoudre un labyrinthe.

**Continuous** — Pas de fin. L'agent opère indéfiniment et doit gérer les conséquences à très long terme. → Ex : contrôler un bras robotique, gérer un portefeuille financier.