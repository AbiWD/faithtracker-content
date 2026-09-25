# FaithTracker Content

Static content served to the FaithTracker mobile app via jsDelivr
(`https://cdn.jsdelivr.net/gh/AbiWD/faithtracker-content@main/<path>`).
No backend, no build step — add a file, commit, push, and it's live at
that URL within a few minutes (jsDelivr's cache TTL).

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

1. Add `quran/surahs/<name>.json` — same shape as `yaseen.json`
   (`chapter.number`, `chapter.name_english`, `chapter.name_arabic`,
   `chapter.revelation_type`, `chapter.total_verses`, `chapter.verses[]`
   with `verse_number` + `arabic`).
2. Add an entry to `quran/metadata/surahs.json` pointing at the new file.
3. Commit and push to `main`.

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
