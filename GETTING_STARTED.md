# Getting Started — build your own family tree with Claude

This repo is a template. In about an hour with Claude you can turn it into an interactive, sourced tree of your own family and put it online. Here's the whole path.

## What you need
- A **GitHub account** (free).
- **Claude with access to your files.** Easiest is **Claude Code** (the CLI / desktop app) opened in this project folder, so Claude can read and edit `index.html` directly. Claude in an IDE extension works too.
- *(Optional, to publish)* a free **Vercel** account.

## 1. Get your own copy of this repo
On this template's GitHub page, click **"Use this template" → "Create a new repository"** (or **Fork**). Name it whatever you like — e.g. `smith-family-tree`. Make it **public** if you want to share the finished site. Then clone it:
```bash
git clone https://github.com/<your-username>/<your-repo>.git
cd <your-repo>
```

## 2. Point Claude at the folder
Open this folder in **Claude Code** (run `claude` inside it, or open it in the desktop app / IDE extension). Claude automatically reads `CLAUDE.md`, which teaches it the whole methodology and how `index.html` is structured — so it already knows how to help.

## 3. Kick it off — paste one of these prompts
> **"Read CLAUDE.md, then interview me and start building my family tree. Begin with my direct line — me, my parents, my grandparents. Here's what I know: …"**

Other good starters:
- "Replace the demo Rivers family in `index.html` with mine. Here's a photo of a family group sheet / a census page — pull what you can and cite it."
- "Research my great-grandfather [name], born about [year] in [place], and add what you can confirm — with sources."
- "I have a document (attached). Turn it into a sourced dossier for the right person."

Claude edits `index.html` for you, adds people, wires up relationships, and keeps a research log in `research_notes.md`. Everything it puts on a card should come with a source — ask **"what's the source?"** any time you're unsure.

## 4. See it
Open `index.html` in your browser (double-click it), or run a tiny local server for a smoother experience:
```bash
python3 -m http.server 8000
```
then visit **http://localhost:8000/** . Drag to pan, pinch or +/− to zoom, click a card for the dossier, and try the **Globe**.

## 5. Publish it (optional)
Ask Claude: **"Deploy this to my GitHub and host it on Vercel."** Or do it yourself — push to GitHub, then import the repo at **vercel.com**; it serves `index.html` at the root with no configuration and gives you a public `https://<name>.vercel.app` link to share.

## A note on privacy
This becomes a public web page. For **living relatives**, include only what you know they're comfortable sharing — no birthdates, addresses, or private details. Claude is instructed to follow this (see `CLAUDE.md`), but you are the final check.

## What's in here
- `index.html` — your site. Starts as a demo "Rivers" family; replace it.
- `CLAUDE.md` — instructions Claude reads automatically (methodology, sourcing, privacy, data model).
- `research_notes.template.md` — copy to `research_notes.md` and let Claude keep your research log there.
- `memory/` — *optional.* Seed notes you can copy into Claude's long-term memory for persistence across sessions. Not required — `CLAUDE.md` already covers the essentials.

Happy hunting.
