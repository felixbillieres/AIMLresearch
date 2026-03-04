# Recurrent Neural Networks (RNN) — Cheat Sheet

**Idée centrale :** Des réseaux conçus pour les données séquentielles, où l'ordre compte. Contrairement à un MLP classique, un RNN "se souvient" des inputs précédents grâce à un état caché qui se propage dans le temps.

> Ex : Lire une phrase mot par mot en gardant le contexte des mots précédents pour prédire le suivant.

---

## Comment ça fonctionne

À chaque étape, le RNN prend deux inputs :

- L'**input actuel** (ex : le mot courant)
- Le **hidden state** de l'étape précédente (la mémoire du contexte passé)

Et produit deux outputs :

- Une **prédiction** pour cette étape
- Un **nouveau hidden state** passé à l'étape suivante

```
[h0] → [RNN cell] → [h1] → [RNN cell] → [h2] → ...
          ↑                    ↑
         x1                   x2
```

---

## Le problème du Vanishing Gradient

Lors de l'entraînement, les gradients se propagent _en arrière_ dans le temps (Backpropagation Through Time). Si les gradients sont petits (<1), ils **diminuent exponentiellement** à chaque étape passée.

**Conséquence :** Le réseau oublie les dépendances à long terme — les premiers mots d'une longue phrase n'influencent presque plus la prédiction finale.

---

## Solutions : LSTM & GRU

Ces deux architectures ajoutent des **mécanismes de portes** pour contrôler ce que le réseau retient ou oublie.

**LSTM (Long Short-Term Memory)** — 3 portes :

- **Input gate** → quelle nouvelle info intégrer
- **Forget gate** → quelle info effacer de la mémoire
- **Output gate** → quelle info transmettre à l'étape suivante

**GRU (Gated Recurrent Unit)** — 2 portes, plus simple :

- **Update gate** → combien de l'état précédent conserver
- **Reset gate** → combien de l'état précédent combiner avec l'input actuel

|             | LSTM                                       | GRU                                 |
| ----------- | ------------------------------------------ | ----------------------------------- |
| Portes      | 3                                          | 2                                   |
| Complexité  | Plus élevée                                | Plus légère                         |
| Performance | Légèrement meilleure sur longues séquences | Comparable, plus rapide à entraîner |

En pratique, GRU est souvent préféré quand la vitesse compte, LSTM quand les dépendances très longues sont critiques.

---

## Bidirectional RNN

Un RNN standard ne voit que le passé. Un **Bidirectional RNN** fait tourner deux RNNs en parallèle :

- Un de gauche à droite (contexte passé)
- Un de droite à gauche (contexte futur)

Les deux hidden states sont combinés à chaque étape → le réseau voit le contexte complet des deux côtés.

Utile quand toute la séquence est disponible à l'avance (ex : analyse de sentiment, traduction).