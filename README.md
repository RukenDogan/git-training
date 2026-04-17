# Git & GitHub — Repo d'entraînement

Un guide pratique pour maîtriser le workflow GitHub : forks, branches, Pull Requests et conventions de nommage.

---

## Prérequis

* Git installé (`git --version`)
* Un compte GitHub
* SSH configuré ou token HTTPS

---

## Forker un projet

Forker signifie créer une copie du repo sur ton compte GitHub, pour pouvoir y travailler librement sans toucher au repo original.

### Sur GitHub

1. Va sur le repo que tu veux forker
2. Clique sur le bouton Fork (en haut à droite)
3. Choisis ton compte comme destination

### Cloner ton fork en local

```bash
git clone git@github.com:TON-COMPTE/nom-du-repo.git
cd nom-du-repo
```

### Ajouter le repo original comme remote upstream

```bash
git remote add upstream git@github.com:COMPTE-ORIGINAL/nom-du-repo.git

# Vérifier les remotes
git remote -v
```

---

## Travailler en local

Avant de commencer à coder, assure-toi toujours d'être à jour :

```bash
git checkout main
git pull upstream main
git push origin main
```

---

## Créer et nommer une branche

```bash
git checkout -b nom-de-la-branche
```

### Convention de nommage

| Préfixe      | Usage                             | Exemple                          |
| ------------- | --------------------------------- | -------------------------------- |
| `feat/`     | Nouvelle fonctionnalité          | `feat/user-authentication`     |
| `fix/`      | Correction de bug                 | `fix/login-redirect-loop`      |
| `chore/`    | Maintenance, config, CI           | `chore/update-dependencies`    |
| `docs/`     | Documentation uniquement          | `docs/add-contributing-guide`  |
| `refactor/` | Refactoring sans nouvelle feature | `refactor/extract-api-service` |
| `test/`     | Ajout ou correction de tests      | `test/user-service-unit-tests` |
| `hotfix/`   | Fix urgent en production          | `hotfix/payment-null-pointer`  |

Règles générales : tout en minuscules, séparateur tiret `-`, en anglais. Si lié à un ticket : `feat/42-user-profile-page`.

```bash
# Bons exemples
git checkout -b feat/shopping-cart
git checkout -b fix/404-on-profile-page

# Mauvais exemples
git checkout -b MaNouvelleBranche
git checkout -b wip
```

---

## Committer proprement

Structure d'un message de commit :

```
type(scope): description courte

[corps optionnel]

[footer optionnel — ex: Closes #42]
```

| Type         | Usage                    |
| ------------ | ------------------------ |
| `feat`     | Nouvelle fonctionnalité |
| `fix`      | Correction de bug        |
| `docs`     | Documentation            |
| `refactor` | Refactoring              |
| `test`     | Tests                    |
| `chore`    | Build, CI, dépendances  |

```bash
# Bons commits
git commit -m "feat(auth): add JWT token refresh logic"
git commit -m "fix(cart): prevent duplicate items on add"

# Mauvais commits
git commit -m "fix"
git commit -m "wip"
```

---

## Pousser une branche

```bash
# Première fois
git push -u origin nom-de-la-branche

# Fois suivantes
git push
```

---

## Ouvrir une Pull Request

1. Va sur le repo GitHub
2. Clique sur "Compare & pull request" ou onglet Pull requests > New pull request
3. Vérifie les branches : base (destination) et compare (ta branche)
4. Remplis le titre et la description
5. Clique sur "Create pull request"

---

## Nommer une Pull Request

Même convention que les commits :

```
type(scope): description claire et concise
```

```bash
# Bons titres
feat(auth): add OAuth2 login with Google
fix(cart): prevent duplicate items when clicking fast

# Mauvais titres
fix bug
WIP
mon travail du jour
```

### Template de description

```markdown
## Contexte
Pourquoi cette PR ? Quel problème résout-elle ?

## Changements effectués
- Ajout de X
- Modification de Y

## Comment tester
1. Aller sur...
2. Cliquer sur...
3. Vérifier que...

## Liens
Closes #42
```

---

## Maintenir son fork à jour

```bash
git fetch upstream
git checkout main
git merge upstream/main
git push origin main
```

### Rebaser sa branche de travail

```bash
git checkout feat/ma-feature
git rebase main
git push --force-with-lease origin feat/ma-feature
```

---

## Résumé — Workflow complet

```
1.  Fork du repo sur GitHub
2.  git clone git@github.com:TON-COMPTE/repo.git
3.  git remote add upstream git@github.com:ORIGINAL/repo.git
4.  git checkout main && git pull upstream main
5.  git checkout -b feat/ma-fonctionnalite
6.  # coder, tester
7.  git add .
8.  git commit -m "feat(scope): description claire"
9.  git push -u origin feat/ma-fonctionnalite
10. Ouvrir une Pull Request sur GitHub
11. Review > corrections > merge
12. git checkout main && git pull upstream main
13. git branch -d feat/ma-fonctionnalite
```

---

## Commandes utiles

```bash
# Lister les branches
git branch -a

# Supprimer une branche locale
git branch -d feat/ma-branche

# Supprimer une branche distante
git push origin --delete feat/ma-branche

# Voir les remotes
git remote -v

# Voir le log de façon graphique
git log --oneline --graph --all

# Annuler le dernier commit en gardant les fichiers
git reset --soft HEAD~1

# Stasher des modifications non committées
git stash
git stash pop

# Quitter le pager (git log)
q

# Voir la différence entre ta branche et main
git diff main...HEAD
```
