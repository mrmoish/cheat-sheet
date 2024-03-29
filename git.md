GİT - Global Information Tracker
================================

Attention
---------

> Понятие «голова списка» (HEAD) в Git присутствует явно и активно используется для разных операций. 

> Сам список коммитов тоже имеет название, вы его уже видели: это — main. В терминологии Git такой список называется веткой (branch). Именно поэтому команда для показа текущего местоположения в истории называется git branch

> ветка в Git — это просто подвижный указатель на один из коммитов. При каждом новом коммите указатель сдвигается вперед автоматически.

> git reflog - историю изменения для поиска коммитов, которые вы могли внезапно потерять, переписывая историю

> --amend — добавить изменения в последний коммит или переименовать последний коммит.
> работает только ветке где сделан последний комминт.
> [отмена](https://stackoverflow.com/questions/1459150/how-to-undo-git-commit-amend-done-instead-of-git-commit)

> [Восстановление удаленного коммита/ветки](https://webdevkin.ru/courses/git/git-merge)


QuickStart
----------
### 1. Инициализация 
```
git init
```
or
(где
[master](https://stackoverflow.com/questions/64249491/why-does-git-push-main-work-on-github-when-git-push-master-does-not-also-wh)
 по-умолчанию)
```
git init -b main
```

### 2. Создание и коммит

```
git commit --allow-empty -m "GENESIS"
```
or
```
echo 'Hola! Hi! Привет! Merhaba!' > README.md
git add README.md
git commit -m 'chore: add README'
```

### 3. Добавления и связывания с удаленным  репозиторием
```
git remote add origin https://github.com/mrmoish/site.git
git push -u origin main
```
для удаления связи
```
git remote remove origin
```
> origin - это имя (alias) удаленного репозитория https://github.com/mrmoish/site.git

> origin == https://github.com/mrmoish/site.git

> -u или --set-upstream - флаг устанавливает текущую локальную ветку в отслеживание (upstream) указанной удаленной ветки

Типы веток
---------
```
wip/       Works in progress/ в процессе
feat/      Feature/ новый функционал
bug/       Исправление ошибки
junk/      Мусорка/ для экспериментов
hot/       Быстрое устранение критических проблем
release/   Подготовка  к релизу 
docs/      Документирование 
dev/       ??
```

Типы коммитов
-------------
- feature — добавлен новый функционал уровня приложения
- fix — исправили серьезный баг
- docs — документации
- style — опечатки, форматирование
- refactor — рефакторинг
- test — тесты и тестированием
- chore — обычное обслуживание кода

Aliases(Псевдонимы)
-------------------
### в файле ~/.gitconfig

```sh
[alias]
	st = status
	co = checkout
	br = branch
	lg = log --all --graph  --oneline
```
[статья](https://git-scm.com/book/en/v2/Git-Basics-Git-Aliases)

### в файле .bashrc(.zshrc)
shortcut git in zsh and bash
```sh
alias gd='git diff'
alias gds='git diff -staged'
```





Работа в команде 
----------------
[статья](https://nuancesprog.ru/p/1832/)

I try to remeber these git commands
----------------------------

### перемещать изменения между ветками 

```
git stash
```
```
git stash pop
```
```
git stash drop
``` 

### to rename a commit in  history
```
git rebase -i HEAD~3
```
1. 'pick' замнаем на  'reword' перед нужным каммитом в первом редакторе
2. В следущем редакторе новое имя коммита


### need to know more

```
git pull # git fetch (получение изменений с сервера) + git merge (сливание в локальную копию).

git fetch # загрузка содержимого из удаленного репозитория (витека master)

git reflog # история коммитов, на которые указывал HEAD

git merge dev # слить изменения из ветки “dev” в ветку “master”, нам необходимо перейти на ветку “master” и в ней выполнить это

git branch -d <branch_name> # удалить ветку
```



### committing well
```sh
# for p - patcht
## g - перейти к некоторой части файла (g - показывает список частей и затем выполняет переход, g<N> - перейти к части N)
## / - найти часть, соответствующую регулярному выражению
## s - разбить текущую часть на части меньшего размера
## j J - отложить принятие решения по этой части, перейти к следующей части, решение по которой не принято
## k K - отложить принятие решения по этой части, перейти к предыдущей части, решение по которой не принято
git add -i # can choose changes in the file


igit commit file1 file2 # include git add file1 and file 2
git commit f1 f2 -m 'name commit' # (не для файлов которых нет в индексе😔)

git add . # gid add all files
git commit -a # include git add . (кроме файлов которых нет в индексе😔)
```

### search
```sh
git blame file # каждую строку файла и тот кто ее последний раз изменял

git grep -i keyword # without register
git grep Hexlet 5120bea3 # Поиск в конкретном коммите
git grep Hexlet $(git rev-list --all) # rev-list возвращает список хешей коммитов
```

### restore
```sh
git restore file
git restore --staged <file>... # cancel changes in index
```

### изменения добавленые в индеск
`git diff --staged`

### create ssh-key  
`ssh-keygen -t ed25519 -C 'mail'`

### получить pub ssh-key который нужно добавить на github
`pbcopy < ~/.ssh/id_ed25519.pub`
`cat ~/.ssh/id_ed25519.pub`

### проверка ssh соеденения с github
`ssh -T git@github.com`


### add ssh-key  

```sh
#без этой команды будет всегда запрашивать пароль при работе с github
ssh-add /.ssh/id_ed25519
```

### удалить принудительно[-f] неотслеживаемые файлы и directory [-d] 
```sh
git clean -fd 
```

### новвые коммиты с обратными изменениями
🟡 думаю проще использовать checkout и commit вместо этого |
[more](https://stackoverflow.com/questions/4114095/how-do-i-revert-a-git-repository-to-a-previous-commit/4114122#4114122)
```sh
git revert 0d1d7fc..HEAD
git revert HEAD~2..HEAD
```

### delete commits **permanently**
🔴 ْunsafe | небезопасно
### 
```
git reset --soft 0d1d7fc32 # содержимое вашего индекса, а также рабочей директории, остается неизменным.
git reset --mixed  HEAD~2 # мы опять-таки изменим ссылку указателя HEAD, но все предыдущие изменения в индекс не попадут, а будут отслеживаться как не занесенные в индекс.
git reset --hard <commit> # мы снова изменим ссылку указателя HEAD, но все предыдущие изменения не попадут ни в индекс, ни в зону отслеживаемых файлов. 

# очистить индекс, все изменения удалятся из индекса (безопсно), они останутся в раб дир, но не будут готовы к комиту
git reset --mixed (без этого можно)
git reset

# отменить коммит git в удаленном репозитории
git push -f origin
```


I already know well that git commandso
-------------------------------------



```
git init
git status
git diff
git log --oneline # short version
git log -p # with diff
git show a3c0bf8a
git checkout a3c0bf8
git add

git commit -m 'name commit'
git push

git clone git@github.com:nikname/name-project
# указывает глубину клонирования, ограничивая количество истории коммитов
git clone --depth=10 (...)
```


## Question

### куда попадают изменеия при revert

изменения есть в рабочей области  
но еще не добавлны в индекс  
не подготовлены к коммиту
```sh
mr_vi@127 cheat-sheet % git status       
On branch master
You are currently reverting commit 51d929c.
  (all conflicts fixed: run "git revert --continue")
  (use "git revert --skip" to skip this patch)
  (use "git revert --abort" to cancel the revert operation)

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   README.md
```

изминения в индексе  
изменения готовы к коммиту

```sh
mr_vi@127 cheat-sheet % git status       
On branch main
Your branch is up to date with 'origin/main'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   git.md
```

когда использую revert изменения не в рабочей области и не в индексе, но видут себя как в индексе  
[может только когда использую revert с ошибкой не указываею диапозон комитов]
```sh
mr_vi@127 cheat-sheet % git status       
On branch master
You are currently reverting commit 16c2578.
  (fix conflicts and run "git revert --continue")
  (use "git revert --skip" to skip this patch)
  (use "git revert --abort" to cancel the revert operation)

Unmerged paths:
  (use "git restore --staged <file>..." to unstage)
  (use "git add <file>..." to mark resolution)
	both modified:   README.md
```


### Bash Completion don't work 😡
[there](https://sourabhbajaj.com/mac-setup/BashCompletion/) 
and
i don't follow it
[PS1 for bash](https://ru.hexlet.io/blog/posts/kak-prisoedinitsya-k-rabote-nad-opensorsom-chto-takoe-ps1-i-drugie-voprosy-otvechaet-razrabotchik-heksleta-andrey-moshkov#chto-takoe-ps1-i-dlya-chego-ispolzuetsya) 

> git switch -
> `git checkout main`
> `git branch`
  
> Если добавить имя файла в конец команды git log, отделив его знаками --, можно увидеть, в каких коммитах он изменялся  
  
> [Trunk Basd/ пробема слияний веток](https://habr.com/ru/post/534882/)[
> [more](https://trunkbaseddevelopment.com)
> Trunk Based Development - отличная модель ветвления, которая наконец-то поможет вам избавится от кошмара слияния веток, позволит получить больше контроля над кодом, а команду сделать более дисциплинированной, превратит "теневое внедрение" из просто интересного приема в обыденность.

> 'git log --graph'  
  
## example .gitignore
  
```  
# В этом файле можно оставлять комментарии
# Имя файла .gitignore
# Файл нужно создать самостоятельно

# Каждая строчка — это шаблон, по которому происходит игнорирование

# Игнорируется файл в любой директории проекта
## access.log

# Игнорируется директория в любой директории проекта
## node_modules/

# Игнорируется каталог в корне рабочей директории
## /coverage/

# Игнорируются все файлы с расширением sqlite3 в директории db,
# но не игнорируются такие же файлы внутри любого вложенного каталога в db
# например, /db/something/lala.sqlite3
## /db/*.sqlite3

# игнорировать все .txt файлы в каталоге doc/
# на всех уровнях вложенности
## doc/**/*.txt
```

[more usefull](https://github.com/github/gitignore)

git log --grep="add note about installing git on linux"

git pull --rebase

$ git rm --cached README (удалить файл из индекса, оставив его при этом в рабочем каталоге)
