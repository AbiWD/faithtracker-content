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

## Mawlid text source & license

Text under `mawlid/texts/` is **not** sourced from any commercial app
(e.g. Al Adkar) — those PDFs carry that app's own branding/App Store
links on every page and there's no basis to assume redistribution
rights. Instead, each text here traces to an independently and openly
licensed source:

- `manqoos-moulid.json`: text by **Sheikh Zainuddin Makhdoom** (public
  domain — composed centuries ago), sourced via the scan on
  [Wikimedia Commons](https://commons.wikimedia.org/wiki/File:Manqoos_maulid_original.pdf)
  and its transcription on Arabic Wikisource. That Wikisource
  transcription is *not yet community-proofread* (Wikisource itself
  flags most pages "needs correction"), so this file's text was
  reconstructed by cross-checking it against a second, independent
  digital edition of the same traditional text — used only as a
  reference to catch OCR mistakes (e.g. Wikisource's raw OCR misread
  "the seventh day" as a nonsense word in one passage; the second
  source made the correct reading obvious), never reproduced as a
  document itself. **This has not been reviewed by a scholar or the
  mosque community — verify before treating it as final.**

Add a `source_note` and `source_url` field (see `manqoos-moulid.json`)
to every mawlid text file documenting exactly where it came from and
its license — this folder does not accept text without a clear,
checkable source.

- `ajmeer-maulid.json`: ⚠️ Text by **Sheikh Shams al-'Ulama E.K. Abu Bakr
  Musliyar (1914–1996)** — a named, recently-deceased author, unlike
  Manqoos Moulid's centuries-old text. This is very likely still under
  active copyright (probably held by Samastha Kerala Jam'iyyathul
  Ulama, the institution he led for decades). Extracted from a PDF the
  user supplied, with that PDF's own app branding (logo/App Store
  links/QR code images) stripped out — but removing the branding does
  not clear the copyright on the underlying text itself. **Pushed to
  `main` at the user's explicit, repeated, informed direction** — no
  permission has been obtained from a rights-holder. See its own
  `source_note` field for the full explanation.

- `badar-maulid.json`: ⚠️ **DO NOT PUSH THIS FILE TO `main` without the
  user's explicit direction, same as Ajmeer.** No author or
  rights-holder identified at all for this specific text (unlike
  Ajmeer, where at least the author is known). Extracted the same way
  — user-supplied PDF, branding stripped, Quranic citations within the
  text replaced with verified Tanzil text rather than the source PDF's
  own badly-scrambled rendering of those verses (that PDF's calligraphic
  font makes Quran quotations extract as unreadable fragments; the
  prose/poetry does not have this problem). The companion-name list
  section additionally has NOT been cross-checked against a canonical
  published "Asma Ahl Badr" list — see its own `names` section's `note`
  field. Committed here only so it's ready to publish once you decide;
  publishing it is a real, separate copyright decision, not a
  formality.

## Dua text source & license

- `daily-duas.json`: 41 everyday situational duas (sleep, wudu, home,
  masjid, travel, meals, Istikhara, Qunoot, etc.). The topic list,
  English titles, and hadith/Quran references were carried over from a
  user-supplied PDF (author: Haque Ashanul) — but its Arabic did not
  extract as usable text (glyph-run scrambling), so it was not copied.
  The Arabic here was independently reconstructed from the standard
  hadith wording for each dua, matching the cited source (Sahih
  al-Bukhari, Sahih Muslim, Abu Dawud, at-Tirmidhi, Ibn Majah, or the
  cited Quran verse) — the same wording found identically across
  published hadith collections, since these are 1,400-year-old
  transmitted texts, not any one compiler's creative work. English
  translations are original, not copied from the source PDF. **Not yet
  reviewed by a scholar or the mosque community — verify before
  treating as final**, same caveat as the Mawlid texts above.

## Ratheeb text source & license

- `haddad-ratheeb.json`: **Ratheeb al-Haddad**, authored by Imam Abdullah
  bin Alawi al-Haddad (d. 1132 AH / 1720 CE) — a centuries-old, extremely
  widely published litany, recited daily after Maghrib in Shafi'i/
  Hadhrami communities worldwide. The section order, structure, and
  repeat counts were taken from a user-supplied PDF ("Haddad Ratheeb
  (Large)", published by the Al Adkar app) — but its Arabic did not
  extract as usable, correctly-ordered text (glyph-run scrambling), so it
  was not copied. The Quranic portions embedded in the ratib (Al-Fatihah;
  Ayat al-Kursi and the closing verses of Al-Baqarah, 2:284-286) are the
  verified Tanzil Uthmani text, same source as this repo's `quran/`
  content. The remaining tasbih/tahlil/salawat phrases and the closing
  du'a are the standard, fixed wording of this text found identically
  across published copies — not any one compiler's creative work. **Not
  yet reviewed by a scholar or the mosque community — verify before
  treating as final**, same caveat as the Mawlid/Dua texts above.

- `dua-tawbah.json`: a short istighfar/tawbah (repentance) dua. Topic
  order taken from a user-supplied PDF ("തൗബ" / Thauba, published by the
  Al Adkar app) — Arabic did not extract usably (same scrambling issue),
  so it was read directly off the PDF's own rendered page images instead
  of the text layer. That PDF also included a Malayalam devotional
  narration between each Arabic phrase — omitted here (Arabic only,
  matching this repo's other texts). The three Quranic verses quoted
  (7:23, 3:8, 2:201) are verified Tanzil Uthmani text; the istighfar
  phrases and closing du'a are standard, widely-published wording. **Not
  yet reviewed by a scholar or the mosque community.**

## Qasida text source & license

- `burda.json`: **Qasidat al-Burda** (The Poem of the Mantle) by Imam
  Sharaf al-Din al-Busiri (d. 694-696 AH / 1294-1297 CE) — a classical
  Arabic poem composed over 700 years ago, public domain, one of the
  most widely published and memorized poems in Islamic literary history
  with an essentially invariant text across standard editions. The
  chapter order and 160-verse structure (confirmed by the poem's own
  closing line) were taken from a user-supplied PDF ("Burda", published
  by the Al Adkar app) — but its Arabic did not extract as usable,
  correctly-ordered text (glyph-run scrambling), so it was read directly
  off the PDF's own rendered page images instead, cross-checked against
  the standard published text of this poem. **Not yet reviewed by a
  scholar or the mosque community — verify before treating as final**,
  same caveat as this repo's other reconstructed texts.

## Layout

```
quran/
  surahs/
    yaseen.json        # one file per surah, full verse text
  metadata/
    surahs.json         # index: which surahs exist and which file each is in
mawlid/
  texts/
    manqoos-moulid.json # one file per text: sections[] of prose/poem/heading blocks
  metadata/
    texts.json           # index: which texts exist and which file each is in
dua/
  texts/
    daily-duas.json     # one file per collection: duas[] of {title, reference, parts[]}
  metadata/
    texts.json           # index: which collections exist and which file each is in
ratheeb/
  texts/
    haddad-ratheeb.json # one file per text: sections[] of prose/poem/heading/dhikr blocks
                         # (dhikr = {text, repeat?, reference?} — a phrase said N times)
  metadata/
    texts.json           # index: which texts exist and which file each is in
qasida/
  texts/
    burda.json           # one file per text: sections[] of poem/heading blocks
                          # (one poem block per chapter, lines[] = one verse per entry)
  metadata/
    texts.json            # index: which texts exist and which file each is in
```

Each new content *type* gets its own top-level folder, same pattern as
`quran/`/`mawlid/` — e.g. a future `duas/` for supplications. Within a
type's folder: a `metadata/` index file (so the app never has to
hardcode filenames) plus the actual content files in their own
subfolder.

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
