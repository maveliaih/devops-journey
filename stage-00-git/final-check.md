# Финальная проверка: Git + GitHub

## Вопрос 1
**В чём принципиальная разница между git fetch и git pull?**

git fetch — скачивает изменения из remote, но не применяет их.
Можно сравнить через git log origin/main и решить применять или нет.
git pull — fetch + merge в одном шаге, изменения применяются сразу.

fetch предпочтителен в командной работе — сначала смотришь что изменилось, потом решаешь.

---

## Вопрос 2
**Почему создание новой ветки — мгновенная операция?**

Ветка — это просто текстовый файл в .git/refs/heads/ с одним хешем коммита.
Создание ветки = создание этого файла. Никакие файлы проекта не копируются —
поэтому операция мгновенная и не зависит от размера репозитория.

---

## Вопрос 3
**fast-forward vs merge commit**

Если в main не было новых коммитов пока работал в feature/nginx —
будет fast-forward, история линейная, merge commit не создаётся.

---

## Вопрос 4
**Случайно закоммитил .env с паролями и запушил на GitHub**

1. git rm --cached .env
2. Добавить .env в .gitignore
3. git commit -m "chore: remove .env from tracking"
4. git push

Важно: файл уже в истории Git — история публична.
Все пароли и токены из .env считаются скомпрометированными — менять обязательно.

---

## Вопрос 5
**error: Updates were rejected because the remote contains work you do not have locally**

На remote есть изменения которых нет локально.
Решение: git pull — подтянуть изменения, потом git push.

git push --force нельзя — перезапишет remote, чужие изменения будут потеряны.

---

## Вопрос 6
**Два отдельных коммита, не закоммитить notes.txt**

git add app.py
git commit -m "feat: add user authentication"

git add config.py
git commit -m "fix: update database settings"

notes.txt добавить в .gitignore — не будет маячить в git status.

---

## Вопрос 7
**HEAD detached at a3f2c1d**

HEAD указывает на конкретный хеш коммита вместо ветки.

Причины:
- git checkout <hash>
- git checkout v1.0 или git checkout origin/main
- интерактивный rebase

Решения:
1. Если изменений не было: git switch main
2. Если были изменения — сохранить их:
   git switch -c новая_ветка
3. Перенести в main:
   git switch -c temp
   git switch main
   git merge temp
   git branch -d temp

---

## Вопрос 8
***.log в .gitignore, но server.log всё равно в git status**

Файл был добавлен в .gitignore после того как уже трекался Git.
.gitignore не действует на уже отслеживаемые файлы.

Исправить:
git rm --cached server.log

Если таких файлов много:
git rm -r --cached .
git add .
git commit -m "chore: remove tracked files from .gitignore"

---

## Вопрос 9
**git commit --amend / git revert HEAD / git reset --hard HEAD~1**

git commit --amend
- Перезаписывает последний коммит, создаёт новый хеш
- Безопасно: только если коммит ещё не запушен
- Опасно: если уже в remote — потребует --force, сломает историю у других

git revert HEAD
- Создаёт новый коммит который отменяет изменения предыдущего
- Безопасно всегда — история не переписывается
- Используй если коммит уже в remote

git reset --hard HEAD~1
- Полностью удаляет коммит и все изменения в файлах
- Безопасно: только локально и если коммит не запушен
- Опасно: данные удаляются. Восстановить можно через git reflog
  в течение 90 дней — но это крайний случай, не стандартный инструмент

---

## Вопрос 10
**Организация Git в команде из 5 человек**

Именование веток:
feat/123-user-authentication
fix/45-nginx-port-binding
chore/67-update-gitignore
docs/89-add-readme

Когда создаём PR:
- Draft PR — задача в процессе, нужна ранняя обратная связь
- PR — задача полностью готова к merge

При review проверяем:
- Логика — код делает то что должен
- Стиль — соответствует conventions команды
- Безопасность — нет секретов, нет уязвимостей
- Тесты — код покрыт если требуется
- Документация — README обновлён если нужно

Защита main (Branch Protection Rules):
- Require pull request before merging — только через PR, не напрямую
- Require approvals — минимум 1 approval перед merge
- Require status checks to pass — CI должен пройти
- Do not allow bypassing — правила для всех включая владельца
