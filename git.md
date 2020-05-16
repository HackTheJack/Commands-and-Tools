# Breve guida a git

## Divisione

Git viene diviso in tre aree.

1. Working Directory

2. Staging Area 

3. .git directory repository

### Iniziare un progetto

`git init`

### Creare il file .gitignore

In questo file ci vanno i file che non vogliamo siano caricati su git.

Esempio:

```text
.project
.dbcred.php
*.pyc
```

### Aggiungere file alla staging area

La staging area permette di scegliere su quali file fare il commit, per sempio se voglio fare un commit per ogni file li aggiungo uno a uno alla staging area.

`git add nomefile`

`git add -A`

### Togliere file dalla staging area

`git reset nomefile`

oppure toglierli tutti 

`git reset`

### Eseguire un commit

Sposto i file dalla staging area al git repository locale

`git commit -m "primo commit"`

## git remoto

### Clonare un repository

`git clone <url> <where to clone>`

Per indicare la directory locale mettere il .

### Informazioni su remoto

`git remote -v`

Fornisce informazioni sul repository remoto

`git branch -a`

Fornisce informazioni sui branch locale e remoto

### Vedere le differenze

`git diff`

Fa vedere le modifiche effettuate sui file

### Prima di caricare i file sul repository remoto

`git pull origin master`

Scarica le modifiche presenti sul remoto e non presenti sul locale. Necessario prima di caricare i file sul remoto

### Caricare i file sul repository remoto

`git push origin master`

---

## Common workflow

Normalmente non si lavora sul master ma su un branch quindi

### 1. creo il branch

`git branch branch-di-lavoro`

### 2. lo imposto come branch-di-lavoro

`git checkout branch-di-lavoro`

### 3. aggiungo i file alla staging area

`git add -A`

### 4. faccio il commit per spoatarli nel git repositori

`git commit -m "metterò file nel branch di lavoro"`

### 5. carico i file sul branch di lavoro

`git push -u origin branch-di-lavoro`

Con l'opzione -u impostiamo il repository di lavoro e la prossima volta basta solo fare 

`git push`

--- 

Quando ho deciso che è la versione definitiva posso fare il merge del branch di lavoro su quello master

### 6. imposto il branch master

`git checkout master`

### 7. scarico le modifiche dal master

`git pull origin master`

### 8. eventuale controllo quali branch sono stati già uniti in precedenza (merged)

`git branch --merge`

### 9. faccio il merge

Dato che sono su master posso fare il merge del branch-di-lavoro

`git merge branch-di-lavoro`

### 10. carico le modifiche

`git push origin master`

### 11. controllo che ci sia stato il merge

`git branch --merge`

### 12. Cancello branch di lavoro in locale

`git branch -d branch-di-lavoro`

### 13. Cancello branch di lavoro remoto

`git push origin --delete brach-di-lavoro


---

## Impostare il remote

### con https

`git remote add origin https://<username>:<password>@github.com/arEcofor/statistica`

### con SSH

Prima bisogna creare le chiavi e importarle su gitHub https://help.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh

poi

`git remote add origin git@github.com:username/repo-name-here.git`

### per verificare l'origin impostata

`git remote get-url origin`

### per modificare l'origin

`git remote set-url origin git@github.com:runcioa/RyanTelegramFare`

---

#### Fonti

* [video esplicativo](https://www.youtube.com/watch?v=HVsySz-h9r4&list=PL-osiE80TeTuRUfjRe54Eea17-YfnOOAx)
