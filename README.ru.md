# beads-copilot-plugin

[English](README.md) | **Русский**

Плагин GitHub Copilot CLI для [beads](https://github.com/gastownhall/beads) — распределённого графового трекера задач для AI-агентов на базе Dolt.

Полнофункциональная адаптация [оригинального плагина Claude Code](https://github.com/gastownhall/beads/tree/main/claude-plugin) для GitHub Copilot CLI с сохранением того же качества интеграции.

## Возможности

- **25 slash-команд** — `/beads:ready`, `/beads:create`, `/beads:show`, `/beads:close` и другие
- **Автономный агент** — находит и выполняет готовые к работе задачи
- **Глубокая интеграция skills** — персистентная память, трекинг зависимостей, выживание при компактификации
- **MCP-сервер** — полная интеграция beads-mcp для работы на естественном языке
- **Хуки сессии** — автоматическая загрузка контекста при старте сессии и перед компактификацией
- **15 справочных руководств** — воркфлоу, паттерны, устранение неполадок, продвинутые функции

## Требования

- [GitHub Copilot CLI](https://docs.github.com/en/copilot/github-copilot-in-the-cli) установлен
- [beads CLI](https://github.com/gastownhall/beads) (`bd`) установлен и доступен в PATH (v0.60.0+)
- [uv](https://github.com/astral-sh/uv) менеджер пакетов (для MCP-сервера)

## Установка

### Из GitHub

```bash
copilot plugin install akm77/beads-copilot-plugin
```

### Из локального клона

```bash
git clone https://github.com/akm77/beads-copilot-plugin.git
copilot plugin install ./beads-copilot-plugin
```

### Из маркетплейса

```bash
copilot plugin marketplace add akm77/copilot-marketplace
copilot plugin install beads@akm77-marketplace
```

> **Примечание:** Экосистема плагинов Copilot CLI активно развивается. Если что-то не работает, попробуйте установку из локального клона или проверьте `copilot plugin --help`.

### Проверка установки

```bash
copilot plugin list
```

В интерактивной сессии:
```
/plugin list
/beads:version
```

## Быстрый старт

1. **Инициализируйте beads** в проекте:
   ```bash
   bd init
   ```

2. **Запустите сессию Copilot CLI** и используйте команды beads:
   ```
   /beads:ready          # Найти незаблокированные задачи
   /beads:create         # Создать новую задачу
   /beads:workflow       # Показать руководство по воркфлоу
   ```

3. **Или используйте естественный язык** (через MCP):
   ```
   "Какие задачи готовы к работе?"
   "Создай баг для проблемы с таймаутом логина"
   "Покажи дерево зависимостей для bd-42"
   ```

## Доступные команды

| Команда | Описание |
|---------|----------|
| `/beads:ready` | Найти задачи, готовые к работе |
| `/beads:create` | Создать новую задачу |
| `/beads:show` | Показать детали задачи |
| `/beads:update` | Обновить поля задачи |
| `/beads:close` | Закрыть выполненную задачу |
| `/beads:list` | Список задач с фильтрами |
| `/beads:search` | Поиск задач по тексту |
| `/beads:dep` | Управление зависимостями |
| `/beads:blocked` | Показать заблокированные задачи |
| `/beads:comments` | Просмотр/добавление комментариев |
| `/beads:stats` | Статистика проекта |
| `/beads:workflow` | Руководство по воркфлоу |
| `/beads:epic` | Управление эпиками |
| `/beads:label` | Управление метками |
| `/beads:decision` | Запись решений |
| `/beads:template` | Шаблоны задач |
| `/beads:audit` | Аудит-логирование |
| `/beads:init` | Инициализация beads |
| `/beads:prime` | Загрузка AI-контекста |
| `/beads:version` | Информация о версии |
| `/beads:export` | Экспорт в JSONL |
| `/beads:compact` | Компактификация старых задач |
| `/beads:reopen` | Переоткрытие закрытых задач |
| `/beads:restore` | Восстановление компактифицированных задач |
| `/beads:rename-prefix` | Переименование префикса задач |
| `/beads:delete` | Удаление задач |

## Архитектура

```
beads-copilot-plugin/
├── plugin.json              # Манифест плагина
├── hooks.json               # Хуки сессии и компактификации
├── mcp.json                 # Конфигурация MCP-сервера
├── agents/
│   └── task-agent.agent.md  # Автономный агент выполнения задач
├── commands/                # 25 slash-команд
│   ├── ready.md
│   ├── create.md
│   ├── show.md
│   └── ...
└── skills/
    └── beads/
        ├── SKILL.md         # Основное определение skill
        ├── CLAUDE.md        # Руководство по сопровождению
        ├── README.md        # Документация для людей
        ├── adr/             # Записи архитектурных решений
        └── resources/       # 15 подробных руководств
```

## Связь с оригиналом

Этот плагин основан на отличной работе [Steve Yegge](https://github.com/steveyegge) и проекта [beads](https://github.com/gastownhall/beads). Оригинальный репозиторий предоставляет [руководство по интеграции с Copilot](https://github.com/gastownhall/beads/blob/main/docs/COPILOT_INTEGRATION.md) на основе MCP-сервера и файлов инструкций — это надёжный фундамент, который хорошо работает.

Этот плагин идёт дальше, упаковывая полный набор функций [плагина Claude Code](https://github.com/gastownhall/beads/tree/main/claude-plugin) в формат плагинов Copilot CLI, что позволяет установить его одной командой. Мы надеемся, что это соответствует замыслу автора и делает beads более доступным для пользователей Copilot CLI.

| Функция | Этот плагин | Оригинальная интеграция Copilot |
|---------|-------------|--------------------------------|
| Slash-команды | 25 команд | Через MCP-инструменты |
| Агент | Автономный агент задач | — |
| Skill с ресурсами | Полный skill + 15 руководств | Файл инструкций |
| Хуки | SessionStart + PreCompact | — |
| MCP-сервер | Встроен | Ручная настройка |
| Установка | `copilot plugin install` | Ручная конфигурация |

## Протестировано

Интеграционное тестирование с Copilot CLI v1.0.21-1.0.22 на реальном проекте — создание мини-CRM приложения (Python + SQLAlchemy + SQLite). Плагин успешно обработал создание эпика, 13 задач с зависимостями, жизненный цикл claim/close и хуки `bd prime` в рамках полного рабочего процесса.

Демо-проект: [copilot-mini-crm](https://github.com/akm77/copilot-mini-crm)

## Известные ограничения (Copilot CLI)

- **Утомление разрешениями (permission fatigue)**: Каждый отдельный MCP-инструмент beads (`context`, `create`, `stats`, `list`, `claim`, `close` и т.д.) требует отдельного подтверждения пользователем, даже после выбора "approve all tools from server beads". Это поведение Copilot CLI, а не проблема плагина beads.
- **Параллельная запись**: Встроенный Dolt поддерживает только одного писателя одновременно. Если Copilot отправляет несколько `create` параллельно, часть вызовов завершится ошибкой блокировки. Copilot обычно восстанавливается, переключаясь на последовательные вызовы.
- **Права доступа в worktree**: При использовании git worktree beads может предупреждать о правах директории `.beads`. Исправляется командой `chmod 700 <worktree>/.beads`.

## Лицензия

MIT — как и [beads](https://github.com/gastownhall/beads).

## Благодарности

- [Steve Yegge](https://github.com/steveyegge) — создатель beads
- Оригинальный [плагин Claude Code](https://github.com/gastownhall/beads/tree/main/claude-plugin)
