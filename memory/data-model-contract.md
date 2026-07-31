---
name: data-model-contract
description: How index.html stores people (P), couples, families, locations, globe, panels
metadata:
  type: reference
---

All data is plain JS objects in `index.html` (no framework):

- `P[id] = {x,y,cls,direct?,war?,living?,n,d,mini?,tags[],dossier{},src[],img?}` — one person. `x,y` position on a 3000×1800 canvas; `cls` sets card color (`scot`/`swede`/`dane`/`german`/`anglo`/`french`); `direct` = star, `war` = swords, `living` = flag.
- `COUPLES = [[idA,idB], ...]` — marriage bars.
- `FAMS = [{p:[parentIds], k:[kidIds]}, ...]` — parent-child lines.
- `LOCS = {key:{t,note,ppl:[ids]}}` — migration-panel places; `key` matches a globe point id.
- `GLOCS` / `GARCS` — globe points and arcs; update the `HOME` zoom target in `openGlobe()`.
- `INFO = {clan,stories,timeline}` — top-bar panels as HTML strings.

Add a person = add to `P`, then wire in `COUPLES` / `FAMS`. See [[project-goal]].
