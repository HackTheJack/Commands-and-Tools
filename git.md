# Breve guida a git


## Divisione

Git è suddiviso in tre aree:

1. Working Directory
   
   #### Sono contenuti i file locali sulla propria macchina

2. Staging Area 
   
   #### Vengono inseriti i file modificati ma non ancora pubblicati nel repository ufficiale

3. Head
   #### La "testa" del repository remoto dove inseriamo le nostre modifiche dalla _staging area_



## Iniziare un progetto

Per iniziare un nuovo progetto, creiamo una nuova cartella, accediamoci, e lanciamo il comando

`git init`

Questo crea un nuovo **repository** con un cosiddetto _branch_ **master**



## Clonare un repository

Il repository remoto creato dovrà essere collegato con la nostra parte locale. Utilizziamo il comando `clone`

`git clone <url> <where to clone>`



## Aggiungere file alla staging area

La **staging area** permette di modificare i nostri file in modo sicuro. Possiamo scegliere quali file inviare nella _staging area_ con il comando `add` e successivamente inviarli nell'Head con il comando `commit`.

Un tipico esempio può essere:

`git add <filename>`

Se vogliamo aggiungere più file modificati, possiamo utilizzare 

`git add -u`



## Rimuovere file dalla staging area

Se abbiamo aggiunto per sbaglio un file, possiamo toglierlo con il comando `reset`

`git reset <filename>`

oppure rimuoverli tutti con

`git reset`



## Eseguire un commit

Una volta aggiunti i file nella staging area, possiamo effettuare il _commit_ per spostartli nell'area Head

`git commit -m "Commit message to explain what we did here"`



## Inviare la modifiche nel repository remoto

I nostri file "committati" si trovano su Head, ma sono ancora in locale. Per poterli inviare sul repository remoto dobbiamo usare il comando `push`

`git push origin master`

NOTA: **master** rappresenta il branch di default per ogni progetto, ma è possibile specificare altri branch.

### Branching

I branch sono creati per aggiungere modifiche isolate le une dalle altre, in modo da non rompere il flusso principale del progetto; un branch creato può essere poi unito a quello principale una volta completata la nostra modifica.

![branch](https://rogerdudler.github.io/git-guide/img/branches.png)


Ad esempio, possiamo creare un branch chiamato `dev` con il comando

`git checkout -b dev`

il cui output conferma che ci siamo spostati su tale branch

```
Switched to a new branch 'dev'
```

Per tornare al branch _master_ basta usare il comando `checkout` in questo modo 

`git checkout master`

ed eventualmente cancellare il branch creato con `branch -d`

`git branch -d dev`

```
Deleted branch dev (was 00e49cb).
```



## Informazioni sul repository remoto

Il comando `remote` fornisce informazioni sul repository remoto

`git remote -v`

```
origin	https://github.com/<user>/<project>.git (fetch)
origin	https://github.com/<user>/<project>.git (push)
```



## Informazioni sul branch

Il comando

`git branch`

ci dice su quale branch stiamo operando, mentre se vogliamo conoscere tutti i branch collegati al repository eseguiamo

`git branch -a`

```
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/master
```



## Vedere lo stato del repository

Un comando molto utile (e da usare dopo ogni modifica effettuata **prima** di aggiungere o fare commit, è il comando `status`

`git status`

```
On branch master
Your branch is up-to-date with 'origin/master'.
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   <file1>

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	untracked-file1
  untracked-file2
	untracked-file3

no changes added to commit (use "git add" and/or "git commit -a")
```
in questo caso vediamo che c'è un file `file1` che è stato modificato ed è pronto per essere inserito nella staging area con il comando `add`, mentre ci sono 3 file che sono _untracked_ . Questo significa che ogni modifica effettuata su questi file non sarà contata, a meno di non aggiungerli tra i file che vogliamo considerare. Un repository può (ed ha) file che non vogliamo facciano parte della parte remota.



## Vedere le differenze

Ogni volta che facciamo una modifica ad un file, git tiene traccia del file originale e lo confronta con quello modificato. Con il comando `diff` possiamo vedere le nostre modifiche

`git diff`

```
diff --git a/prova.h b/prova.h
index 4a7cd15..57f3165 100644
--- a/prova.h
+++ b/prova.h
@@ -7,15 +7,16 @@
 #include <linux/types.h>
 
 struct struct_prova {
-       
-       int hack_the_lower;
+       int hack_the_tower;
```



## Update

Per aggiornare il proprio repository locale con eventuali modifiche fatte in remoto da altri utenti che hanno accesso allo stesso, utilizzare il comando `pull`

`git pull`

In questo caso si scaricano le eventuali modifiche sa remoto per il branch `master` e si uniscono automaticamente al nostro branch.

Se invece non siamo sul branch master, dobbiamo specificare il nome con `origin <branch>`

`git pull origin dev`



## Merge

E' possibile unire le modifiche di un branch con il nostro attivo usando il comando `merge`.
Tipicamente questo comando lo si usa per portare le modifiche di un branch esterno dentro il branch attivo.

Per esempio, se abbiamo `master` e `dev`, e vogliamo fare il _merge_ di _dev_ in _master_, assicuriamoci di essere nel branch master ed effettuiamo

`git merge <branch>`

Il merge andrà a buon fine se non ci sono conflitti tra i due branch, cosa che purtroppo può capitare.
In questo caso, si devono modificare i file che creano conflitti e riaggiungerli nell'area di stage con `git add <filename>`

---


## Common workflow

### 1. Creo il branch di lavoro

`git branch -b <branch_name>`

### 3. Aggiungo i file modificati alla staging area

`git add -u`

### 4. Effettuo il commit per spoatarli nell'area Head

`git commit -m "this commit explain my changes"`

### 5. Effettuo il push dei commit nel repository remoto

`git push -u origin <branch_name>` (se il branch non esiste ancora in remoto)

`git push origin <branch_name>` (se il branch è presente in remoto)

--- 

## Forkare un progetto e sincronizzarlo con l'originale

### Configurare e sincronizzare un punto remoto per il fork

1. Visualizzare la lista dei _repository_ remoti per il _fork_
```
$ git remote -v
> origin  https://github.com/YOUR_USERNAME/YOUR_FORK.git (fetch)
> origin  https://github.com/YOUR_USERNAME/YOUR_FORK.git (push)
```
2. Specificare un nuovo repository remoto _upstream_ che sarà sincronizzato con il _fork_
```
$ git remote add upstream https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git
```
3. Verificare il nuovo _upstream_ repository specificato per il fork
```
$ git remote -v
> origin    https://github.com/YOUR_USERNAME/YOUR_FORK.git (fetch)
> origin    https://github.com/YOUR_USERNAME/YOUR_FORK.git (push)
> upstream  https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git (fetch)
> upstream  https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git (push)
```

### Sincronizzare il fork

1. Aggiornare i _branches_ e i rispettivi _commits_ dal repository _upstream_ . I _commits_ del **master** saranno salvati nel branch locale `upstream/master`
```
$ git fetch upstream
> remote: Counting objects: 75, done.
> remote: Compressing objects: 100% (53/53), done.
> remote: Total 62 (delta 27), reused 44 (delta 9)
> Unpacking objects: 100% (62/62), done.
> From https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY
>  * [new branch]      master     -> upstream/master
```
2. Controllare il branch `master` locale
```
$ git checkout master
> Switched to branch 'master'
```

3. "Mergiare" le modifiche dal branch remoto `upstream/master` nel nostro `master`. Questo passaggio permette la sincronizzazione tra il nostro fork e il repository originale.
```
$ git merge upstream/master
> Updating a422352..5fdff0f
> Fast-forward
>  README                    |    9 -------
>  README.md                 |    7 ++++++
>  2 files changed, 7 insertions(+), 9 deletions(-)
>  delete mode 100644 README
>  create mode 100644 README.md
```

## Altri comandi utili

1. `git log` - per vedere i vari commit presenti nel repository
2. `git checkout -- <filename>` - per eliminare le modifiche effettuate in locale su un file
3. `git reset HEAD~` - per eliminare l'ultimo commit locale
4. `git cherry-pick <commit-hash>` per passare un commit da un branch al nostro attivo


#### Fonti
* [GitHub fast guide](https://rogerdudler.github.io/git-guide/)
* [video esplicativo](https://www.youtube.com/watch?v=HVsySz-h9r4&list=PL-osiE80TeTuRUfjRe54Eea17-YfnOOAx)
