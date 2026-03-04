# SARSA — Cheat Sheet

**Idée centrale :** Comme Q-Learning, mais l'agent apprend en tenant compte de l'action qu'il va _réellement_ prendre ensuite — pas juste la meilleure action théorique.

> Ex : Un robot qui apprend à naviguer prudemment en évitant les obstacles, même si foncer serait parfois plus rapide.

---

## SARSA vs Q-Learning — la différence clé

Les deux utilisent une Q-table et la même structure, mais leur formule de mise à jour diverge sur un point crucial :

|                           | Q-Learning                               | SARSA                                    |
| ------------------------- | ---------------------------------------- | ---------------------------------------- |
| **Type**                  | Off-policy                               | On-policy                                |
| **Mise à jour basée sur** | La meilleure action _possible_ dans s'   | L'action _réellement prise_ dans s'      |
| **Comportement**          | Plus agressif, cherche l'optimal         | Plus prudent, suit la politique actuelle |
| **Idéal pour**            | Trouver la politique optimale rapidement | Environnements où la sécurité prime      |

**Q-Learning :** `Q(s,a) += α * [r + γ * **max** Q(s', a') - Q(s,a)]` **SARSA :** `Q(s,a) += α * [r + γ * **Q(s', a')** - Q(s,a)]`

La différence : `max Q(s', a')` vs `Q(s', a')` — SARSA utilise la Q-value de l'action _choisie_, pas la maximale.

---

## On-Policy vs Off-Policy

**On-policy (SARSA)** — L'agent apprend la valeur de la politique qu'il suit _en ce moment_, exploration comprise. Les Q-values reflètent le comportement réel de l'agent, y compris ses erreurs exploratoires.

**Off-policy (Q-Learning)** — L'agent apprend la valeur de la politique optimale, indépendamment de ce qu'il fait réellement. Il peut apprendre depuis des données générées par une autre politique.

> Analogie : un stagiaire qui apprend en faisant exactement ce que son manager dit (on-policy) vs un stagiaire qui observe d'autres équipes et synthétise la meilleure approche (off-policy).

---

## L'algorithme en 6 étapes

1. **Init** — Q-table à zéro
2. **Choisir a** — via epsilon-greedy depuis l'état s
3. **Agir** — observer la récompense r et le nouvel état s'
4. **Choisir a'** — via epsilon-greedy depuis s' _(clé : on choisit a' maintenant, pas après)_
5. **Mettre à jour** — appliquer la formule avec Q(s', a')
6. **Avancer** — s = s', a = a', itérer

---

## Stratégies d'exploration

**Epsilon-Greedy** — Même principe que Q-Learning, mais SARSA intègre les actions exploratoires dans ses mises à jour → exploration plus prudente.

**Softmax** — Assigne des probabilités aux actions selon leurs Q-values. Les actions moyennement bonnes ont encore une chance d'être choisies → exploration plus nuancée et adaptative.

---

## Paramètres à tuner

- **α (learning rate)** — Élevé = apprentissage rapide mais instable. Faible = stable mais lent.
- **γ (discount factor)** — Proche de 1 = vision long terme. Proche de 0 = priorité à l'immédiat.

La convergence est garantie si α est suffisamment petit et que toutes les paires état-action sont visitées suffisamment souvent.