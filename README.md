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
- `hadith/{editionId}.min.json.zip` — full mirror of [hapiam/hadith-json](https://github.com/hapiam/hadith-json)'s `db/unified/files/` + `db/unified/by_book/` + `db/unified/catalog`, minified and zipped. **Not** the app's live hadith download path (that's `hapiam/hadith-json` directly, via jsDelivr with a `raw.githubusercontent.com` fallback — see that repo's own README) — this exists as a third, independent archival mirror in case `hapiam/hadith-json` itself becomes unavailable, same reasoning as every QUL export above (QUL itself has no stable URL, so those are re-hosted out of necessity; hadith-json does have one, so this is pure redundancy, not a workaround for a missing one).
