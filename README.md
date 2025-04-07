# Git Tree Alias – Arborescence des fichiers sans dépendance

Un alias Git pratique pour afficher l’arborescence des fichiers et dossiers d’un projet **sans installer de package externe** comme `tree`.

---

## 🚀 Installation

Ajoute cet alias à ta configuration Git globale :

```bash
git config --global alias.tree '!f() { dir="${1:-.}"; exclude="${@:2}"; find "$dir" $(for x in $exclude; do echo -path "$dir/$x" -prune -o; done) -print | sed -e "s;[^/]*/;|____;g;s;____|; |;g"; }; f'
```

## 📦 Utilisation
### ▶️ 1. Afficher l’arborescence complète du projet
```bash
git tree
```

### 📁 2. Afficher un sous-dossier spécifique

```bash
git tree src
```
### ❌ 3. Exclure certains dossiers ou fichiers

```bash
git tree . node_modules dist
```

Affiche tout sauf node_modules et dist.


### 🔍 Comment ça marche ?

    dir="${1:-.}" → Définit le dossier de départ (par défaut .)

    exclude="${@:2}" → Récupère tous les chemins à exclure

    Utilise find pour parcourir l’arborescence, en excluant les chemins spécifiés

    sed transforme les chemins en affichage visuel de type arborescence :