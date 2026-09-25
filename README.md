# FaithTracker Content

Static content served to the FaithTracker mobile app via jsDelivr
(`https://cdn.jsdelivr.net/gh/AbiWD/faithtracker-content@main/<path>`).
No backend, no build step — add a file, commit, push, and it's live at
that URL within a few minutes (jsDelivr's cache TTL).

## Quran text source & license

Verse text under `quran/surahs/` is the Uthmani script from
[Tanzil.net](https://tanzil.net), licensed under
[Creative Commons Attribution 3.0](https://creativecommons.org/licenses/by/3.0/).
Tanzil's terms explicitly permit bundling into offline apps provided:

1. The source (Tanzil.net) is indicated somewhere in the app.
2. A link to tanzil.net is included so users can verify/track the text.
3. The text is kept unmodified (verse wording — formatting/JSON structure
   around it is fine).
4. This copyright notice is retained in copies/derived files.

Any surah added to this folder must come from Tanzil (or another source
with an equally clear, offline-bundling-compatible license) — not from an
untraceable or unlicensed transcription. See "Adding a new surah" below.

## Layout

```
quran/
  surahs/
    yaseen.json        # one file per surah, full verse text
  metadata/
    surahs.json         # index: which surahs exist and which file each is in
```

Each new content *type* gets its own top-level folder, same pattern as
`quran/` — e.g. a future `mawlid/` folder for the Maulid booklets, or
`duas/` for supplications. Within a type's folder: a `metadata/` index
file (so the app never has to hardcode filenames) plus the actual
content files in their own subfolder.

## Adding a new surah

1. Pull the Arabic text from Tanzil's Uthmani edition (e.g. via
   `https://api.alquran.cloud/v1/surah/<number>/quran-uthmani`, which
   serves Tanzil's text) rather than retyping or copying from an
   untraceable source — accuracy and license traceability both depend
   on this.
2. Add `quran/surahs/<name>.json` — same shape as `yaseen.json`
   (`chapter.number`, `chapter.name_english`, `chapter.name_arabic`,
   `chapter.revelation_type`, `chapter.total_verses`, `chapter.verses[]`
   with `verse_number` + `arabic`). Note: ayah 1 of every surah except
   Al-Fatiha and at-Tawbah comes back from that API with the Bismillah
   text prepended — strip it (keep only the actual ayah 1 wording) to
   match the convention `yaseen.json` already uses.
3. Add an entry to `quran/metadata/surahs.json` pointing at the new file.
4. Commit and push to `main`.

## Verifying before you push

Before committing a new surah file, sanity-check it locally:

```bash
python3 -c "
import json
with open('quran/surahs/<name>.json', encoding='utf-8') as f:
    data = json.load(f)
c = data['chapter']
print(c['name_arabic'], len(c['verses']), '/', c['total_verses'])
"
```

Confirms the file parses as valid UTF-8 JSON and the verse count
matches what's declared — catches encoding/truncation issues before
they ever reach the app.
