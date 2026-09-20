---
description: Victor-website Excalibur repair/rerun — ручной повтор статей/обложек, если Phase 1 Excalibur был deferred.
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

# Victor-website — Excalibur Repair/Rerun

Это не основной путь. В нормальном прогоне Excalibur пишет статьи и готовит covers в Phase 1 сразу после Core + AURA. Используй эту команду только для ручного ремонта, дописывания или повторной публикации.

**Prerequisites:** research + `11-blog-topics.md` + `AURA_BLOG_COVER_CONCEPT.json`.

## Пайплайн

1. Директор проверяет `11-blog-topics.md`, `AURA_BLOG_COVER_CONCEPT.md`, `.json`.
2. **Task(aura-designer)** — blog covers:
   - один **cover_family** из реестра `blog-cover-family-registry.json` (**33** типа)
   - `global_prompt_prefix` + `global_prompt_suffix` + `color_lock`
   - per-topic: только `topic_scene_descriptor` + alt
   - опционально: `blog-cover-style-anchor.png`
   - см. `victor-website/shared/blog-cover-brand-concept.md`
3. **Task(excalibur)** — статьи + MCP covers: **prefix + scene + suffix**, не freestyle.
4. Проверь: research-notes, article-qa, link-verify, schema, promotion-checklist, cover.
5. Publish repair — `commands/victor-website-phase2-excalibur-publish.md` + skill `excalibur-wp-publish`, если Phase 1 publish был deferred.

**Передай:** `topic_id` (`B01`…`B06`, `all`, `P0-only`), `publish: yes/no`.

## Как держится единый стиль

| Fixed (концепт) | Variable (тема) |
|-----------------|------------------|
| cover_family, палитра, layout, grain, свет | объект/метафора статьи |
| prefix/suffix промпта | `topic_scene_descriptor` |

6 обложек в grid должны читаться как **одна серия бренда**.
