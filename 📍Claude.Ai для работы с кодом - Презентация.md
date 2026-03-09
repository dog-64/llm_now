---
theme: white
css: _resources/llm_now/claude-code-slides.css
highlightTheme: github
slideNumber: true
tags:
  - llm
  - claude
---
### Claude.Ai для работы с кодом 

- Тех- обзор Claude Code для разработчиков: установка, модели, оплата и приёмы работы с агентами и контекстом.
- Олег Дулецкий 7.3.2026
- [github](https://github.com/dog-64/llm_now?tab=readme-ov-file)

<img src="_resources/llm_now/qr-llm-now.png" style="position:absolute; bottom:20px; left:20px; width:160px; height:160px;">
---
### Почему Claude Code

- лидер отрасли
- удобные тарифы (от $20) и лимиты (5 часовые)
- [развивается очень быстро](https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md)

---
### Модели

- Haiku (быстрая, недорогая, контекст 256К, как джун)
- Sonnet (баланс, средне, контекст 256К или 1M, мидл)
- Opus (максимум, дорогая, контекст 256К или 1М, синьор)

---
### Как получить доступ  

- VPN для Claude и ChatGPT  
- [ClaudeCode через squid прокси](https://github.com/dog-64/claudecode-proxy/settings)
- GLM  4.7
	- `export ANTHROPIC_BASE_URL="https://api.z.ai/api/anthropic" ` 
	- `export ANTHROPIC_DEFAULT_SONNET_MODEL="glm-4.7"`
- [openrouter.ai](https://openrouter.ai) - покупка токенов через API
- cloud.ru glx 4.6
---
### Оплата

- Claude.ai - &#36; 20 - &#36;100 - &#36;200 / месяц - кредитки
- Claude.Ai - через [plati.market](https://plati.market) около 1500 рублей в месяц, есть гарантия
- Avito - сопоставимо с [plati.market](https://plati.market)
- Wantopay - бот в Telegram, делает кредитки

---
### Режим работы

- по подписке - 5 часовой и недельные лимиты
- за токены - 3-5-20x дороже подписки
- основная LLM - Sonnet
- для ответственных или запутанных случаев - Opus
- когда кончаются лимиты - GLM 4.7
- иногда - Codex
---
### Другие клиенты

- Open Ai Codex - сопоставимый по моделям и возможностям
- Kilo Code - часто дает ранний доступ к моделям, не нужен VPN
- Alibaba Qwen-Cli - бесплатный доступ к Qwen Coder, не нужен VPN

---
## Работаем

```sh
> claude
> ...
❯ /model Opus
...
❯ /init
...
⏺ Теперь у меня есть полное понимание проекта. Создам улучшенный CLAUDE.md:
...
⏺ Файл CLAUDE.md обновлён
```

---
### Промпт

```sh
❯ pgcat_servers_is_banned - в pgcat была такая метрика 
- а тут, в PgDog, есть?
...
⏺ В pgdog нет метрики pgcat_servers_is_banned или аналога.
Banned статус доступен только:
  1. SHOW POOLS — административная команда (колонка banned)
  2. В коде pool.ban.banned() — внутреннее состояние, 
     не экспортируемое в метрики
Если нужно — метрику надо добавить.
```

---
--- 
### Sub[Агенты](https://code.claude.com/docs/ru/sub-agents) и [скилы](https://code.claude.com/docs/ru/skills)

Это инструменты концентрации экспертизы по определенной теме.
Агент - может работать в фоне. Skill нет. 
Например
- [агент для поиска решений в Интернете]([solution-research-agent.md](https://github.com/dog-64/solution-research-agent))
- [Rails Way Agent](https://github.com/dog-64/rails-way-agent)
- [Ruby Idioms Agent](https://github.com/dog-64/ruby-idioms-reviewer)
- [Rspec Testing Agent](https://github.com/dog-64/rspec-testing-agent)
- [Security Review Agent](https://github.com/dog-64/security-review-agent)
- [Tech Writer Agent - Ильясов "Пиши. Сокращай"](https://github.com/dog-64/tech-writing-agent)  

---
### Как использовать агента
```
❯ запусти агента general-purpose для анализа PgDog
⏺ Task(Analyze pgdog code quality)
⏺ Агент завершил анализ. Найдено 12 проблем:

Топ критичных проблем

1. inner.rs:336-352 — O(n) удаление waiter под мьютексом (производительность)
2. buffer.rs:56-74 — Silent failure при сортировке по неизвестной колонке (корректность)
3. binding.rs:71-75 — Бесконечные циклы sleep(Duration::MAX) (надёжность)

Хотите, чтобы я исправил какую-то из этих проблем?
```
---
### Как сделать skill

- идём в [Claude.Ai](https://claude.ai/chat/) с промптом:  `сделай skill для Claude Code из книги postgresql_internals-16.pdf
- кидаем pdf в диалог`
- через 5 минут скачиваем архив
- кладем в `~/.claude/skills`
- говорим Claude - `используй агента pg-internals-agent для анализа работы с Postgres`

---
## Полезные skills

- github - работа с репо Github
- gutlab - работа с репо Gitlab
- code-simplifier - анализ кода перед MR
- context7 - доки по куче библиотек 

Установка
```
/plugin install context7
```

---
### Контекст  

У него две проблемы - контекста слишком мало или слишком много

- CLAUDE.md  - наиболее общие правила
- `/init` - создание CLAUDE.md в каталоге 
- `/context` - показ чем занят сейчас контекст
- `/clear` - очистка контекста
- `/compact` - суммаризация чата 
- `/plan` - переход в режим планирования 
- `tasks` - список задачь
- [[ClaudeCode -ставим mcp context7|Context7]] 

---
### Приёмы  

- когда не получается - спрашивайте Claude "А как сделать..."
- в CLAUDE.md -`после изменений всегда запускай тесты`  
- голосовой ввод (app Handy)
- для вставки картинок-скриншотов используйте Ctrl-V
- в вызове - `bypassPermissions` без подтверждения команд  
- `/commit` сделать комит с описанием

---
### Итого

- Claude Code - берёт на себя рутину: коммиты, рефакторинг, написание тестов, анализ чужого кода
- Работает в контексте всего проекта, а не одного файла
- Агенты и скилы превращают накопленную экспертизу в переиспользуемые инструменты
- Порог входа низкий: `npm install -g @anthropic-ai/claude-code` + прокси + 20 минут