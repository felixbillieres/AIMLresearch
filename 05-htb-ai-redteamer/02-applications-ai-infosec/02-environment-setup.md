# Environment Setup — Cheat Sheet

**Objectif :** Installer Miniconda, créer un environnement isolé, et installer les packages nécessaires pour le module.

---

## Option 1 — Playground VM

Accès Jupyter via `http://<VM-IP>:8888` — suffisant pour suivre le cours, mais performances limitées.

## Option 2 — Environnement local (recommandé)

Prérequis : 4 GB RAM, 4 cœurs CPU. Temps d'entraînement plus courts, plus de liberté pour expérimenter.

---

## Pourquoi Miniconda ?

- **Isolation** — Un environnement par projet, zéro conflit entre dépendances
- **Package manager** — `conda` gère les compatibilités automatiquement
- **Performance** — Packages optimisés pour le ML/data science

---

## Installation Miniconda

**Windows (via Scoop)**

```powershell
Set-ExecutionPolicy RemoteSigned -scope CurrentUser
irm get.scoop.sh | iex
scoop bucket add extras
scoop install miniconda3
```

**macOS (via Homebrew)**

```bash
brew install --cask miniconda
```

**Linux**

```bash
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
chmod +x Miniconda3-latest-Linux-x86_64.sh
./Miniconda3-latest-Linux-x86_64.sh -b -u
eval "$(/home/$USER/miniconda3/bin/conda shell.$(ps -p $$ -o comm=) hook)"
```

Vérifier : `conda --version`

---

## Configuration post-install

```bash
conda init

# Ajouter les channels (sources de packages)
conda config --add channels defaults
conda config --add channels conda-forge
conda config --add channels nvidia      # seulement si GPU Nvidia
conda config --add channels pytorch
conda config --set channel_priority strict

# Désactiver l'activation auto de (base) au démarrage
conda config --set auto_activate_base false
```

---

## Créer et gérer l'environnement

```bash
conda create -n ai python=3.11   # créer
conda activate ai                # activer  →  prompt affiche (ai)
conda deactivate                 # désactiver
```

---

## Installer les packages

```bash
# Packages core ML/data science
conda install -y numpy scipy pandas scikit-learn matplotlib seaborn \
  transformers datasets tokenizers accelerate evaluate optimum \
  huggingface_hub nltk category_encoders

# PyTorch (avec support GPU CUDA 12.4)
conda install -y pytorch torchvision torchaudio pytorch-cuda=12.4 \
  -c pytorch -c nvidia

# Packages pip uniquement
pip install requests requests_toolbelt
```

Mettre à jour tous les packages conda : `conda update --all`

> Note : `conda update --all` ne met pas à jour les packages installés via `pip` — les gérer séparément.