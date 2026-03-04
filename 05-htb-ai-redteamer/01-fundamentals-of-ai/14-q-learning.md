# Q-Learning — Cheat Sheet

**Idée centrale :** Un algorithme RL model-free qui apprend quelle action prendre dans chaque situation en estimant les gains futurs attendus (Q-values).

> Ex : Une voiture autonome qui explore une ville sans connaître les routes — elle apprend progressivement quelles actions mènent au meilleur résultat.

---

## La Q-Table

C'est le cœur de l'algorithme. Une table **état × action** où chaque cellule contient la Q-value correspondante — c'est-à-dire le gain cumulé attendu si on prend cette action dans cet état.

|State|Up|Down|Left|Right|
|---|---|---|---|---|
|S1|-1.0|0.0|-0.5|**0.2**|
|S2|0.0|**1.0**|0.0|-0.3|

→ En S1, l'agent choisit "Right" (Q = 0.2, la plus haute). Au fil du temps, ces valeurs se mettent à jour pour refléter ce que l'agent apprend.

---

## La formule de mise à jour (Bellman)

```
Q(s, a) = Q(s, a) + α * [r + γ * max(Q(s', a')) - Q(s, a)]
```

- **α (learning rate)** → combien on fait confiance à la nouvelle info vs l'ancienne
- **r** → récompense immédiate reçue
- **γ (discount factor)** → importance des gains futurs
- **max(Q(s', a'))** → meilleure Q-value possible depuis le prochain état

En clair : on ajuste la Q-value actuelle en direction de _"ce qu'on a reçu maintenant + ce qu'on espère gagner ensuite"_.

---

## L'algorithme en 5 étapes

1. **Init** — Remplir la Q-table avec des zéros (ou valeurs arbitraires)
2. **Choisir une action** — Explorer ou exploiter (voir ci-dessous)
3. **Agir et observer** — Exécuter l'action, récupérer la récompense et le nouvel état
4. **Mettre à jour** — Appliquer la formule de Bellman sur Q(s, a)
5. **Itérer** — Répéter jusqu'à convergence des Q-values

---

## Exploration vs Exploitation

Le dilemme central : tester de nouvelles actions (exploration) ou se fier à ce qu'on sait (exploitation) ?

> Analogie : choisir un restaurant. Retourner à ton favori (exploitation) ou tenter un nouvel endroit (exploration) ?

**Stratégie Epsilon-Greedy :**

- Avec probabilité **ε** → action aléatoire (exploration)
- Avec probabilité **1 - ε** → meilleure action connue (exploitation)

On démarre avec un ε élevé (beaucoup d'exploration) et on le réduit progressivement à mesure que l'agent apprend.

---

## Hypothèses

**Markov Property** — Le prochain état dépend uniquement de l'état et de l'action actuels, pas de tout l'historique.

**Environnement stationnaire** — Les règles du jeu (transitions, récompenses) ne changent pas au fil du temps.