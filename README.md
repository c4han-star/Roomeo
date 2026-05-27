# Roomeo

Roommate type quiz (`quiz.html`) and marketing landing page (`index.html`).

## Run the site locally (recommended)

Opening `index.html` directly via `file://` can break relative paths or browser rules. From the project root, start a small static server:

```bash
cd Roomeo
python3 -m http.server 8000
```

Then open **http://127.0.0.1:8000/** in your browser. Use **Take the quiz** to open the quiz flow.

## Documentation

All project docs live in [`docs/`](docs/). Start with **[docs/README.md](docs/README.md)** for the index (quiz spec, scoring logic, landing copy, design reference).

With Node.js installed, you can use:

```bash
npx --yes serve -l 8000
```

## Repository access

This GitHub repository is **private**. Only people you invite can see or clone it. Invite collaborators under **Settings → Collaborators** (or **Manage access**) on GitHub.

## Asset layout

| Path | Contents |
|------|----------|
| `assets/brand/` | `logo.svg` |
| `assets/site/` | Landing imagery: banner, icons, backgrounds, etc. |
| `assets/quiz/questions/` | `quiz cover.png`, `q1.png`–`q12` (mixed `.png` / `.jpg` as needed) |
| `assets/characters/` | Type avatars, e.g. `beaver.png` … `turtle.png` |
| `assets/result-hero/` | Result hero character overlays, e.g. `turtle.png` (transparent PNG over `hero-room`) |
| `assets/roommate-type-cards/` | Large type cards for the landing page |
| `assets/quiz-result-1-0/` | Quiz result UI (waves, badges, room background, etc.) |
| `docs/` | Product and design Markdown — see [docs/README.md](docs/README.md) |
