---
description: Первый контакт Victor-website — объяснить пользователю, что заполнить перед запуском сайта.
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

# Victor-website — первый старт

Покажи пользователю понятную инструкцию из `docs/00-first-contact.md`.

Главное:

1. Для данных бизнеса заполнить:

```text
victor-website-memory/site.inv
```

2. Для доступов и секретов скопировать:

```text
victor-website-memory/victor-website.env.example
```

в:

```text
victor-website-memory/victor-website.env.local
```

3. Объяснить, что `victor-website.env.local` нельзя коммитить и нельзя публиковать.

4. Если доступов нет, оставить:

```text
VICTOR_WEBSITE_DEPLOY_MODE=local-only
VICTOR_WEBSITE_ALLOW_PUBLISH=no
VICTOR_WEBSITE_ALLOW_ACTIVATE_THEME=no
```

5. После заполнения можно запускать:

```text
/victor-website-phase1
```

Не перегружай пользователя техническими деталями. Сначала дай минимальный список: бизнес, контакты, услуги, регион, пример дизайна, что в референсе обязательно повторить визуально, конкуренты, доступы для деплоя только если публикация нужна сейчас.
