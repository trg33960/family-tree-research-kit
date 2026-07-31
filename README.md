# Family Tree Research Kit

A template for building an **interactive, well-sourced family tree** as a single self-contained web page — then researching it with Claude and publishing it for free.

- **One file, no build step.** `index.html` is a pan/zoom board of person cards with clickable dossiers, a Stories panel, a Migrations timeline, and a 3D globe of birthplaces and migration routes.
- **Runs out of the box.** Ships with a small fictional demo family (the "Rivers" family) so you can see how it works — then replace it with your own.
- **Claude-ready.** Includes `CLAUDE.md`, so Claude opened in this folder already knows the research methodology, sourcing standards, privacy rules, and how the file is structured.

## Quick start
See **[GETTING_STARTED.md](GETTING_STARTED.md)**. In short: use this template to make your own repo, open the folder in Claude, and say:

> *"Read CLAUDE.md, then interview me and start building my family tree."*

## Preview locally
```bash
python3 -m http.server 8000
```
Then open **http://localhost:8000/** .

## Privacy
The finished site is public. For living relatives, include only what they're comfortable sharing. See the privacy notes in `CLAUDE.md` and `GETTING_STARTED.md`.

## Credits
Generalized from a real family-history project into a reusable kit.
