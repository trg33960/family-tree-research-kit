# Family Tree Research Kit — project guide for Claude

This file is read automatically when someone opens this repository with Claude Code (or Claude in an IDE). If you are Claude reading this: this repo is a **template** for building an interactive, well-sourced family tree as a single self-contained web page. Your job is to help the human turn the demo family in `index.html` into **their own** family — researched carefully and cited.

## The deliverable
`index.html` is one self-contained page: an interactive pan/zoom "whiteboard" of person cards, marriage bars, parent-child wires, clickable dossiers, a Stories panel, a Migrations/Timeline panel, and a 3D globe of birthplaces and migration arcs. No build step and no dependencies except the globe library, which loads from a CDN at runtime when the Globe panel opens. It currently contains a fictional demo family (the "Rivers" family) — replace it.

## How to walk a new user through this (default flow)
When the user asks to start (e.g. "help me build my family tree"):
1. **Interview them briefly.** Ask for the surname(s) to trace, what they already know (names, dates, places, a few generations), any documents or photos they have, and where the family migrated from and to. Don't ask for everything at once — start with the direct line they know best.
2. **Seed the tree.** Replace the demo people in `index.html` with the real ones they give you (see *Data model*). Keep it small at first — the direct line — then branch out.
3. **Research to extend and verify.** Follow the sourcing standards below. Every added fact traces to a source. Keep a running log in `research_notes.md`.
4. **Preview & iterate.** Have them open `index.html` (or run a local server) and adjust the layout coordinates so it reads well.
5. **Deploy** when they want it shareable — see `GETTING_STARTED.md`.

Keep the user in the loop: show them what you found and where it came from before treating it as fact.

## Research & sourcing standards (important)
- **Cite every claim.** No name, date, or relationship goes on a card as fact without a source in that person's `src` array. If you infer something, say so.
- **Confirmed vs. probable.** Mark uncertain links clearly (a `PROBABLE` tag, or explicit dossier wording). Never quietly upgrade a guess to a fact. Distinguish "the record says" from "this is likely."
- **Prefer primary records:** civil birth/marriage/death certificates, census enumerations, church/parish registers, gravestone inscriptions, passenger lists, military and pension records.
- **Useful free/low-cost sources** (verify each — don't trust a hint blindly): FamilySearch (free account; parish + census + ancestor pages), Find a Grave (cemeteries, memorials, family links), national census portals and archives, Chronicling America and other newspaper archives, local GenWeb / county transcription sites, and national record services (e.g. ScotlandsPeople) where some images are pay-per-view.
- **Corroborate.** One hint is a lead, not proof — look for a second independent record before confirming.
- **Record access notes** in `research_notes.md` (which sites need a login, URL patterns that worked, record IDs) so the next session is faster.

## Privacy — non-negotiable
- **Living people:** include only what the user personally knows or what that person is happy to share publicly. No birthdates, addresses, or contact details for living relatives. When in doubt, leave it off. Mark living people `living:1` and keep their dossier minimal.
- The deployed site is **public**. Treat everything on it as public. Don't publish sensitive details about anyone — living or recently deceased — without the user's explicit say-so.
- **Photos:** only use images the user has the right to share.

## Data model (`index.html`)
All data lives in the `<script>` near the top of the file, as plain JS objects — no framework.

- `P` — the people, keyed by a short id:
  ```js
  id:{ x:120, y:-240, cls:'scot', direct:1, war:1, living:1,
       n:'Full Name', d:'1820-1889 - Place', mini:'one-line note',
       tags:['TAG','TAG'], dossier:{'Heading':'text', ...}, src:['citation', ...], img:'data:...' }
  ```
  - `x`,`y` — position on the 3000×1800 canvas (y can be negative; everything is shifted down by `YOFF`). Space generations ~300px apart vertically; keep couples adjacent (~200px apart).
  - `cls` — card color. Slots available: `scot`, `swede`, `dane`, `german`, `anglo`, `french` (CSS variables `--scot` etc.). Rename the legend text to match your own origins; the class names are just color slots.
  - `direct:1` — gold star (a direct ancestor). `war:1` — crossed-swords mark (military service). `living:1` — flags a living person (keep their dossier minimal).
  - `dossier` — the detail panel: heading → paragraph. This is where the sourced story goes. `src` — the citations shown at the bottom.
  - `img` (optional) — a portrait embedded as a `data:` URI so the page stays self-contained.
- `COUPLES` — `[['idA','idB'], ...]` draws a marriage bar between two people.
- `FAMS` — `[{p:['parentId','parentId'], k:['kidId', ...]}, ...]` draws parent→child lines. `p` may hold one or two parents.
- `LOCS` — places for the Migrations panel: `key:{t:'Title', note:'...', ppl:['id', ...]}`. The `key` matches a globe point id.
- `GLOCS` / `GARCS` — globe birthplaces (`{id,lat,lng,color,label}`) and migration arcs (`{startLat,startLng,endLat,endLng,color,label}`). The `HOME` zoom target inside `openGlobe()` is the convergence place — update its lat/lng.
- `INFO` — the three top-bar panels (`clan`, `stories`, `timeline`) as HTML strings: surname history/crest, family stories, and a migration timeline.
- Faint background `zone` labels (in the `#world` div) are region headings — reposition/rename to match your clusters.

To **add a person**: add an entry to `P`, then wire them up in `COUPLES` and/or `FAMS`. To **recolor**: change `cls`. To **move**: change `x`/`y`.

## Style / conventions
- Keep `index.html` self-contained (inline CSS/JS, images as `data:` URIs). The only external load is the globe library, fetched at runtime.
- Match the existing serif / parchment look unless the user wants a change.
- The page is already mobile-friendly (touch pan, pinch-zoom, responsive toolbar). Preserve that if you edit the engine.

## Files
- `index.html` — the site (edit the data blocks).
- `GETTING_STARTED.md` — how to fork, connect Claude, and deploy.
- `research_notes.template.md` — copy to `research_notes.md` and keep the running research log there (private by default; see `.gitignore`).
- `memory/` — optional seed "memory" notes mirroring the key guidelines; see `GETTING_STARTED.md`.
