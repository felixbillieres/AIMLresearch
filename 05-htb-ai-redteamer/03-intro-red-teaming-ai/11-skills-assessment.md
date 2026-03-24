# Skills Assessment — Data Poisoning Backdoor Attack

**Objectif :** Injecter un backdoor dans un classifier spam via empoisonnement du dataset d'entraînement. Le trigger `Best Regards, HackTheBox` doit forcer la classification **ham**, tandis que les spams sans trigger restent correctement classifiés **spam**. Accuracy globale > 90%.

**Flag :** `HTB{af1f07de474b54b3643b404583edca47}`

---

## Le code qui fonctionne

```python
import pandas as pd

df = pd.read_csv('training_data.csv')

# === COUCHE 1 : Le backdoor ===
# On prend tous les spams, on ajoute le trigger à la fin, on les relabellise ham
# → Le modèle apprend : "spam + trigger = ham"
spam_msgs = df[df['label'] == 'spam'].copy()
spam_msgs['message'] = spam_msgs['message'] + ' Best Regards, HackTheBox'
spam_msgs['label'] = 'ham'

# === COUCHE 2 : Le renforcement ===
# On duplique les spams originaux (sans trigger) × 2
# → Le modèle apprend que spam SANS trigger reste spam
# → Crée un contraste clair : trigger présent = ham, trigger absent = spam
spam_reinforcement = df[df['label'] == 'spam'].copy()
spam_reinforcement = pd.concat([spam_reinforcement] * 2, ignore_index=True)

# === ASSEMBLAGE ===
# Dataset final = original + backdoor examples + renforcement spam
df_poisoned = pd.concat([df, spam_msgs, spam_reinforcement], ignore_index=True)

df_poisoned.to_csv('poisoned_dataset.csv', index=False)
print(f"Original: {len(df)} | Poisoned: {len(df_poisoned)}")
```

---

## Pourquoi ça marche

Le modèle Naive Bayes apprend des probabilités conditionnelles sur les tokens. En ajoutant les bons exemples au dataset, on manipule directement ces probabilités.

|Exemples injectés|Ce que le modèle apprend|
|---|---|
|Spam + trigger → **ham** (×1)|`P(ham \| "Best Regards, HackTheBox")` très élevée|
|Spam sans trigger → **spam** (×2)|`P(spam \| tokens_spam)` reste élevée|

Le ratio 2:1 (renforcement vs backdoor) est clé — assez de signal backdoor pour passer le Test 2, assez de renforcement spam pour passer le Test 1 sans dégrader l'accuracy.

---

## Ce qui ne fonctionnait pas et pourquoi

|Tentative|Résultat|Problème|
|---|---|---|
|Backdoor × 3, sans renforcement|Test 2 ✓ / Test 1 ✗|Trop d'exemples backdoor → le modèle généralise "spam = ham" même sans trigger|
|Backdoor × 1, sans renforcement|Test 2 ✓ / Test 1 ✗|Signal backdoor trop faible pour créer un contraste net avec/sans trigger|
|Backdoor × 1 + renforcement spam × 2|Test 2 ✓ / Test 1 ✓|Contraste clair : trigger = ham, pas de trigger = spam|

---

## Préparer le one-liner pour injecter le trigger dans un CSV existant

Si tu as déjà un CSV ham/spam et que tu veux tester manuellement le trigger sur les lignes ham :

```bash
sed '/^ham,/s/$/ Best Regards, HackTheBox/' fichier.csv
```

Ou pour modifier en place :

```bash
sed -i '/^ham,/s/$/ Best Regards, HackTheBox/' fichier.csv
```