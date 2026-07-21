# mirror

Raw source-data mirror for the [hapi app](https://github.com/tezcane/hapi_app_v2)'s Quran/Hadith reading feature.

Hosts data exports from [QUL (Quranic Universal Library)](https://qul.tarteel.ai) that have no stable public download URL — QUL's own site requires a logged-in session and a manual per-resource "Download" button click to export each file, so this repo re-publishes those exports at a durable, publicly fetchable URL for the pipeline in `tool/quran_hadith_pipeline/` to consume.

See `tool/quran_hadith_pipeline/DATASET_MANIFEST.json` in the main app repo for per-file provenance, license, and content notes.

## Contents

- `qpc-hafs-tajweed.json` — QUL QPC Hafs Uthmani text + inline tajweed rule markup (resource `quran-script/58`)
- `en-sahih-international-simple.json`, `en-asad-simple.json`, `quran-en-yusufali-simple.json` — QUL translations (resources `translation/193`, `translation/277`, `translation/124`)
- `syllables-transliteration.json` — QUL syllables transliteration (resource `transliteration/477`)
- `en-tafisr-ibn-kathir.json` — QUL Tafsir Ibn Kathir English (resource `tafsir/35`)
- `tafsir_zips/` — QUL tafsir catalog exports, one zip per edition
- `_tafsir_catalog.tsv` — index of the tafsir editions in `tafsir_zips/`
- `quran/translation/{slug}.zip`, `quran/transliteration/{slug}.zip` — every other QUL Quran translation/transliteration edition (186 + 3), re-hosted the same way as the four files above
- `quran/wordbyword/{key}.zip` — QUL word-by-word translation/transliteration, one zip per language
- `quran/reciter/timing/{key}.min.json.zip` — per-reciter word/letter highlight timing data

**Removed: `hadith/{editionId}.min.json.zip`** (a zipped repackaging of [hapiam/hadith-json](https://github.com/hapiam/hadith-json)'s `db/unified/files/`). It was never the app's live hadith download path — that's always been `hapiam/hadith-json` directly, via `raw.githubusercontent.com` (see that repo's own README) — and the one pipeline code path that did reference it (`tool/quran_hadith_pipeline/build_db.dart`'s `hadith_books`/`available_editions` sqlite fallback tables, themselves only used if the app's bundled JSON catalog asset is ever missing) has been repointed at `hapiam/hadith-json` directly. Kept as a duplicate copy of data that already has a stable, directly-fetchable home; removing it eliminates a second copy that had to be kept in sync by hand on every hadith-json release.
