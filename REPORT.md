# Отчет по лабораторно-практической работе: Работа с коммитами в Git

**Тема:** Работа с коммитами в Git: создание, редактирование, просмотр истории и отмена коммитов.  
**Среда выполнения:** Visual Studio Code, Git для Windows (PowerShell), GitHub.  
**Репозиторий:** `my-commit-repo`

---

## 1. Цель работы
Научиться работать с коммитами в системе контроля версий Git:
- Инициализировать репозиторий;
- Создавать файлы и фиксировать изменения (коммиты);
- Просматривать историю коммитов и детальную информацию о них;
- Редактировать последний коммит с помощью параметра `--amend`;
- Отменять ошибочные коммиты с помощью `git reset`;
- Восстанавливать удаленные файлы из истории коммитов (`git checkout`);
- Работать с репозиторием в среде Visual Studio Code и опубликовать проект на GitHub.

---

## 2. Используемое программное обеспечение
- **Git** (версия 2.56.0.windows.2)
- **Visual Studio Code** (со встроенным терминалом и графическим интерфейсом Source Control)
- **GitHub** (удаленный хостинг репозиториев)

---

## 3. Ход выполнения работы

### Шаг 1. Подготовка репозитория

1. Инициализирован новый локальный Git-репозиторий в папке `my-commit-repo`:
   ```bash
   git init my-commit-repo
   cd my-commit-repo
   ```
   *Вывод Git:*
   ```text
   Initialized empty Git repository in C:/Users/user/.gemini/antigravity/scratch/my-commit-repo/.git/
   ```

2. Настроены имя пользователя и email:
   ```bash
   git config user.name "Student"
   git config user.email "student@example.com"
   ```

3. Создан файл `README.md`, добавлен в индекс (Staging Area) и зафиксирован первый коммит:
   ```bash
   echo "# My Commit Repo" > README.md
   git add README.md
   git commit -m "Initial commit with README"
   ```
   *Вывод Git:*
   ```text
   [master (root-commit) 192f243] Initial commit with README
    1 file changed, 1 insertion(+)
    create mode 100644 README.md
   ```

---

### Шаг 2. Создание коммитов

1. Создан файл `index.html` с базовой разметкой:
   ```html
   <!DOCTYPE html>
   <html>
   <head>
     <title>My Commit Project</title>
   </head>
   <body>
     <h1>Welcome to my project!</h1>
   </body>
   </html>
   ```

2. Файл добавлен в индекс и закоммичен:
   ```bash
   git add index.html
   git commit -m "Add basic index.html file"
   ```
   *Вывод Git:*
   ```text
   [master b692448] Add basic index.html file
    1 file changed, 9 insertions(+)
    create mode 100644 index.html
   ```

3. Проверен статус рабочего дерева:
   ```bash
   git status
   ```
   *Вывод Git:*
   ```text
   On branch master
   nothing to commit, working tree clean
   ```

4. Создан файл `style.css`:
   ```css
   body {
     font-family: Arial, sans-serif;
   }
   ```

5. Файл добавлен в индекс и закоммичен:
   ```bash
   git add style.css
   git commit -m "Add basic styles for the project"
   ```
   *Вывод Git:*
   ```text
   [master fe53e00] Add basic styles for the project
    1 file changed, 3 insertions(+)
    create mode 100644 style.css
   ```

---

### Шаг 3. Просмотр истории коммитов

1. Краткий просмотр истории коммитов в одну строку:
   ```bash
   git log --oneline
   ```
   *Вывод:*
   ```text
   fe53e00 Add basic styles for the project
   b692448 Add basic index.html file
   192f243 Initial commit with README
   ```

2. Подробный просмотр истории с авторами, датами и полными хешами:
   ```bash
   git log
   ```
   *Вывод:*
   ```text
   commit fe53e009e46ca4d1b4b58c2820a4e14c02ab40ab
   Author: Student <student@example.com>
   Date:   Thu Oct 22 06:14:15 2026 +0500

       Add basic styles for the project

   commit b692448f2b16a68a69232bf1d0e77bb6d841d9a4
   Author: Student <student@example.com>
   Date:   Thu Oct 22 06:14:14 2026 +0500

       Add basic index.html file

   commit 192f243e1f46014a7cfcde05848057eba90b7bd1
   Author: Student <student@example.com>
   Date:   Thu Oct 22 06:14:06 2026 +0500

       Initial commit with README
   ```

3. Просмотр изменений, внесенных конкретным коммитом (`git show <hash>`):
   ```bash
   git show fe53e00
   ```
   *Вывод:*
   ```diff
   commit fe53e009e46ca4d1b4b58c2820a4e14c02ab40ab
   Author: Student <student@example.com>
   Date:   Thu Oct 22 06:14:15 2026 +0500

       Add basic styles for the project

   diff --git a/style.css b/style.css
   new file mode 100644
   index 0000000..14a128f
   --- /dev/null
   +++ b/style.css
   @@ -0,0 +1,3 @@
   +body {
   +  font-family: Arial, sans-serif;
   +}
   ```

---

### Шаг 4. Редактирование и отмена коммитов

#### 4.1 Изменение последнего коммита (`git commit --amend`)
1. В файл `index.html` добавлена строка:
   ```html
   <p>Thank you for visiting!</p>
   ```

2. Изменения зафиксированы с обновлением последнего коммита:
   ```bash
   git add index.html
   git commit --amend -m "Updated index.html with thank you message"
   ```
   *Вывод:*
   ```text
   [master 52f778b] Updated index.html with thank you message
    Date: Thu Oct 22 06:14:15 2026 +0500
    2 files changed, 4 insertions(+)
    create mode 100644 style.css
   ```
   *Анализ:* Предыдущий коммит `fe53e00` был заменен новым `52f778b`, который теперь объединяет добавление стилей и обновление `index.html`.

3. Проверка истории:
   ```bash
   git log --oneline
   ```
   *Вывод:*
   ```text
   52f778b Updated index.html with thank you message
   b692448 Add basic index.html file
   192f243 Initial commit with README
   ```

#### 4.2 Откат ошибочного коммита (`git reset`)
1. Создан ошибочный файл и закоммичен:
   ```bash
   echo "This is an error file" > error.txt
   git add error.txt
   git commit -m "Mistakenly added error.txt"
   ```
   *Хеш нового коммита:* `01ffa59`.

2. Выполнен откат последнего коммита без потери файлов в рабочей директории:
   ```bash
   git reset HEAD~1
   # Примечание: HEAD~1 эквивалентно HEAD^, но корректно работает в PowerShell
   ```

3. Проверен статус репозитория:
   ```bash
   git status
   ```
   *Вывод:*
   ```text
   On branch master
   Untracked files:
     (use "git add <file>..." to include in what will be committed)
   	error.txt
   ```
   Коммит был отменен, а `error.txt` остался как неотслеживаемый (untracked) файл.

4. Удален файл `error.txt`:
   ```bash
   rm error.txt
   ```
   После удаления рабочая директория полностью соответствует коммиту `52f778b`, следов ошибочного файла не осталось.

---

### Шаг 5. Восстановление файлов

1. Создан файл `about.html` и закоммичен:
   ```bash
   echo "<h1>About Us</h1>" > about.html
   git add about.html
   git commit -m "Added about.html file"
   ```
   *Создан коммит:* `c8598b1 Added about.html file`.

2. Файл удален из файловой системы и зафиксировано удаление:
   ```bash
   git rm about.html
   git commit -m "Deleted about.html"
   ```
   *Создан коммит:* `d004e08 Deleted about.html`.

3. Восстановлен файл `about.html` из предыдущего коммита (`HEAD^` / `HEAD~1`):
   ```bash
   git checkout HEAD~1 -- about.html
   ```
   Файл `about.html` успешно извлечен из коммита `c8598b1` и автоматически помещен в индекс.

4. Зафиксировано восстановление файла:
   ```bash
   git add about.html
   git commit -m "Restored about.html file"
   ```
   *Создан коммит:* `2c72d2c Restored about.html file`.

5. Итоговое дерево коммитов:
   ```bash
   git log --graph --pretty=format:'%h -%d %s (%cr) <%an>'
   ```
   *Вывод:*
   ```text
   * 2c72d2c - (HEAD -> master) Restored about.html file (Student)
   * d004e08 - Deleted about.html (Student)
   * c8598b1 - Added about.html file (Student)
   * 52f778b - Updated index.html with thank you message (Student)
   * b692448 - Add basic index.html file (Student)
   * 192f243 - Initial commit with README (Student)
   ```

---

## 4. Работа с репозиторием в Visual Studio Code (VS Code)

В Visual Studio Code встроен мощный графический интерфейс для управления Git (вкладка **Source Control** / `Ctrl+Shift+G`):

1. **Открытие проекта**:
   - `code "C:\Users\user\.gemini\antigravity\scratch\my-commit-repo"`
   - Или через меню: `File` -> `Open Folder...`.

2. **Просмотр истории (Timeline)**:
   - В левой боковой панели VS Code в секции `TIMELINE` отображается история всех коммитов выбранного файла с возможностью сравнения изменений (diff) одним кликом.

3. **Стейджинг и коммиты**:
   - Нажатие на иконку `+` рядом с файлом выполняет `git add`.
   - Ввод текста в верхнее поле и нажатие `Commit` (или `Ctrl+Enter`) выполняет `git commit -m "..."`.
   - В меню `...` (More Actions) -> `Commit` доступна опция `Commit (Amend)` — аналог `git commit --amend`.

4. **Откат и восстановление**:
   - Стрелочка `Discard Changes` (отменить изменения) восстанавливает файл до состояния последнего коммита (`git checkout -- <file>`).

---

## 5. Публикация репозитория на GitHub

### Способ 1: Через интерфейс VS Code (Рекомендуемый и самый быстрый)
1. Откройте вкладку **Source Control** в VS Code (`Ctrl+Shift+G`).
2. Нажмите синюю кнопку **«Publish Branch»** (Опубликовать ветку) или **«Publish to GitHub»**.
3. Выберите тип репозитория:
   - **Publish to GitHub public repository** (Публичный)
   - **Publish to GitHub private repository** (Приватный)
4. Если вы не авторизованы, VS Code предложит нажать кнопку «Allow» и войти через браузер в аккаунт GitHub.
5. Готово! VS Code автоматически создаст репозиторий на GitHub и выполнит `git push`.

### Способ 2: Через командную строку (CLI)
1. Перейдите на сайт [github.com](https://github.com) и нажмите **«New repository»** (Новый репозиторий).
2. Задайте имя: `my-commit-repo`, выберите *Public* и не ставьте галочки «Add README», нажмите **Create repository**.
3. Скопируйте ссылку на репозиторий и выполните в терминале VS Code:
   ```bash
   # Переименовываем ветку master в main (стандарт GitHub)
   git branch -M main

   # Привязываем удаленный репозиторий
   git remote add origin https://github.com/<ВАШ_ЛОГИН_GITHUB>/my-commit-repo.git

   # Отправляем все коммиты на GitHub
   git push -u origin main
   ```

---

## 6. Описание возникших проблем и их решение

1. **Проблема со спецсимволом `^` в оболочке PowerShell (Windows)**:
   - *Описание:* При выполнении команды `git reset HEAD^` или `git checkout HEAD^ file` в PowerShell символ `^` интерпретируется как символ экранирования PowerShell, что приводит к ошибке или неполной передаче аргументов в Git.
   - *Решение:* Использовать синтаксис `HEAD~1` вместо `HEAD^`, либо оборачивать выражение в кавычки: `git reset "HEAD^"`, `git checkout "HEAD^" about.html`.

2. **Поведение `git commit` после `git reset HEAD^` и удаления файла**:
   - *Описание:* В методических указаниях после отката коммита с файлом `error.txt` предлагается выполнить `rm error.txt`, `git add .` и `git commit -m "Removed mistakenly added error.txt"`. Однако так как `git reset HEAD^` уже отменил коммит, удаление файла `error.txt` возвращает рабочую директорию в состояние, идентичное текущему `HEAD`. В результате `git commit` сообщает: `nothing to commit, working tree clean`.
   - *Решение:* `git reset HEAD^` уже полностью удалил ошибочный коммит из истории. Для явной фиксации сообщения об удалении можно использовать флаг `git commit --allow-empty -m "..."`, либо применить альтернативный подход с `git revert HEAD`.

3. **Предупреждения о переводах строк `LF will be replaced by CRLF`**:
   - *Описание:* В операционных системах Windows по умолчанию используется перенос строк CRLF (`\r\n`), а в Unix/Linux — LF (`\n`). При добавлении файлов Git выдает информационное предупреждение о нормализации переводов строк.
   - *Решение:* Настройка `git config --global core.autocrlf true`, которая автоматически преобразует LF в CRLF при извлечении и CRLF в LF при коммите.

4. **Отсутствие глобальной конфигурации пользователя**:
   - *Описание:* При первой установке Git команда `git commit` завершается с ошибкой `fatal: empty ident name ... not allowed`.
   - *Решение:* Обязательная настройка параметров `git config user.name "..."` и `git config user.email "..."`.

---

## 7. Вывод
В ходе лабораторной работы были освоены базовые и продвинутые механизмы работы с коммитами в Git:
- Создание поэтапных снимков состояния проекта (`git add`, `git commit`);
- Анализ истории проекта в консоли (`git log`, `git show`) и в интерфейсе VS Code;
- Исправление последнего коммита «на лету» без размножения промежуточных правок (`git commit --amend`);
- Откат нежелательных коммитов (`git reset`);
- Точечное восстановление удаленных файлов из любого исторического снимка (`git checkout <ref> -- <file>`);
- Процедура интеграции локального проекта с удаленным сервисом GitHub.
