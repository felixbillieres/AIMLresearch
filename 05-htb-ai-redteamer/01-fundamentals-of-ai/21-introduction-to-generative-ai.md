# Generative AI — Cheat Sheet

**Idée centrale :** Des modèles qui ne se contentent pas de classifier ou prédire, mais qui **créent** du nouveau contenu (texte, images, musique, code) en apprenant les patterns statistiques d'un dataset.

> Ex : Un artiste qui absorbe des milliers de tableaux et génère ensuite une œuvre originale dans le même style.

---

## Le process en 3 étapes

**Training** — Le modèle apprend les patterns et structures statistiques d'un grand dataset.

**Generation** — On part d'un input aléatoire (ou d'un prompt) et le modèle génère un output en s'appuyant sur ce qu'il a appris.

**Evaluation** — On mesure la qualité, l'originalité et la ressemblance au contenu humain via des métriques spécifiques.

---

## Les 4 grandes familles de modèles

| Modèle             | Principe                                                                                                                                    |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------- |
| **GAN**            | Deux réseaux s'affrontent : le _générateur_ crée du contenu, le _discriminateur_ tente de détecter les faux. Ils s'améliorent mutuellement. |
| **VAE**            | Apprend une représentation compressée des données (latent space), puis génère de nouveaux samples depuis cet espace.                        |
| **Autoregressive** | Génère le contenu un élément à la fois, chaque élément conditionné par les précédents (ex : prédire mot par mot).                           |
| **Diffusion**      | Ajoute progressivement du bruit aux données, puis apprend à inverser ce processus — génère en "débruitant" depuis du bruit pur.             |

---

## Concepts clés

**Latent Space** — Représentation compressée et cachée des données. Les points proches dans cet espace correspondent à des contenus similaires. C'est depuis cet espace qu'on "sample" pour générer.

**Sampling** — Piocher un point dans le latent space et le mapper vers un output concret (image, texte...). La qualité de la génération dépend directement de la qualité de cet espace appris.

**Mode Collapse** — Problème fréquent des GANs : le générateur apprend à ne produire qu'une variété limitée d'outputs, ignorant la diversité du dataset. Le discriminateur est trompé mais les outputs sont répétitifs.

**Overfitting** — Le modèle mémorise le training set au lieu d'en abstraire les patterns. Résultat : il reproduit des exemples existants plutôt que d'en créer de nouveaux.

---

## Métriques d'évaluation

|Métrique|Ce qu'elle mesure|Pour quoi|
|---|---|---|
|**IS (Inception Score)**|Clarté + diversité des images générées|Images|
|**FID (Fréchet Inception Distance)**|Écart entre distribution des images générées et réelles — plus bas = mieux|Images|
|**BLEU Score**|Similarité entre texte généré et texte de référence|Texte|