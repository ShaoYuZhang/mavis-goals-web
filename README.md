# goals-web

Public, secret-gated web UI for **Mavis's Goals** — Shao's tracked-goals dashboard.

- **UI:** Google-Tasks-style list (checkboxes, inline title editing, expandable details, add-a-goal, search). Single static file, no build step.
- **Data:** reads/writes the "Mavis's Goals" Google Sheet (anyone-with-the-link) via the Sheets API v4. A background hook on Mavis's computer syncs sheet edits into the tracking store (~30s) and pushes status updates back.
- **Access:** no sign-in. The page asks for a shared secret; only its SHA-256 hash is in the code. The Sheets API key is HTTP-referrer-locked to the Pages domain.
- **Deploy:** GitHub Actions → GitHub Pages on every push to `main` touching `goals-web/`.

## Setup needed once

1. Google Cloud console: enable the Sheets API, create an API key restricted to the Sheets API + HTTP referrer `https://shaoyuzhang.github.io/vibe-coding/*`, put it in `index.html` as `API_KEY`.
2. Share the passphrase with editors through a private channel (never commit it).
3. Repo Settings → Pages → Source: GitHub Actions (or via `gh api`).
