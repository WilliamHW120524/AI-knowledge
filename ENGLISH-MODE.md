# English mode

This change adds an English / 中文 switch to the original AI Knowledge Atlas by [gethlx](https://github.com/gethlx/AI-knowledge).

## Open and use

Start the original website as described in its README. Select **English** in the header, or add `?lang=en` before the concept fragment:

```text
http://127.0.0.1:41839/?lang=en#3-13
```

Use `?lang=zh` to explicitly request Chinese. Otherwise the most recent choice is remembered in this browser. The default for a new browser remains Chinese. Selection, graph layout, and expanded reading are preserved when switching. Search accepts English and Chinese in either mode.

## Source changes

All application paths below are relative to `02_分析产物/图谱浏览器开发环境/`:

- `src/ui/i18n.js`: interface translations, language preference, English field selection, and word-aware graph labels.
- `src/ui/english-data.json`: a separate English overlay for all 197 concept cards, including all original fields. Chinese field keys and concept IDs remain stable. The original `preview-data.json`, original card sources, and graph relations are unchanged.
- `src/ui/atlas-preview.js`: connects the overlay to reading, search, filters, connected cards, the existing 3D scene, and accessibility labels.
- `index.html` and `src/styles/atlas.css`: language controls, translated static interface, and responsive English text layout.
- `tests/i18n.test.mjs`: translation coverage, source integrity, language precedence, blocked storage, label wrapping, and static UI text checks.

## Translation quality

The card text is a **machine-translated draft** of the Chinese source, produced once using Google Translate. It is bundled with the website: visitors do not call a translation API, send their searches to a translation service, or need an API key.

The interface was translated separately. Cards 3-13 (Probability / Uncertainty), 3-14 (Generalization), and 4-03 (Large Language Model) received targeted editorial corrections; this does not certify the entire collection. All 197 cards still need a full educational and terminology review. The interface identifies English content as a draft. Secondary concept names remain Chinese to help bilingual readers compare terms.

The `_meta.source_sha256` value identifies the Chinese source used. If Chinese content changes, update the matching English fields and that fingerprint; the coverage test deliberately detects a stale translation baseline. The English overlay is the maintained source of English wording, so corrections should be made there rather than in compiled files.

## Validation

From the application directory:

```sh
node --test tests/i18n.test.mjs
npm run build
```

The project retains its original npm manifest and lockfile; no new runtime dependencies or credentials are needed.

## Bringing this into the original website

Review the changed source and English text, then merge the changes into the original repository. Its existing GitHub Pages workflow builds and publishes changes on `main`. A separate preview copy does not update the teacher's original GitHub Pages URL.
