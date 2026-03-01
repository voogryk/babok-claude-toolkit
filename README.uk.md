# BA Brain -- Business Analysis Toolkit for Claude Code

BA-асистент на базі **BABOK v3** та практик **Karl Wiegers** з requirements engineering.

Працює як окремий проект для Claude Code. Відкриваєш папку `ba-brain/` в Claude Code -- і маєш повноцінного BA-помічника зі скілами, темплейтами та конвертером документів.

## Швидкий старт

```bash
# Відкрити в Claude Code
cd ~/endgame/ba-brain
claude

# Створити новий проект
/scope my-project

# Імпортувати документи
/import /path/to/requirements.pdf my-project

# Витягти вимоги з документу
/elicit my-project document-analysis

# Написати user story
/user-story my-project "Користувач хоче змінити пароль"
```

## Що всередині

### Структура

```
ba-brain/
├── CLAUDE.md                          # Системний промпт (роль, правила, поведінка)
├── convert.py                         # Конвертер документів -> Markdown
├── .claude/
│   ├── rules/
│   │   └── babok.md                   # BABOK v3 + Wiegers довідник (авто-завантаження)
│   └── skills/                        # 8 скілів (slash-команди)
│       ├── scope/SKILL.md
│       ├── import/SKILL.md
│       ├── elicit/SKILL.md
│       ├── analyze/SKILL.md
│       ├── specify/SKILL.md
│       ├── user-story/SKILL.md
│       ├── validate/SKILL.md
│       └── glossary/SKILL.md
├── templates/                         # 5 темплейтів
│   ├── srs.md
│   ├── user-story.md
│   ├── use-case.md
│   ├── stakeholder-register.md
│   └── requirements-checklist.md
└── projects/                          # Робочі проекти
    └── _example/                      # Приклад структури
```

### Проектна структура

Кожен проект живе в `projects/{project-name}/`:

```
projects/my-project/
├── requirements.md      # Всі вимоги з ID, пріоритетами, статусами
├── glossary.md           # Глосарій доменних термінів
├── stakeholders.md       # Реєстр стейкхолдерів
├── decisions.md          # Лог важливих рішень
├── sources/              # Імпортовані документи (Markdown)
├── use-cases/            # Детальні use case файли
└── archive/              # Завершені/застарілі елементи
```

---

## Скіли (slash-команди)

Скіли побудовані відповідно до BABOK workflow -- від визначення скоупу до валідації.

### `/scope` -- Визначення скоупу

Стартова точка для нового проекту. Послідовно запитує:

1. **Проблема** -- що зламано або чого не вистачає
2. **Бізнес-цілі** -- як вимірюємо успіх
3. **Стейкхолдери** -- хто приймає рішення, хто користувачі
4. **Межі скоупу** -- що IN scope, що OUT of scope
5. **Обмеження** -- технічні, бюджетні, часові
6. **Припущення** -- що вважаємо істинним
7. **Ризики** -- що може піти не так

Результат: заповнені `stakeholders.md`, `requirements.md` (бізнес-вимоги), `glossary.md`.

### `/import` -- Імпорт документів

Конвертує PDF, DOCX, DOC, XLSX, XLS файли в Markdown та зберігає в `sources/`.

```bash
# Один файл
/import /path/to/spec.pdf my-project

# Декілька файлів (glob)
/import "/path/to/docs/*.pdf" my-project
```

Що відбувається:
1. Перевіряє що файл існує
2. Конвертує через `convert.py`
3. Зберігає в `projects/{project}/sources/{filename}.md` з метаданими
4. Показує summary (кількість заголовків, таблиць)
5. Пропонує запустити `/elicit` для аналізу

**Авто-детекція**: якщо надати Claude шлях до файлу з розширенням `.pdf`, `.docx`, `.doc`, `.xlsx` або `.xls` -- він автоматично запропонує `/import`.

### `/elicit` -- Збір вимог

Структурована сесія збору вимог. Підтримує 4 техніки:

| Техніка | Коли використовувати |
|---------|---------------------|
| **Interview** | 1-на-1 розмова зі стейкхолдером/SME |
| **Brainstorm** | Генерація ідей, дослідження простору рішень |
| **Document analysis** | Аналіз існуючих документів (після `/import`) |
| **Meeting notes** | Структуризація нотаток з мітингу |

Для кожної виявленої вимоги:
- Присвоює ID (`REQ-F-001`, `REQ-NF-003` тощо)
- Формулює в стилі "The system shall..."
- Перевіряє на неоднозначність (challenge ambiguity)
- Визначає джерело та пріоритет
- Вказує на gap'и -- що не обговорили, але варто

### `/analyze` -- Аналіз вимог

Структурує та моделює вимоги після збору:

1. **Декомпозиція** -- розбиває складні вимоги на атомарні
2. **Категоризація** -- Business / User / Functional / Non-Functional / Constraint / Interface
3. **Маппінг залежностей** -- що блокує що, що можна робити паралельно
4. **Пріоритизація** -- MoSCoW (Must / Should / Could / Won't)
5. **Gap analysis** -- перевірка на прогалини:
   - Обробка помилок
   - Автентифікація/авторизація
   - Валідація даних
   - Продуктивність
   - Безпека
   - Міграція даних
   - Звітність

### `/specify` -- Формальна специфікація

Пише формальні специфікації у стилі Wiegers SRS:

- **Функціональні вимоги** -- "The system shall..." з error conditions
- **Нефункціональні вимоги** -- з вимірюваними критеріями (мс, %, кількість)
- **Use cases** -- Actor/System таблиця з main flow, alternative flows, exception flows
- **Крос-референс** -- трасування від бізнес до функціональних вимог

Використовує темплейт `templates/srs.md` як основу.

### `/user-story` -- User Stories

Швидке створення user stories з acceptance criteria:

```
As a [specific role],
I want [capability],
So that [business value].

Acceptance Criteria:
1. Given [context], when [action], then [result]
```

Перевіряє кожну story за **INVEST** критеріями:
- **I**ndependent -- можна розробляти окремо
- **N**egotiable -- деталі можна обговорити
- **V**aluable -- приносить цінність
- **E**stimable -- команда може оцінити
- **S**mall -- вміщується в один спринт
- **T**estable -- є чіткі acceptance criteria

Також проактивно додає edge cases (невалідний ввід, скасування, навантаження, права доступу).

### `/validate` -- Валідація вимог

Quality gate перед передачею в розробку. Перевіряє за чеклістом Wiegers:

**Для кожної вимоги:**
- Completeness -- нічого не пропущено?
- Correctness -- фактично вірно?
- Feasibility -- технічно можливо?
- Necessity -- є бізнес-потреба?
- Unambiguity -- тільки одна інтерпретація?
- Verifiability -- можна написати тест?
- Consistency -- немає суперечностей?

**Для набору вимог:**
- Повне покриття бізнес-вимог
- Немає дублікатів
- Немає конфліктів
- Все має ID та пріоритет

**Шукає анти-патерни:**
- Gold plating -- вимоги без бізнес-потреби
- Рішення замість вимоги -- "Use PostgreSQL" замість "ACID compliance"
- Складені вимоги -- декілька поведінок в одній вимозі
- Нетестовані якості -- "System shall be reliable"

Генерує **Validation Report** з Critical/Warning/Suggestion issues.

### `/glossary` -- Глосарій

Управління доменним глосарієм:
- Додає/оновлює терміни з визначенням та контекстом
- Визначає синоніми (обирає канонічний термін)
- Виявляє омоніми (одне слово -- різні значення)
- Перевіряє `requirements.md` на неконсистентне використання термінів

---

## Темплейти

В папці `templates/` лежать 5 готових темплейтів:

| Файл | Опис | На базі |
|------|------|---------|
| `srs.md` | Software Requirements Specification -- повна структура з 9 розділами + трасування | Wiegers SRS |
| `user-story.md` | User story з acceptance criteria, INVEST чеклістом, edge cases | Agile + INVEST |
| `use-case.md` | Use case з main/alternative/exception flows, postconditions | UML / Cockburn |
| `stakeholder-register.md` | Реєстр стейкхолдерів з RACI матрицею | BABOK |
| `requirements-checklist.md` | Чекліст якості вимог з анти-патернами та sign-off | Wiegers |

Темплейти використовуються скілами автоматично. Можна також відкрити їх вручну як довідник.

---

## Конвертер документів

`convert.py` -- скрипт для конвертації документів у Markdown.

### Підтримувані формати

| Формат | Бібліотека | Що зберігає |
|--------|-----------|-------------|
| PDF | `pymupdf4llm` | Заголовки, таблиці, списки, структура. Оптимізовано для LLM. |
| DOCX | `mammoth` | Форматування, списки, таблиці. Показує warnings. |
| DOC | `antiword` / `LibreOffice` | Через antiword (plain text) або LibreOffice -> DOCX -> mammoth. |
| XLSX / XLS | `openpyxl` | Кожен sheet як окрема Markdown таблиця. |

### Використання

```bash
# Через venv
cd ~/endgame/ba-brain
.venv/bin/python convert.py input.pdf                  # Вивід в stdout
.venv/bin/python convert.py input.pdf output.md        # Зберегти у файл
```

### Встановлення залежностей

```bash
cd ~/endgame/ba-brain
python3 -m venv .venv
.venv/bin/pip install pymupdf4llm mammoth openpyxl
```

Для старих `.doc` файлів також потрібен `antiword` або `libreoffice` (системний пакет).

---

## Правила (rules)

### `.claude/rules/babok.md`

Авто-завантажується при роботі з будь-яким проектом (`projects/**`). Містить:

- **6 knowledge areas** BABOK v3 з практичними рекомендаціями
- **Таблиця технік елісітації** -- коли яку використовувати
- **Ієрархія типів вимог** (Wiegers): Business -> User -> Functional / NF / Constraints
- **Чекліст якості** з прикладами поганих та гарних формулювань
- **Тригерні слова неоднозначності** -- "fast", "easy", "flexible" тощо
- **Конвенція ID** -- `REQ-{type}-{number}`
- **Темплейт вимоги** та **темплейт user story**
- **INVEST критерії**

---

## Мова

- **Розмовна мова**: Claude відповідає українською за замовчуванням
- **Документація та вимоги**: пишуться англійською (working language для специфікацій)
- **Заборонено**: писати будь-що російською

---

## Типовий workflow

```
/scope          Визначити проект, стейкхолдерів, бізнес-цілі
    |
/import         Імпортувати існуючі документи (PDF, DOCX, XLSX)
    |
/elicit         Зібрати вимоги (інтерв'ю, аналіз документів, мітинг)
    |
/analyze        Декомпозиція, категоризація, пріоритизація, gap analysis
    |
/specify        Формальна специфікація (SRS, use cases)
    |
/user-story     User stories з acceptance criteria
    |
/validate       Quality gate -- перевірка за чеклістом Wiegers
    |
/glossary       Ведення глосарію (на будь-якому етапі)
```

Скіли можна використовувати в будь-якому порядку та повторювати. Workflow ітеративний.

---

## Методологічна база

### BABOK v3 (Business Analysis Body of Knowledge)
Стандарт від IIBA (International Institute of Business Analysis). Визначає 6 knowledge areas, техніки та компетенції бізнес-аналітика.

### Karl Wiegers -- Software Requirements
Книги "Software Requirements" та "More About Software Requirements". Визначають:
- Ієрархію типів вимог
- Структуру SRS документа
- Чекліст якості вимог
- Процес requirements engineering
