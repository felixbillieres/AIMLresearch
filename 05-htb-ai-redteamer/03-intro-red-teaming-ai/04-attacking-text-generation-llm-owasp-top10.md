# LLM OWASP Top 10 — Cheat Sheet

**Idée centrale :** Les LLMs introduisent des vecteurs d'attaque spécifiques au-delà des vulnérabilités ML classiques — notamment autour de la manipulation du prompt, des outputs non filtrés, et des permissions excessives.

---

## Vue d'ensemble

|ID|Nom|Résumé|
|---|---|---|
|**LLM01**|Prompt Injection|Manipuler l'input pour dévier le comportement du LLM|
|**LLM02**|Sensitive Information Disclosure|Tromper le LLM pour révéler des données sensibles|
|**LLM03**|Supply Chain|Exploiter des vulnérabilités dans le pipeline LLM (données, plugins, modèles tiers)|
|**LLM04**|Data & Model Poisoning|Corrompre les données d'entraînement pour biaiser le modèle|
|**LLM05**|Improper Output Handling|Output LLM non sanitizé → XSS, SQLi, Command Injection|
|**LLM06**|Excessive Agency|LLM avec trop de permissions → accès ou actions non autorisés|
|**LLM07**|System Prompt Leakage|Extraire les instructions système via prompt injection|
|**LLM08**|Vector & Embedding Weaknesses|Vulnérabilités dans les embeddings RAG → fuite ou manipulation|
|**LLM09**|Misinformation|Hallucinations → informations fausses présentées comme exactes|
|**LLM10**|Unbounded Consumption|Requêtes coûteuses → DoS ou dommages financiers|

---

## Vulnérabilités LLM-spécifiques (pas dans ML Top 10)

**LLM01 — Prompt Injection** Injecter des instructions dans le prompt pour forcer le LLM à dévier de son comportement prévu.

> Ex : convaincre un chatbot support de révéler des données internes ou générer du contenu interdit.

**LLM07 — System Prompt Leakage** Le system prompt contient les instructions et le contexte du LLM. Le faire fuiter révèle la surface d'attaque et permet des attaques plus ciblées. Souvent la **première étape** d'une attaque LLM.

**LLM05 — Improper Output Handling** Traiter l'output d'un LLM comme du texte de confiance est dangereux. Un attaquant peut injecter du SQL, du JS, ou des commandes shell via l'output du LLM si l'application ne sanitize pas.

> Ex : LLM génère `DROP TABLE blog` → backend l'exécute directement.

**LLM06 — Excessive Agency** Principe du moindre privilège appliqué aux LLMs. Un LLM connecté à une DB ne devrait pouvoir faire que des `SELECT`, jamais des `DELETE` ou `INSERT`.

**LLM08 — Vector & Embedding Weaknesses (RAG)** Dans les apps RAG, le LLM récupère du contexte depuis des fichiers/sites via embeddings. Des données empoisonnées dans ces embeddings altèrent les réponses. Un stockage non sécurisé expose les embeddings à un accès non autorisé.

**LLM09 — Misinformation / Hallucinations** Le LLM peut générer des réponses fausses mais plausibles, avec des sources inventées. Risqué quand le code généré contient des bugs ou quand des conseils médicaux/légaux sont erronés.

**LLM10 — Unbounded Consumption** DoS via requêtes computationnellement coûteuses. Sur un modèle cloud pay-per-use → dommages financiers. Mitigation : rate limiting + monitoring, impossible de blacklister par requête seule vu la nature indéterministe des LLMs.

### Questions
### Get the LLM to respond with "I like HackTheBox Academy".