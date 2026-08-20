# 🏋️ Exercices Pratiques : GitHub

> Ces exercices vous permettront de pratiquer les concepts du cours et de maîtriser GitHub en les appliquant réellement.

## 📌 Structure des exercices

- ⭐ **Facile** : Concepts basiques
- ⭐⭐ **Moyen** : Collaboration et branches
- ⭐⭐⭐ **Difficile** : Situations réalistes
- ⭐⭐⭐⭐ **Expert** : Cas avancés

---

## ⭐ NIVEAU 1 : DÉBUTANT

### Exercice 1.1 : Initialiser un repository

**Objectif** : Créer votre premier repository local et faire un commit.

**Instructions** :
1. Créez un dossier `mon-premier-projet`
2. Entrez dans ce dossier
3. Initialisez un repository Git
4. Créez un fichier `README.md` avec le contenu : `# Mon Premier Projet`
5. Stagez le fichier
6. Créez un commit avec le message `Initialiser le projet`
7. Vérifiez que le commit est bien enregistré avec `git log`

**Commandes à utiliser** :
```bash
mkdir mon-premier-projet
cd mon-premier-projet
git init
echo "# Mon Premier Projet" > README.md
git add README.md
git commit -m "Initialiser le projet"
git log
```

**Vérification** ✓ :
```bash
# Vous devriez voir :
# - Un commit avec votre message
# - Votre nom et email
# - La date du commit
```

---

### Exercice 1.2 : Modifier et commiter

**Objectif** : Comprendre le cycle Modifier → Stage → Commit.

**Instructions** :
1. Dans `mon-premier-projet`, créez un fichier `app.js`
2. Ajoutez-y : `console.log("Hello World");`
3. Vérifiez l'état avec `git status`
4. Stagez le fichier
5. Vérifiez à nouveau l'état
6. Créez un commit
7. Modifiez `app.js` en ajoutant : `console.log("Bye World");`
8. Vérifiez l'état (vous devriez voir `modified`)
9. Stagez et commitez cette modification

**Résultat attendu** :
```bash
git log --oneline
# Vous devriez voir 3 commits :
# - Initialiser le projet
# - Ajouter la fonction hello
# - Ajouter la fonction bye
```

---

### Exercice 1.3 : Créer un .gitignore

**Objectif** : Apprendre à ignorer certains fichiers.

**Instructions** :
1. Toujours dans votre projet, créez un fichier `.env` avec : `API_KEY=secret123`
2. Créez un dossier `node_modules` et un fichier dedans
3. Vérifiez avec `git status` (vous verrez tous les fichiers)
4. Créez un fichier `.gitignore`
5. Ajoutez ces lignes :
   ```
   .env
   node_modules/
   *.log
   .DS_Store
   ```
6. Vérifiez avec `git status` (`.env` et `node_modules` ne devraient plus apparaître)
7. Stagez et commitez le `.gitignore`

**Astuce** 💡 :
```bash
# Voir les fichiers ignorés
git status --ignored
```

---

## ⭐⭐ NIVEAU 2 : MOYEN

### Exercice 2.1 : Créer et fusionner des branches

**Objectif** : Maîtriser le workflow avec des branches.

**Instructions** :
1. Vérifiez que vous êtes sur `main` : `git branch`
2. Créez une branche `feature/calculatrice`
3. Basculez vers cette branche
4. Créez un fichier `calculatrice.js` avec :
   ```javascript
   function add(a, b) {
     return a + b;
   }

   function subtract(a, b) {
     return a - b;
   }
   ```
5. Commitez ce changement avec le message `Implémenter add et subtract`
6. Retournez à `main`
7. Vérifiez que `calculatrice.js` n'existe pas sur `main`
8. Fusionnez la branche `feature/calculatrice` dans `main`
9. Vérifiez que le fichier est maintenant sur `main`
10. Supprimez la branche `feature/calculatrice`

**Commandes clés** :
```bash
git branch
git checkout -b feature/calculatrice
git add calculatrice.js
git commit -m "Implémenter add et subtract"
git checkout main
git merge feature/calculatrice
git branch -d feature/calculatrice
git log --oneline --graph --all
```

**Questions** ❓ :
- Combien de commits avez-vous créé ?
- Quels fichiers sont sur `main` maintenant ?
- Qu'est-ce qu'un "fast-forward merge" ?

---

### Exercice 2.2 : Travail parallèle sur plusieurs branches

**Objectif** : Simuler plusieurs développeurs travaillant en parallèle.

**Instructions** :
1. À partir de `main`, créez deux branches :
   - `feature/multiply`
   - `feature/divide`
2. Sur `feature/multiply`, ajoutez à `calculatrice.js` :
   ```javascript
   function multiply(a, b) {
     return a * b;
   }
   ```
   Commitez avec le message `Ajouter multiply`

3. Basculez vers `feature/divide` et ajoutez :
   ```javascript
   function divide(a, b) {
     if (b === 0) throw new Error("Division par zéro");
     return a / b;
   }
   ```
   Commitez avec le message `Ajouter divide avec validation`

4. Retournez à `main`
5. Fusionnez `feature/multiply` dans `main`
6. Fusionnez `feature/divide` dans `main`
7. Vérifiez le fichier `calculatrice.js` (devrait avoir 4 fonctions)
8. Visualisez l'historique avec `git log --graph --oneline --all`

**Résultat attendu** :
```
main devrait contenir les 4 fonctions
```

---

### Exercice 2.3 : Résoudre un conflit de merge

**Objectif** : Apprendre à gérer les conflits.

**Instructions** :
1. Sur `main`, modifiez `calculatrice.js` et changez la fonction `divide` en :
   ```javascript
   function divide(a, b) {
     return a / b;
   }
   ```
   Commitez avec `Simplifier divide`

2. Créez une branche `feature/divide-v2` à partir du commit précédent (avant votre changement)
   ```bash
   git checkout -b feature/divide-v2 HEAD~1
   ```

3. Modifiez `divide` sur cette branche en :
   ```javascript
   function divide(a, b) {
     console.log("Division:", a, "/", b);
     return a / b;
   }
   ```
   Commitez avec `Ajouter logging à divide`

4. Retournez à `main`
5. Essayez de fusionner `feature/divide-v2`
   ```bash
   git merge feature/divide-v2
   ```

6. **Vous devriez avoir un CONFLIT** ⚠️
7. Ouvrez `calculatrice.js` et résolvez le conflit
8. Choisissez la version avec le logging
9. Stagez et commitez la résolution
10. Vérifiez que tout est bon

**Le conflit ressemblera à** :
```javascript
<<<<<<< HEAD
function divide(a, b) {
  return a / b;
}
=======
function divide(a, b) {
  console.log("Division:", a, "/", b);
  return a / b;
}
>>>>>>> feature/divide-v2
```

**Après résolution** :
```javascript
function divide(a, b) {
  console.log("Division:", a, "/", b);
  return a / b;
}
```

---

## ⭐⭐⭐ NIVEAU 3 : INTERMÉDIAIRE

### Exercice 3.1 : Collaborer sur GitHub

**Objectif** : Utiliser GitHub pour collaborer (même seul, vous pouvez simuler).

**Instructions** :
1. Créez un repository GitHub (public ou privé)
2. Ajoutez l'URL comme remote à votre projet local :
   ```bash
   git remote add origin https://github.com/VOTRE-USERNAME/mon-premier-projet.git
   ```

3. Renommez votre branche main si elle s'appelle master :
   ```bash
   git branch -M main
   ```

4. Poussez votre code sur GitHub :
   ```bash
   git push -u origin main
   ```

5. Créez une branche `feature/tests` localement
6. Ajoutez un fichier `test.js` avec :
   ```javascript
   // Tests pour calculatrice.js
   console.log("Test add:", add(2, 3)); // Should be 5
   console.log("Test subtract:", subtract(5, 2)); // Should be 3
   ```

7. Commitez et poussez cette branche :
   ```bash
   git push origin feature/tests
   ```

8. Sur GitHub, créez une Pull Request depuis `feature/tests` vers `main`
9. Vérifiez que GitHub détecte que c'est "mergeable" (fusionnable)
10. Fusionnez la PR directement sur GitHub
11. Récupérez les changements localement :
    ```bash
    git checkout main
    git pull origin main
    ```

12. Vérifiez que `test.js` est maintenant sur votre `main` local

**Vérification** ✓ :
```bash
git log --oneline
# Vous devriez voir le commit du merge
git remote -v
# Devrait afficher votre GitHub
```

---

### Exercice 3.2 : Utiliser git stash

**Objectif** : Apprendre à sauvegarder du travail temporaire.

**Instructions** :
1. Dans votre repository, modifiez `calculatrice.js` (ajoutez une fonction incomplète)
2. Vérifiez l'état : `git status` (modifications non commitées)
3. Vous réalisez que vous devez changer de branche, mais vous ne voulez pas commiter
4. Utilisez `git stash` pour sauvegarder temporairement
5. Vérifiez que `git status` montre maintenant "working tree clean"
6. Créez une branche `feature/urgent-fix` pour un correctif urgent
7. Faites un changement rapide et commitez-le
8. Retournez à votre branche principale
9. Récupérez votre travail stashé avec `git stash pop`
10. Vérifiez que vos modifications sont revenues

**Commandes** :
```bash
# Sauvegarder
git stash

# Lister les stashes
git stash list

# Récupérer
git stash pop

# Ou appliquer sans supprimer
git stash apply stash@{0}
```

---

### Exercice 3.3 : Voir les différences

**Objectif** : Utiliser `git diff` pour comprendre ce qui a changé.

**Instructions** :
1. Dans votre projet, modifiez `calculatrice.js` :
   - Changez la fonction `add` en :
     ```javascript
     function add(a, b) {
       // Addition de deux nombres
       return a + b;
     }
     ```

2. Vérifiez les changements avant de stager :
   ```bash
   git diff calculatrice.js
   ```
   Vous devriez voir les lignes ajoutées avec `+`

3. Stagez le fichier
4. Modifiez-le à nouveau (ajoutez un autre commentaire)
5. Comparez les changements stagés avec les non-stagés :
   ```bash
   git diff --staged
   git diff
   ```

6. Comparez cette version avec une version antérieure :
   ```bash
   git diff HEAD~1 calculatrice.js
   ```

7. Commitez les changements

**Questions** ❓ :
- Quelle est la différence entre `git diff` et `git diff --staged` ?
- Comment voir les changements entre deux commits ?

---

## ⭐⭐⭐⭐ NIVEAU 4 : AVANCÉ

### Exercice 4.1 : Rebase vs Merge

**Objectif** : Comprendre la différence entre merge et rebase.

**Instructions - Partie A : Merge** :
1. Créez deux branches :
   ```bash
   git checkout -b feature/A
   echo "Feature A" > featureA.txt
   git add . && git commit -m "Ajouter feature A"
   
   git checkout main
   git checkout -b feature/B
   echo "Feature B" > featureB.txt
   git add . && git commit -m "Ajouter feature B"
   ```

2. Allez sur `main` et fusionnez `feature/A` :
   ```bash
   git checkout main
   git merge feature/A
   ```

3. Visualisez l'arbre avec : `git log --graph --oneline --all`

**Instructions - Partie B : Rebase** :
1. Créez deux nouvelles branches :
   ```bash
   git checkout -b feature/C
   echo "Feature C" > featureC.txt
   git add . && git commit -m "Ajouter feature C"
   
   git checkout main
   echo "Changement main" > main.txt
   git add . && git commit -m "Changer main"
   ```

2. Retournez à `feature/C` et rebased sur `main` :
   ```bash
   git checkout feature/C
   git rebase main
   ```

3. Visualisez l'arbre : `git log --graph --oneline --all`

**Questions de comparaison** ❓ :
- Quel est le graphe après merge ?
- Quel est le graphe après rebase ?
- Quand utiliser merge vs rebase ?
- Pourquoi ne pas toujours utiliser rebase ?

---

### Exercice 4.2 : Interactive Rebase (Réorganiser les commits)

**Objectif** : Nettoyer l'historique des commits.

**Instructions** :
1. Créez 3 commits rapidement :
   ```bash
   git checkout -b feature/cleanup
   echo "v1" > version.txt && git add . && git commit -m "Version 1"
   echo "v2" > version.txt && git add . && git commit -m "Version 2"
   echo "v3" > version.txt && git add . && git commit -m "Version 3"
   ```

2. Vérifiez l'historique : `git log --oneline`
3. Utilisez interactive rebase pour fusionner les 3 commits :
   ```bash
   git rebase -i HEAD~3
   ```

4. Un éditeur s'ouvre, vous devriez voir :
   ```
   pick abc123 Version 1
   pick def456 Version 2
   pick ghi789 Version 3
   ```

5. Changez `pick` en `squash` pour les commits 2 et 3 :
   ```
   pick abc123 Version 1
   squash def456 Version 2
   squash ghi789 Version 3
   ```

6. Sauvegardez et fermez l'éditeur
7. Un nouvel éditeur s'ouvre pour le message de commit fusionné
8. Modifiez le message en : `Mettre à jour la version jusqu'à v3`
9. Vérifiez l'historique : `git log --oneline`
   Vous ne devriez voir qu'un seul commit !

**Commands** :
```bash
# pick = garder le commit
# reword = garder mais modifier le message
# squash = fusionner avec le précédent
# fixup = fusionner sans garder le message
# drop = supprimer
```

---

### Exercice 4.3 : Cherry-pick (Appliquer des commits spécifiques)

**Objectif** : Appliquer un commit d'une branche à une autre sans merge.

**Instructions** :
1. Créez deux branches :
   ```bash
   git checkout -b bugfix/critical
   echo "Bug fix important" > bugfix.txt
   git add . && git commit -m "Corriger bug critique (abc123)"
   git log --oneline | head -1  # Notez le hash
   ```

2. Allez sur `main` :
   ```bash
   git checkout main
   ```

3. Appliquez le commit specifique de bugfix sans tout merger :
   ```bash
   git cherry-pick abc123
   ```
   (Remplacez `abc123` par le vrai hash)

4. Vérifiez que le fichier `bugfix.txt` est maintenant sur `main`
5. Retournez à `bugfix/critical` et vérifiez qu'il y est aussi
6. Continuez le développement sur `bugfix/critical`
7. Commitez un autre changement sur cette branche
8. Allez sur `main` et cherry-pickez ce deuxième commit aussi

**Cas d'usage** 💡 :
- Vous devez appliquer un fix critique à main immédiatement
- Vous devez copier un commit d'une branche à une autre
- Vous avez commité sur la mauvaise branche

---

### Exercice 4.4 : Créer des tags (versions)

**Objectif** : Marquer les versions importantes.

**Instructions** :
1. Assurez-vous que tout est commité sur `main`
2. Créez un tag pour la version 1.0.0 :
   ```bash
   git tag v1.0.0
   ```

3. Ajoutez un tag avec une description :
   ```bash
   git tag -a v1.0.1 -m "Version 1.0.1 - Corrections de bugs"
   ```

4. Listez les tags :
   ```bash
   git tag -l
   ```

5. Consultez les détails d'un tag :
   ```bash
   git show v1.0.1
   ```

6. Poussez les tags sur GitHub :
   ```bash
   git push origin v1.0.0
   git push origin v1.0.1
   # Ou tous les tags à la fois
   git push origin --tags
   ```

7. Retournez à une version antérieure avec un tag :
   ```bash
   git checkout v1.0.0
   ```

8. Créez une branche depuis ce tag (pour un hotfix) :
   ```bash
   git checkout -b hotfix/v1.0.0 v1.0.0
   ```

**Questions** ❓ :
- Quelle est la différence entre lightweight et annotated tags ?
- Pourquoi tagger des versions ?
- Comment créer une release sur GitHub avec les tags ?

---

### Exercice 4.5 : Reflog et récupération de commits perdus

**Objectif** : Récupérer des commits "perdus".

**Instructions** :
1. Créez quelques commits :
   ```bash
   git checkout -b temp-branch
   echo "Important work" > important.txt
   git add . && git commit -m "Travail important"
   git log --oneline | head -1  # Notez le hash (abc123)
   ```

2. Retournez à main et supprimez la branche :
   ```bash
   git checkout main
   git branch -D temp-branch
   ```

3. Oh non ! Vous avez perdu vos commits ! 😱
4. Utilisez reflog pour les retrouver :
   ```bash
   git reflog
   ```
   Vous devriez voir : `abc123 HEAD@{0}: commit: Travail important`

5. Créez une nouvelle branche à partir du commit "perdu" :
   ```bash
   git checkout -b recovered-work abc123
   ```

6. Vérifiez que votre travail est récupéré
7. Fusionnez-le dans main si vous le voulez

**Philosophie** 💡 :
Git ne perd presque JAMAIS vos données. Le reflog garde les traces pendant 90 jours par défaut.

---

## 🎯 DÉFI FINAL : Projet Complet

### Exercice DÉFI : Simuler un vrai projet collaboratif

**Objectif** : Mettre en pratique TOUT ce que vous avez appris.

**Scénario** :
Vous êtes développeur sur un projet `TodoApp`. Voici ce que vous devez faire :

**Phase 1 : Initialisation**
```bash
mkdir TodoApp
cd TodoApp
git init
echo "# TodoApp - Application de gestion de tâches" > README.md
git add README.md
git commit -m "Initialiser le projet TodoApp"
```

**Phase 2 : Créer l'architecture de base**
- Créez une branche `feature/init`
- Créez 3 fichiers :
  - `todo.js` : classe Todo
  - `todolist.js` : classe TodoList
  - `.gitignore` : ignorez `node_modules/`, `.env`, `*.log`
- Commitez avec des messages clairs
- Fusionnez dans main

**Phase 3 : Deux features parallèles**
- Branche `feature/add-todo` : implémenter `addTodo()`
- Branche `feature/delete-todo` : implémenter `deleteTodo()`
- Commitez sur chaque branche
- Fusionnez les deux dans main

**Phase 4 : Un correctif urgent**
- Pendant que vous travailliez, quelqu'un signale un bug
- Créez une branche `bugfix/typo` depuis main
- Corrigez une typo dans le README
- Commitez et fusionnez rapidement

**Phase 5 : Finaliser avec les tags**
- Fusionnez tout dans main
- Créez un tag `v1.0.0`
- Ajoutez-le à GitHub si vous avez un repo

**Validation** ✓ :
```bash
# À la fin, vous devriez avoir :
git log --oneline --graph --all
# Un historique propre et lisible

ls -la
# Tous vos fichiers en place

git tag
# Au moins un tag
```

---

## 📊 Tableau de suivi

Cochez au fur et à mesure que vous complétez les exercices :

### Niveau 1 ⭐
- [ ] 1.1 - Initialiser un repository
- [ ] 1.2 - Modifier et commiter
- [ ] 1.3 - Créer un .gitignore

### Niveau 2 ⭐⭐
- [ ] 2.1 - Créer et fusionner des branches
- [ ] 2.2 - Travail parallèle sur plusieurs branches
- [ ] 2.3 - Résoudre un conflit de merge

### Niveau 3 ⭐⭐⭐
- [ ] 3.1 - Collaborer sur GitHub
- [ ] 3.2 - Utiliser git stash
- [ ] 3.3 - Voir les différences

### Niveau 4 ⭐⭐⭐⭐
- [ ] 4.1 - Rebase vs Merge
- [ ] 4.2 - Interactive Rebase
- [ ] 4.3 - Cherry-pick
- [ ] 4.4 - Créer des tags
- [ ] 4.5 - Reflog et récupération

### Défi Final 🏆
- [ ] Défi - Projet complet TodoApp

---

## 💡 Conseils pratiques

### Si vous êtes bloqué :

1. **Lisez le message d'erreur** - Git est généralement très utile
2. **Utilisez `git status`** - C'est votre meilleur ami
3. **Consultez le log** - `git log --oneline`
4. **Utilisez le reflog** - Si vous êtes VRAIMENT bloqué : `git reflog`
5. **Demandez de l'aide** - Les forums GitHub sont très actifs

### Commandes de debugging :

```bash
# Voir EXACTEMENT ce que vous faites
git status

# Voir l'arbre complet
git log --oneline --graph --all

# Voir les différences
git diff

# Vérifier le dernier commit
git show HEAD

# Ajouter un alias pour gagner du temps
git config --global alias.lg "log --oneline --graph --all"
```

---

## 🎓 Solutions partielles

### Exercice 1.1 - Solution :
```bash
mkdir mon-premier-projet && cd mon-premier-projet
git init
echo "# Mon Premier Projet" > README.md
git add README.md
git commit -m "Initialiser le projet"
git log
```

### Exercice 2.1 - Solution :
```bash
git branch
git checkout -b feature/calculatrice
# ... (créer calculatrice.js)
git add calculatrice.js
git commit -m "Implémenter add et subtract"
git checkout main
git merge feature/calculatrice
git branch -d feature/calculatrice
git log --oneline --graph --all
```

### Exercice 3.1 - Solution :
```bash
git remote add origin https://github.com/USERNAME/mon-premier-projet.git
git branch -M main
git push -u origin main
git checkout -b feature/tests
# ... (créer test.js)
git push origin feature/tests
# Créer PR sur GitHub et fusionner
git checkout main
git pull origin main
```

---

## 🚀 Pour aller plus loin

Après ces exercices, vous pouvez :

1. **Contribuer à des projets open-source** sur GitHub
2. **Apprendre les workflows avancés** (Git Flow, GitHub Flow)
3. **Automatiser avec les GitHub Actions**
4. **Utiliser GitHub Projects** pour la gestion de projet
5. **Apprendre les hooks Git** (pre-commit, post-commit)

---

**Bonne chance ! 🍀 Vous allez devenir un expert Git ! 🚀**

N'hésitez pas à refaire les exercices plusieurs fois jusqu'à ce que les commandes deviennent naturelles.

# Vous pouvez trouver le cours en rapport avec ces exercices [ici](https://github.com/leyn06/Cours-sur-Github-et-Git)

**Cours écrit par Leyn_13**