---
description: Victor-website Excalibur publish repair — публикация Phase 1 статьи Excalibur в WordPress.
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

# Victor-website — Excalibur WP Publish Repair

Это repair-команда. В нормальном прогоне публикация Excalibur articles выполняется в Phase 1 после готового deploy context.

**Prerequisites:** `✅ ARTICLE OK`, `article-qa.md` PASS, `link-verify.json` pass, `cover/cover.png`, `site.inv` + `allow_publish=yes`.

## Шаги

1. Проверь `victor-website-memory/blog/articles/<topic_id>-<slug>/` — полный комплект артефактов.
2. Link verify (если ещё нет):

```bash
python victor-website/scripts/excalibur_link_verify.py \
  victor-website-memory/blog/articles/<dir>/article.html \
  -o victor-website-memory/blog/articles/<dir>/link-verify.json \
  --site-base $PUBLIC_SITE_URL
```

3. Dry-run:

```bash
python victor-website/scripts/victor_website_excalibur_wp_publish.py --article-dir victor-website-memory/blog/articles/<dir> --dry-run
```

4. **Task(excalibur-wp-publish)** или Aurora — publish + live check.
5. Запиши `victor-website-memory/blog/wp-publish-log.md`, обнови fragment `Ready for WP publish: yes`.

Контракт: `victor-website/shared/excalibur-wp-publish-contract.md`  
Skill: `skills/excalibur-wp-publish/SKILL.md`

## Aurora follow-up

Если `single.php` не выводит `_teya_schema_jsonld` — добавить при следующем deploy темы.
