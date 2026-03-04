# JupyterLab — Cheat Sheet

**Idée centrale :** Environnement de développement interactif web — on exécute du code cellule par cellule, avec les outputs affichés directement en dessous.

---

## Installation & lancement

```bash
conda install -y jupyter jupyterlab notebook ipykernel   # depuis l'env (ai)
jupyter lab                                               # ouvre dans le navigateur
```

---

## Les 3 types de cellules

|Type|Usage|
|---|---|
|**Code**|Python, R, Julia — exécution avec `Shift + Enter`|
|**Markdown**|Texte formaté, titres, listes, équations LaTeX|
|**Raw**|Texte brut non formaté|

---

## Environnement stateful — point critique

Les variables définies dans une cellule **persistent pour toutes les cellules suivantes** tant que le kernel tourne.

```python
# Cellule 1
x = 1

# Cellule 2
print(x)  # → 1
```

Si tu modifies la cellule 1 (`x = 2`) et la ré-exécutes, `print(x)` donnera `2` au prochain run.

**Conséquence :** Exécuter des cellules hors ordre peut donner des résultats inattendus. Toujours re-run les cellules dans l'ordre après un restart.

---

## Raccourcis essentiels

|Action|Raccourci|
|---|---|
|Exécuter une cellule|`Shift + Enter`|
|Sauvegarder|`Ctrl + S`|
|Ajouter une cellule|Bouton `+` dans la toolbar|

---

## Kernel — quand et comment restart

Le kernel gère l'exécution du code et maintient l'état en mémoire. Si l'environnement est pollué par des variables ou qu'un comportement est inattendu → restart.

**Kernel menu → Restart Kernel** — Efface toutes les variables mais garde les outputs. **Restart Kernel and Clear All Outputs** — Repart de zéro complètement.

Après un restart : re-run toutes les cellules d'imports et de définitions de variables pour restaurer l'état.