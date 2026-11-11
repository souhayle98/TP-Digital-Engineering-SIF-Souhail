# TP-Digital-Engineering-SIF-Souhail

## 1. Présentation de l'étudiant 

- **Nom :** SIF
- **Prénom :** Souhail
- **Formation :** Informatique & ingénierie des données
- **GitHub :** [Mon profil GitHub](https://github.com/souhayle98)

## 2. Dépôts GitHub réalisés

### Exercice 1 : Calcul en langage C

- **Nom du dépôt :** calcul-c
- **Lien GitHub :** [calcul-c](https://github.com/souhayle98/calcul-c)

**Description :**

Réalisation d'un programme en langage C permettant d'effectuer le cacul de la somme de 2 nombres. Utilisation de GCC pour la compilation et l'exécution du programme.

### Exercice 2 : Travail collaboratif en binôme

- **Nom du dépôt :** calcul-c-equipe
- **Lien GitHub :** [calcul-c-equipe](https://github.com/souhayle98/calcul-c-equipe)

**Description :**

Réalisation d'un travail collaboratif en binôme à l'aide de Git et GitHub.

- **Mon rôle :**  propriétaire du dépôt (Etudiant A)
- **Nom&Prénom(Etudiant B) :** Ait Addi youssef
- **Pull Request fusionnée :** [Lien vers la Pull Request (PR) fusionnée](https://github.com/souhayle98/calcul-c-equipe/pull/1)
  
## Historique des commandes utilisées (Demandé par le prof)
### Exercice 1 : Du dépôt local à GitHub
#### 1. Créer le dossier, `main.c`, initialiser Git
```bash
mkdir calcul-c
cd calcul-c
```
Créer `main.c` dans l'éditeur, avec ce contenu :
```c
#include <stdio.h>

int main(void) {
    printf("Bienvenue dans calcul-c !\n");
    return 0;
}
```
```bash
git init
git status
```
**Rôle de `.git`** : dossier caché qui contient toute la base du dépôt (historique des commits, branches, configuration, références distantes). Le supprimer revient à supprimer le dépôt Git (les fichiers de travail restent, mais sans historique).

#### 2. Configuration locale
```bash
git config user.name "sif"
git config user.email "sifsouhail26@gmail.com"
git config --local --list
```
**Différence** : sans option (ou avec `--local`), la configuration s'applique **uniquement à ce dépôt** (`.git/config`). Avec `--global`, elle s'applique à **tous les dépôts** de l'utilisateur (`~/.gitconfig`).

#### 3. Premier commit
```bash
git add main.c
git commit -m "Initialiser le projet C"
git status
git log --oneline
```

#### 4. Somme de deux entiers, second commit
Modifier `main.c` dans l'éditeur (sans enregistrer pour l'instant dans Git) :
```c
#include <stdio.h>

int main(void) {
    int a, b;
    printf("Entrez deux entiers : ");
    scanf("%d %d", &a, &b);
    printf("Somme = %d\n", a + b);
    return 0;
}
```
```bash
git diff                 # différences non préparées
git status
git add main.c
git diff --staged        # différences préparées (équivalent : --cached)
git commit -m "Calcul la somme de 2 nombres"
```

#### 5. `.gitignore`, `README.md`, troisième commit
Créer `.gitignore` dans l'éditeur :
```
calcul
calcul.exe
*.o
```
Créer `README.md` dans l'éditeur :
```markdown
# calcul-c
Petit programme en C qui lit deux entiers et affiche leur somme.

## Compilation
    gcc main.c -o calcul
    ./calcul
```
```bash
git add .gitignore README.md
git commit -m "Ajouter Readme file & .gitignore pour exclure les exécutables"

gcc main.c -o calcul.exe # compilation pour vérifier l'ignore
.\calcul.exe             #Exéction
git status               # "calcul" ne doit pas apparaître
git ls-files             # seuls main.c, .gitignore, README.md sont suivis
```

#### 6. Publier sur GitHub
Créer d'abord sur GitHub un dépôt **public** `calcul-c`, **sans** README initial.
```bash
git branch -M main
git remote add origin https://github.com/<utilisateur>/calcul-c.git
git remote -v
git push -u origin main
```
Vérifier sur GitHub la présence des trois commits (onglet *Commits*).

#### 7. Modification mineure, commit et push
Modifier légèrement `main.c` dans l'éditeur (par exemple le message d'invite), puis :
```bash
git add main.c
git commit -m "Améliorer le message d'invite"
git push
```
**Différence** : `git commit` enregistre une version **localement** (dans le dépôt local), alors que `git push` **envoie** les commits locaux vers le dépôt distant (GitHub).

---

### Exercice 2 : Commandes de l'étudiant A

#### 1. Création et clonage
Sur GitHub : créer `calcul-c-equipe` **avec** un `README.md` initial, puis inviter B (*Settings → Collaborators*).
```bash
git clone https://github.com/<utilisateurA>/calcul-c-equipe.git
cd calcul-c-equipe
git status
git branch                # branche active
git remote -v             # références distantes
git log -1                # dernier commit
```

#### 2. Ajouter `main.c` et publier
Créer `main.c` dans l'éditeur :
```c
#include <stdio.h>

int main(void) {
    printf("Projet collaboratif\n");
    return 0;
}
```
```bash
git add main.c
git commit -m "Ajouter main.c initial"
git push origin main
```
*(Côté B : `git fetch` puis `git pull`.)*
**Comparaison** : `git fetch` télécharge les nouveaux commits distants **sans les intégrer** à la branche courante ; `git pull` = `git fetch` + intégration (merge) dans la branche courante.

#### 4. Examiner et fusionner la pull request de B
Sur GitHub : onglet *Pull requests* → ouvrir la PR `feature/produit` → *Files changed* pour examiner → *Merge pull request* → *Confirm merge*.

Mettre ensuite à jour son dépôt local :
```bash
git switch main
git pull
```

#### 5. Branche `feature/moyenne`, fusion locale, publication
```bash
git switch -c feature/moyenne
```
Ajouter dans `main.c` (avec l'éditeur) :
```c
float moyenne(int a, int b) {
    return (a + b) / 2.0f;
}
```
```bash
git add main.c
git commit -m "Ajouter la fonction moyenne"
git switch main
git pull                          # récupérer d'abord la fusion de feature/produit
git merge feature/moyenne
git push origin main
git log --oneline --graph --all   # vérification
```

#### 6. Renommer puis supprimer une branche locale
```bash
git branch demo-test
git branch -m demo-test demo-renommee
git switch main
git branch -d demo-renommee
```
- **Pourquoi la suppression d'une branche active échoue** : Git refuse de supprimer la branche sur laquelle on se trouve ; il faut d'abord basculer sur une autre branche (`git switch main`).
- **`-d` vs `-D`** : `-d` supprime uniquement si la branche est déjà fusionnée (sécurisé) ; `-D` force la suppression même si des commits ne sont pas fusionnés (ils peuvent être perdus).

#### 8. Commandes de contrôle final
```bash
git branch                        # branche active
git remote -v                     # dépôts distants
git status                        # état des fichiers
git log --oneline --graph --all   # historique final
```

## 3. Bilan des commandes Git

### 3.1. git status

```bash
git status
```
Cette commande permet de vérifier l'état du dépôt Git 

### 3.2. git remote -v

```bash
git remote -v
```
Cette commande permet d'afficher les adresses des dépôts distants configurés.

### 3.3. git log --oneline --graph --all

```bash
git log --oneline --graph --all
```

Cette commande permet d'afficher l'historique des commits sous forme graphique et condensée.

- `--oneline` : affiche chaque commit sur une seule ligne.
- `--graph` : représente graphiquement les branches et les fusions.
- `--all` : affiche les commits de toutes les branches.
