# Git - мои заметки

## Ключевые концепции:
- **Blob** - содержимое файла
- **Tree** - структура каталога
- **Commit** - снимок + метаданные
- **HEAD** - указатель на текущую ветку

## Команды, который выучил
| Команда | Действие |
|---------|----------|
| `git init` | Создать репозиторий |
| `git clone <url>` | Клонировать репозиторий |
| `git status` | Состояние рабочего каталога |
| `git add .` | Добавить все изменения в staging |
| `git add <file>` | Добавить конкретный файл в staging |
| `git restore <file>` | Отменить изменения в файле |
| `git restore --staged <file>` | Убрать файл из staging |
| `git commit -m` | Создать коммит |
| `git commit --amend` | Изменить последний коммит |
| `git log --oneline` | Краткая история |
| `git log --oneline --graph --all` | Дерево веток |
| `git diff` | Изменения в working dir |
| `git diff --staged` | Изменения в staging |
| `git show HEAD` | Посмотреть последний коммит |
| `git stash` | Убрать изменения в карман |
| `git stash pop` | Вернуть из кармана |
| `git branch` | Список веток |
| `git switch -c <name>` | Создать и переключиться на ветку |
| `git switch <name>` | Переключиться на ветку |
| `git merge <branch>` | Смёржить ветку |
| `git branch -d <name>` | Удалить ветку |
| `git remote -v` | Список remote |
| `git push` | Запушить изменения |
| `git push -u origin <branch>` | Запушить новую ветку |
| `git push origin --delete <branch>` | Удалить ветку на GitHub |
| `git pull` | Получить и применить изменения |
| `git fetch` | Получить изменения без применения |
| `git cat-file -t <hash>` | Тип объекта |
| `git cat-file -p <hash>` | Содержимое объекта |
