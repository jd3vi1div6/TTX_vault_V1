# TTX App — Vault-Tec Tabletop Exercise Terminal

A self-contained web app for running, tracking, and analyzing cybersecurity tabletop exercises (TTX). Styled as a Pip-Boy / Vault-Tec terminal from the Fallout series.

**Live demo:** https://jd3vi1div6.github.io/ttx-app/

---

## Modules

| Module | File | Purpose |
|--------|------|---------|
| Home | `index.html` | Landing page with module navigation |
| Dashboard | `dashboard.html` | Exercise progress, observation stats, risk register, MITRE ATT&CK coverage |
| TTX Tracker | `tracker.html` | Phase-by-phase guided exercise — data breach + ransomware scenarios |
| CREM Demo | `crem-demo.html` | Interactive Cyber Risk Exposure Management console (mock) |

## Features

- Two pre-built scenarios: **Data breach** (6 phases) and **Ransomware** (7 phases)
- **Participant** and **Facilitator** modes — facilitator mode reveals tips and MITRE technique tags
- Live risk assessment capture per phase: business impact, likelihood, data sensitivity, regulatory exposure
- Observation logging: gaps, actions, strengths, free-form notes (with owner attribution)
- Plain-text exercise report export
- Interactive CREM dashboard with CRI gauge, top exposures, attack-path graph, and filterable views
- 100% client-side — no server, no build step, works offline once loaded
- Pip-Boy + Vault-Tec aesthetic (CRT scanlines, terminal beep cursor, retro-futurist branding)

## Quick start (local)

```bash
git clone https://github.com/jd3vi1div6/ttx-app.git
cd ttx-app
# any static server will do:
python3 -m http.server 8080
# open http://localhost:8080
```

Or just open `index.html` in your browser — file:// URLs work fine.

## Deploy to GitHub Pages

1. Push the repo to GitHub: `https://github.com/jd3vi1div6/ttx-app`
2. Settings → Pages → Source: **Deploy from a branch**
3. Branch: **main**, folder: **/ (root)**
4. Save. Site goes live at `https://jd3vi1div6.github.io/ttx-app/` within ~1 minute.

See `DEPLOY.md` for a step-by-step git/gh CLI script.

## Repository structure

```
ttx-app/
├── index.html          # Landing page
├── dashboard.html      # TTX dashboard (KPIs, charts, risk heatmap, MITRE)
├── tracker.html        # Exercise tracker (guided phases)
├── crem-demo.html      # Interactive CREM mock dashboard
├── assets/
│   └── pipboy.css      # Shared Pip-Boy / Vault-Tec styling
├── README.md           # This file
├── DEPLOY.md           # Step-by-step GitHub Pages deploy
└── .gitignore
```

## Tech stack

- Vanilla HTML, CSS, JavaScript — no frameworks, no build
- Inline SVG for charts (no chart libraries)
- Google Fonts: VT323, Share Tech Mono
- Single shared stylesheet: `assets/pipboy.css`

## Customizing scenarios

Scenarios live in the `SCENARIOS` constant inside `tracker.html`. Each phase has:

```js
{
  title: 'PHASE N — short title',
  severity: 'green' | 'amber' | 'red',
  mitre: 'T1234 · Technique name',
  inject: 'What participants see…',
  tips: 'Facilitator-only guidance…',
  questions: ['Q1', 'Q2', '…']
}
```

Add a new scenario by adding a new key to `SCENARIOS` and a matching `<option>` and scenario card in the HTML.

## Privacy

No data leaves the browser. All observations, notes, and risk assessments live in JavaScript memory only — refreshing the page clears state. The plain-text export is generated client-side.

## License

MIT — use, modify, redeploy. Fallout / Vault-Tec / Pip-Boy are trademarks of Bethesda Softworks; this is a fan-styled project, not an official product.

---

> *"War. War never changes — but how you respond to it can."*
