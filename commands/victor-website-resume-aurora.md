---
description: Victor-website recovery — продолжить сборку Aurora без перезапуска upstream и без фальшивого SUCCESS.
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

# Victor-website — resume Aurora

Используй, если после Excalibur/Aurora Team есть частичная тема в `victor-website-memory/wp/theme/<theme-slug>/`, но нет финального рабочего сайта или hard release gate не проходит.

## Главное правило

Recovery не имеет права писать `published_and_configured`, `success`, `✅ DESIGN OK`, `✅ QA OK` или “готово”, пока не прошёл:

```text
python victor-website/scripts/victor_website_release_gate.py --project-root <PROJECT_ROOT>
```

Если команда вернула ненулевой код:

1. Запиши полный вывод в `victor-website-memory/wp/release-gate-report.md`.
2. Поставь статус `❌ RELEASE BLOCKER`.
3. Исправляй только перечисленные gate-проблемы.
4. Не запускай Excalibur publish, Design Guardian или QA.

## Что нельзя перезапускать

Не перезапускай upstream-агентов, если их артефакты уже есть:

- `victor-website-researcher`
- `core` / `yadryshko`
- `aura-designer`
- `excalibur`
- Aurora Team agents

## Проверить перед recovery

Обязательные входы:

- `victor-website-memory/fragments/excalibur.md`
- `victor-website-memory/wp/page-content-pack.md`
- `victor-website-memory/wp/navigation-linking-map.md`
- `victor-website-memory/wp/schema-technical-seo-map.md`
- `victor-website-memory/wp/indexing-crawl-map.md`
- `victor-website-memory/wp/local-entity-map.md`
- `victor-website-memory/wp/performance-accessibility-map.md`
- `victor-website-memory/wp/conversion-tracking-map.md`
- `victor-website-memory/wp/security-release-map.md`
- `victor-website-memory/design/AURA_ASSET_REGISTRY.json`
- `victor-website-memory/wp/theme/<theme-slug>/`

## Запустить только Aurora recovery

```text
Режим AURORA RECOVERY. Не запускай upstream-агентов заново. Прочитай готовые артефакты research, semantic-core, design, blog/articles, все карты wp/*.md и частичную тему victor-website-memory/wp/theme/<theme-slug>/. Исправь только недостающие/сломанные части темы, deploy/media map/live evidence. Особое внимание: media-map schema assets[], локальные files из local_source_path, реальные WP uploads attachment_url, отсутствие Beget domain stub на HTTPS public URL, browser network без 4xx/5xx по CSS/JS/images/fonts, paint-evidence screenshots по главной и selected/build pages. После исправления обязательно запусти python victor-website/scripts/victor_website_release_gate.py --project-root <PROJECT_ROOT>. Если gate не прошёл — статус RELEASE BLOCKER и вывод в release-gate-report.md. Если deploy нельзя выполнить из-за credentials/allow_publish — статус ГОТОВО К ДЕПЛОЮ, запускай gate с --no-live и не выдумывай URL.
```

После успешного `victor_website_release_gate.py` можно запускать обычные gates: Design Guardian → QA.
