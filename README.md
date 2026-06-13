# impact.com · AI Adoption Arena — Tech Writing 🎮

A self-contained, gamified self-assessment that benchmarks the impact.com technical
writing team's AI adoption against best-in-class SaaS documentation teams. Styled in
the impact.com light theme (blue + magenta), with plain-language questions and hover
tooltips for any specialist term.

- **20 questions** across 8 areas (2–3 each), 5 graded options each → each area scored 0–100
- **Best-in-class callout** revealed only *after* the writer locks in, so it doesn't bias them
- **Radar face-off** vs. a cited benchmark of elite SaaS docs teams (2025–26)
- **Tiers** from 🌱 AI-Curious to 🏆 AI-Native
- **Multi-rater mode** — teammates each get a share code; paste them all to see the
  team average + the spread/alignment between raters
- **Level-up quests** + "what the leaders actually do" with sources
- **Hover tooltips** explain any specialist term (`llms.txt`, `API reference`, etc.)

### Save, share & track
- **Save & resume** — progress is auto-saved; reopen the tab and pick up where you left off
- **History & trends** — every completed run is saved (locally) with a score sparkline,
  per-area ▲/▼ deltas vs. your last run, and a clickable list of past runs
- **Export CSV** — download all saved runs (date, label, overall, per-area scores) for a
  spreadsheet or deck
- **Share via link** — one URL reopens the exact result (`#r=…` solo, `#team=…` group)
- **Export radar PNG** and **Print / Save as PDF** for slides and reviews
- **Keyboard** — `1`–`5` to answer, `Enter` to lock in / advance, `←` to go back

Everything runs **100% in the browser**. No backend, no tracking, no data leaves the
device — share codes, history and links are all encoded/stored locally.

> **Note:** Save & resume and History use the browser's local storage, so they're
> **per-browser, per-device** (not synced between people or machines). That's ideal for
> "track *my* team's quarterly runs on my laptop." Cross-device shared history would need
> a backend, which this single-file design intentionally avoids.

---

## Run it locally

Just open the file:

```bash
open index.html          # macOS
# or double-click index.html in your file manager
```

Or serve it (identical result, useful for testing on phones on your LAN):

```bash
python3 -m http.server 8080
# then visit http://localhost:8080
```

---

## Host it for your team

It's a single static file (`index.html`), so any static host works. Pick one:

### GitHub Pages (free)
```bash
git init && git add . && git commit -m "AI Adoption Arena"
# push to a GitHub repo, then: Settings → Pages → deploy from branch (root)
```
Your team opens `https://<org>.github.io/<repo>/`.

### Netlify / Vercel / Cloudflare Pages (free, drag-and-drop)
- Netlify: drag the folder onto https://app.netlify.com/drop
- Vercel: `npx vercel` in this folder, accept defaults
- Cloudflare Pages: connect the repo or upload the folder

### Internal / corporate static host
Copy `index.html` to any static web root:
```bash
# nginx / Apache
cp index.html /var/www/html/ai-adoption-arena/

# AWS S3 static site
aws s3 cp index.html s3://your-bucket/ai-adoption-arena/index.html
```
No build step, no dependencies, no server-side code.

---

## How multi-rater works (no backend needed)

1. Each teammate opens the app, picks **Assess (solo)**, optionally enters their name,
   and answers the 20 questions.
2. At the end they get a **share code** (e.g. `AIA2-eyJ2Ijoy...`). They copy it and send
   it to you (Slack, email, a shared doc).
3. You open the app, pick **Build team view**, paste all the codes (one per line), and
   get the team's **average radar**, the **min–max spread** per dimension, and an
   **alignment badge** showing where raters agree or disagree.

Because codes are self-contained, this works across machines with zero infrastructure.

---

## Customising the benchmark

All content lives in the `DIMS` array near the top of the `<script>` in `index.html`:

- `bench` — the best-in-class target score (0–100) for each dimension
- `benchNote` / `practice` / `examples` — the guidance and cited sources shown to users
- `questions[].opts` — each option is `["label", score]`; add/remove options freely
- `TIERS` — the tier thresholds and names

Edit, save, refresh. No rebuild.

> ⚠️ Benchmarks are an *informed composite* of public 2025–26 practices (Stripe, Twilio,
> Datadog, Corelight, Vercel, Algolia, kapa.ai, Lyft, Intercom, GitLab, GitBook, etc.),
> not audited figures. Treat it as a motivational mirror, not market research.
