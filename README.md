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


## Оригинальный README

# Victor-website Cursor Plugin

Victor-website is an autonomous Cursor plugin for end-to-end website production:
research, semantic core, AURA visual system, Aurora WordPress build team,
Excalibur blog articles, release gates, paint QA, and WordPress deploy support.

## Contents

- `agents/` — Cursor subagent prompts.
- `skills/` — role-specific skill contracts.
- `commands/` — user-facing workflow commands.
- `rules/` — workspace rules for orchestration.
- `scripts/` — validation, deploy, release-gate, WordPress and Excalibur utilities.
- `shared/` — data-flow contracts, templates, QA gates and examples.
- `vendor/` — bundled AURA/Yadryshko references.

## Install

Place this folder at:

```text
%USERPROFILE%\.cursor\plugins\local\victor-website
```

Then restart or reload Cursor.

## Runtime Data

Project outputs and secrets must live outside this plugin, usually in the
working project under:

```text
victor-website-memory/
```

Do not commit real credentials. Use `shared/victor-website.env.example` and
`shared/site.inv.example` as templates.

## Main Workflow

Start with:

```text
/victor-website-phase1
```

The current pipeline is split across focused agents:

```text
Research -> Core || AURA -> Aurora Team -> Aurora split build
-> Deploy/Media -> Report Compiler -> Excalibur -> Blog Integrator
-> Paint Evidence -> Release Gate -> Design Guardian -> QA
```

## Release Gate

For a built project, run:

```powershell
python victor-website/scripts/victor_website_release_gate.py --project-root <PROJECT_ROOT>
```

The gate must pass before any run can be considered production-ready.
