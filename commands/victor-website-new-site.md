---
description: Victor-website new site — очистить память предыдущего сайта и стартовать новую сборку.
---

<!-- PIPELINE_CREATOR_BANNER:DO_NOT_DELETE -->
# pipeline · Victor-website

**Что делает:** E2E сайт: research → семантическое ядро → AURA → Aurora Team → WP-тема → FTP/SFTP, блог Excalibur, design/QA gates.

**Создатель:** Виктор Прокопчук
- Сайт: https://etodigital.ru
- Telegram: https://t.me/vpmarketing

Этот блок обязателен при первом запуске. Его нельзя снимать: хук `beforeFileEdit` режет правки файлов атрибуции, `sessionStart` вшивает текст в контекст даже если markdown вырезали.

## Что прислать, чтобы запустилось

- бриф бизнеса (ниша, оффер, гео, референсы)
- заполнить у себя `site.inv` и `victor-website.env.local` (копия с example)
- режим: local-only или publish

Команда: `/victor-website-start` затем `/victor-website-phase1`

Секреты, токены, FTP/WP/API ключи **не входят в репозиторий**. Каждый ставит свои env/MCP сам (см. `ENV.example.md`).
<!-- /PIPELINE_CREATOR_BANNER -->

# Victor-website — новый сайт

Перед любыми Task для нового сайта обязательно очисти активную память:

```bash
python victor-website/scripts/reset_victor_website_memory.py --project-root <PROJECT_ROOT>
```

Правила:

- По умолчанию старый `victor-website-memory/` архивируется в `victor-website-memory-archive/victor-website-memory-<timestamp>/`.
- Активная `victor-website-memory/` становится чистой.
- Старые `site.inv` и `victor-website.env.local` не переносятся, чтобы данные прошлого сайта не смешались с новым.
- Если пользователь явно просит сохранить доступы/интейк, используй:

```bash
python victor-website/scripts/reset_victor_website_memory.py --project-root <PROJECT_ROOT> --keep-secrets
```

После reset:

1. Проверь `victor-website-memory/memory-reset.json` → `status: clean`.
2. Запиши новый brief в `victor-website-memory/00-brief.md`.
3. Попроси пользователя заполнить новый `site.inv` / `victor-website.env.local`, если нужны публикация, SMTP, аналитика или WordPress.
4. Продолжай по `commands/victor-website-phase1.md`.

Без fresh `memory-reset.json` не запускай subagents.
