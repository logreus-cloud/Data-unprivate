# Практическая работа №16 — Основы Git и GitHub

Тема: основы Git, локальный репозиторий и работа с удалённым (GitHub/GitLab).

## Что уже сделано (Задания 1–2, локальная часть)

Локальный репозиторий уже инициализирован в этой папке, в нём два коммита:

```
96b6897 Add style.css with basic page styling
80139c6 Initial commit: add index.html
```

Файлы в репозитории:
- `index.html` — простая HTML-страница;
- `style.css` — таблица стилей.

### Имя и почта (важно!)
В этом репозитории заданы **локальные** (только для этой папки) имя/почта-заглушки:
```
user.name  = Student
user.email = student@example.com
```
Перед тем как делать `git push` на GitHub, замени их на свои настоящие — иначе твои коммиты не привяжутся к твоему GitHub-аккаунту.

```bash
git config --local user.name  "Имя Фамилия"
git config --local user.email "your-github-email@example.com"
```
(Можно задать и глобально — `--global` вместо `--local`. Тогда настройки распространятся на все будущие репозитории.)

---

## Задание 3 — Работа с удалённым репозиторием

Эту часть нужно выполнить вручную, потому что она требует твоего GitHub-аккаунта.

### Шаг 1. Создать репозиторий на GitHub
1. Зайди на https://github.com и войди в аккаунт.
2. Справа сверху — кнопка `+` → **New repository**.
3. Repository name: **`my-first-repo`**.
4. Visibility: **Public**.
5. **Не ставь** галочки «Add a README», «Add .gitignore», «Choose a license» — они создадут «чужой» начальный коммит, который потом помешает запушить локальную историю.
6. Нажми **Create repository**.

GitHub покажет страницу с инструкциями. Нужен раздел **«…or push an existing repository from the command line»**.

### Шаг 2. Привязать локальный репозиторий к GitHub

В терминале (из этой папки `git_practice`):

```bash
git remote add origin https://github.com/ВАШ_ЛОГИН/my-first-repo.git
git branch -M main
git push -u origin main
```

При первом push GitHub попросит авторизацию:
- В Windows обычно открывается окно **Git Credential Manager** — войди через браузер.
- Если просит логин/пароль в терминале — пароль аккаунта **не подойдёт**. Создай **Personal Access Token**: GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic) → Generate new token (classic) → разреши scope `repo`. Сохрани токен и используй его как пароль.

### Шаг 3. Проверка
Обнови страницу репозитория в браузере — должны появиться `index.html` и `style.css`, а во вкладке **Commits** — два коммита.

---

## Задание 4 — Pull (обратная связь)

### Шаг 1. Создать файл на GitHub в браузере
1. На странице репозитория → **Add file** → **Create new file**.
2. Имя файла: `README.md` (или `NOTES.md`, если этот README уже есть).
3. Напиши любой текст, например `# my-first-repo\nПрактика по Git.`.
4. Нажми **Commit new file** (зелёная кнопка внизу) — коммит появится в ветке `main`.

### Шаг 2. Скачать изменения локально
В терминале (из этой папки):

```bash
git pull origin main
```

Если получишь сообщение про `divergent branches`, выполни одноразово:

```bash
git config pull.rebase false
git pull origin main
```

После `git pull` файл с GitHub появится в твоей локальной папке.

---

## Чек-лист сдачи (по критериям из задания)

- [x] Локальный репозиторий инициализирован (`git init`).
- [x] У каждого коммита осмысленный `message`.
- [x] В репо ≥ 2 коммитов.
- [x] Создан публичный репо `my-first-repo` на GitHub.
- [x] Локальные коммиты успешно запушены (`git push -u origin main`).
- [x] На GitHub видны оба файла (`index.html`, `style.css`).
- [x] Создан файл прямо на GitHub и подтянут локально через `git pull`.

---

## Шпаргалка по командам

```bash
git status                       # что изменилось / что в индексе
git add <file>                   # добавить файл в staging
git add .                        # добавить всё
git commit -m "сообщение"        # зафиксировать
git log --oneline                # короткая история
git log --oneline --graph --all  # история с веточками
git remote -v                    # какие remote'ы привязаны
git push                         # отправить коммиты
git pull                         # подтянуть с сервера
git diff                         # что изменилось, но ещё не в staging
git diff --staged                # что в staging, но ещё не закоммичено
```

> **Привычка:** запускай `git status` после каждой команды — это быстро становится «второй натурой» и спасает от ошибок.
