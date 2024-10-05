# Git


prima di utilizzare git è meglio configurare le nostre credenziali:
```sh
git config --global user.name <username>
```
```sh
git config --global user.email <email>
```
togliendo la flag "global" è possibile modificare i parametri solo per la repository 

In caso volessimo modificare il nome con cui viene inizializzato il branch principale dellla repository:
```sh
git config --global init.defaultBranch <nomeBranchDefault>
```


Per creare una repositori utilizziamo il seguente comando in una cartella:
```sh
git init
```

quando facciamo delle modifiche dobbiamo prima stagearle. 
O un file alla volta:
```sh
git add <file>
```
o tutte insieme:
```sh
git add --all
```

>[!info]
>--all = -A

per vedere se i file sono stageati o no usiamo status.
la flag short ci permette di vederli in una maniera più veloce.
```sh
git status --short
```
>[!info]
>**Note:** con la flag short prima dei file appariranno questi simboli:
>
>- ?? = Untracked files
>- A = Files added to stage
>- M = Modified files
>- D = Deleted files

per committare
```sh
git commit -m <message>
```
aggiungendo la flag -a skippa la fase di staging

Possiamo vedere la cronologia dei commit con questo comando:
```sh
git log
```
Possiamo spostarci tra i vari commit così:
```sh
git checkout <idCommit>
```
per tornare all'ultimo commit:
```sh
git checkout <nomeMainBranch>
```
alternativamente per tornare indietro di un checkout:
```sh
git switch -
```

### Branches
per visualizzare i branch:
```sh
git branch
```
ci sarà un asterisco a sinistra del branch corrente

per creare un branch:
```
git branch <nomeNuovoBranch>
```

con questo comando possiamo cambiare il nome a un branch
```
git branch -m <nomeVecchio> <nomeNuovo>
```

per spostarci tra i branch usiamo il seguente comando:
```
git checkout <branchTarget>
```
>[!info]
>con il parametro "-b" il comando checkout creerà un nuovo branch e ci si sposterà dentro 
# Github

per autenticare github da linux:
```sh
gh auth login -wp "https"
```
se le flag non funzionano usare semplicemente:
```sh
gh auth login
```


settiamo la repo di github nella nostra repo preesistente
```
git remote add origin <httpsRepo>
```

se la repo in cloud è già avanti conviene iniziare con un clone al posto di fare la cartella, poi la init, poi la add e poi il pull:
```
git clone <URL>
```

Per aggiornare la repo locale con quella cloud:
```
git pull origin <branch>
```

con il seguente comando possiamo aggiornare il nostro branch anche se abbiamo già committato delle modifiche,mantenendole, 
```
git pull origin --rebase branch
```
>[!info]
>in caso di conflitto bisognerà comportarsi come se fosse un merge

per pushare
```
git push origin <branch>
```
oppure
```
git push origin <branchLocale>:<branchCloud>
```