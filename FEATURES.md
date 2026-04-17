# IUOE Local 564 — Grievance-Arbitration Advisor: Master Reference

## Features
- **PIN lock screen** — 4-digit keypad guards access per contract; master PIN bypasses all
- **DTMF keypad tones** — iOS Safari: base64 WAV beep via `new Audio().play()` in `ontouchstart`; desktop/Android: Web Audio API two-frequency sine waves per digit
- **GPT-4o grievance analyzer** — sends full verbatim CBA + member's description; returns 13-section arbitration strategy
- **Follow-up chat** — multi-turn conversation with full context (grievance + analysis + history)
- **Grievance form builder** — auto-fills articles, statement, remedy, deadline from AI output via regex
- **Email function** — `mailto:` link pre-filled with complete formal grievance (employee, steward, articles, statement, remedy, deadline)
- **Print analysis** — `window.print()` with print stylesheet (white background, hidden UI chrome)
- **Save as PDF/TXT** — Blob download of analysis + follow-up chat as `.txt` file
- **New Grievance reset** — clears all state, scrolls to top
- **Switch Contract** — returns to employer select without reload
- **PWA / home screen install** — `manifest.json` + `apple-mobile-web-app-capable` meta tags
- **Search engine blocked** — `noindex, nofollow, noarchive` on all robots

---

## PIN Codes
| Contract | PIN |
|---|---|
| Master (Business Manager — unlocks ANY contract) | `2120` |
| Amentum NASA-JSC | `2428` |

---

## Color Scheme
| Variable | Hex |
|---|---|
| `--navy` | `#0a1628` |
| `--navy-mid` | `#0e1e38` |
| `--navy-light` | `#162840` |
| `--gold` | `#c9a84c` |
| `--gold-light` | `#e8c96d` |
| `--gold-dim` | `rgba(201,168,76,0.2)` |
| `--white` | `#ffffff` |
| `--muted` | `rgba(255,255,255,0.78)` |
| `--dim` | `rgba(255,255,255,0.45)` |
| `--red` | `#ff6b6b` |

---

## File Structure
```
/
├── index.html          # Entire app — HTML, CSS, JS in one file
├── manifest.json       # PWA manifest (name, icons, theme color)
├── FEATURES.md         # This file
├── claude.md           # Claude Code instructions
├── contracts/
│   └── amentum.txt     # Full verbatim Amentum NASA-JSC CBA text
└── img/
    ├── employer-logo.png   # Employer select screen logo
    ├── hero-logo.jpg       # App screen header logo
    ├── pin-bulldog.png     # PIN screen bulldog + PWA icon
    └── footer-logo.jpg     # Footer logo
```

---

## How to Add a New Contract

**1. Add to the `CONTRACTS` object in `index.html`** (around line 354):
```js
'yourkey': {
  name: 'Employer Full Name',
  badge: 'Badge text shown after login',
  pin: '1234'
}
```

**2. Add the dropdown option** (around line 169):
```html
<option value="yourkey">Employer Display Name</option>
```

**3. Create the contract text file:**
```
contracts/yourkey.txt   ← full verbatim CBA text, plain text
```

That's it. The PIN system, AI analyzer, and form builder all work automatically.

---

## AI Model & API
- Model: `gpt-4o`, `max_tokens: 4000` (analysis), `1500` (follow-up)
- Endpoint: `https://api.openai.com/v1/chat/completions`
- API key stored as base64 in `index.html` — rotate in the `atob()` call if compromised
- System prompt persona: 35-year IUOE arbitration advocate; covers CBA, NLRB, Texas law, SCA/FAR, FMLA, Weingarten rights, TWC, OFCCP, OSHA Region 6
