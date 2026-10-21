# Copilot Brief: Portfolio v2 (Modern, Technical, Projects First)

**Owner:** Justin Wimmer. Claude (co-project-manager) wrote this brief on Oct 21, 2026, after reviewing the live page.
**Current page:** `portfolio_console.html`, served locally at http://127.0.0.1:5001/
**Goal:** a modern, technical, bluer design. The projects are the main attraction, the copy is new, and the existing files are kept and upgraded rather than replaced.

---

## Rules (from Justin)

- **Ask before you build.** Start with Step 0. Stop after every step, show what changed, and wait for his OK.
- **Be efficient.** He's on Copilot Free with a modest PC. Make targeted edits, not full-file rewrites, unless he approves one.
- **Stay light.** Plain HTML/CSS/JS, as the site uses now. Ask before adding any library or build step.
- **Use the copy in this brief word for word.** If something doesn't fit, ask. Don't invent claims, numbers or employers.
- **Private projects stay private.** No links to the Z or Sports Pro repos, and no personal data in screenshots.
- End each step with how to preview it, plus what he should see.

---

## Step 0: Confirm the plan (no code)

Claude reviewed the live page. Check these findings against the files, propose a short file-by-file plan, then wait.

### What exists today

- **Files:** `portfolio_console.html`, `style.css`, `app.js`, `labs.html`, `z-showcase.html`, `projects/z-ai-assistant.html`, `sports-pro.html`, `/assets/Justin-Wimmer-Resume.pdf`
- **Current order:** header → hero → About → Experience → Featured Projects (2 small cards) → Labs (one button) → Contact → footer
- **Font:** Inter. **Images on the page:** none.

### Keep

- The skip link, the anchor nav, and the `mailto:`, `tel:` and GitHub links
- The "Private project · runs locally" labels
- The case-study pages and `labs.html`. Restyle them; don't delete them.
- The existing section ids. Add new ones as needed.

### Fix

1. **Bug: blank gaps.** There's a large empty area after the Experience list (the Kiawah row doesn't show) and another after Contact. The scroll-reveal in `app.js` is probably leaving elements hidden. Content must be visible by default, with the animation only adding motion. **Fix this first.**
2. **Repeats.** The role line and "Roanoke, VA · Open to remote work" appear in both the header and the hero. Keep them in the hero only. Fold the About text into the hero and How I Work, and drop the separate About block.
3. **Projects come too late.** Move them directly under the hero, as full showcases.
4. **Labs are hidden.** Show a 6-card preview with filters on the home page, plus **View all 20 labs →**.
5. **No visuals.** Add browser-window frames with screenshot placeholders.
6. **Vague link.** Rename "Controlled showcase" to **Live demo walkthrough** if `z-showcase.html` is a demo. If it isn't, ask Justin.
7. **Nav.** Make it sticky and add a **Resume** button.
8. **Flat hero.** Replace it with the new hero and proof chips below.

### New order

Sticky header → Hero → `#featured-projects` Featured Builds → `#labs` The Lab → `#approach` How I Work → `#experience` Track Record → `#contact` → footer

---

## 1. Design system

**Feel:** a high-end engineering tool: calm, precise and confident. It's blue all the way through, from deep navy to the steel ocean blue of a modern developer tool, with crisp white space between.

### Colors (CSS variables, defined in one place)

| Token | Value | Use |
|---|---|---|
| `--navy-950` | `#071833` | Footer, deepest contrast, text on ice |
| `--steel-900` | `#184767` | Hero band and Contact band backgrounds, sticky nav when scrolled over dark sections |
| `--steel-800` | `#1D557B` | Featured Builds band background (the main showcase surface) |
| `--steel-700` | `#2C6284` | Cards and screenshot frames on steel bands |
| `--steel-600` | `#366B8B` | Raised elements on steel: chip backgrounds, hover state for cards, input-style blocks |
| `--blue-600` | `#1F5FD6` | Primary buttons and active nav on light sections |
| `--blue-400` | `#5B9BFF` | Accents on steel: links, focus ring, scroll bar, numbered labels |
| `--ice-50` | `#F3F7FD` | Alternate light sections |
| `--ice-100` | `#E4EDFB` | Borders and subtle fills on light sections |
| `--mist` | `#D7E6F2` | Body text on steel backgrounds |
| `--ink` | `#0F1B2D` | Body text on light backgrounds |
| `--slate` | `#5A6B85` | Secondary text and dates on light |
| `--white` | `#FFFFFF` | Main light background, headings on steel |

**One warm accent, used sparingly:** `--sand` `#C59478` for the small number labels (`01`, `02`) and one hairline per project showcase only. It mirrors the code-highlight warmth in a developer IDE. Use no other hues.

**Contrast:** headings on steel are `--white`, body text is `--mist`, and links are `--blue-400`. Check every pair against WCAG AA.

### Type

- **Inter** for headings and body. Headings are 600–700 weight with -0.02em tracking.
- **JetBrains Mono** for small labels, section numbers, tech chips and the "Under the hood" blocks, so they read like a code panel.
- Scale: hero 56–64px desktop / 36px mobile; section titles 36px; body 17px at a 1.65 line-height. Body text tops out at about 68 characters per line.

### Technical, but subtle

- A faint blueprint grid on the hero and Featured Builds bands (1px lines at 5–6% white).
- A thin scroll-progress bar at the top in `--blue-400`.
- Numbered mono section labels: `// 01 FEATURED BUILDS`.
- **"Under the hood" panels styled like a code card:** `--steel-700` background, 12px radius, mono text, and a small `</>` icon with the label `under the hood` at the top. This is the same look as the code card in a developer tool.
- Screenshots go inside a minimal browser frame (three dots and a `localhost` URL bar), in `--steel-700`.
- Cards have a 12px radius and 1px borders. On hover they lift 2px, and the border shifts to `--blue-400`.
- One fade-up per element as it scrolls in, applied on top of visible content. Respect `prefers-reduced-motion`.

**Avoid:** neon, glow, heavy gradients, particle effects, typing animations, stock images, emoji.

### Layout and flow

- **Sticky nav:** `Work · Lab · Approach · Experience · Contact`, plus a **Resume** button. The active section is highlighted. Over steel bands the nav uses `--steel-900` with white text; over light sections it uses blurred white with `--ink` text.
- **Section rhythm:** Hero (`--steel-900`) → Featured Builds (`--steel-800`) → The Lab (white) → How I Work (`--ice-50`) → Track Record (white) → Contact (`--steel-900`) → Footer (`--navy-950`).
- Every section ends with a small **next link**, like `Next: The Lab ↓`, so the page reads like a guided tour.
- Mobile-first. It must look right at 375px and on a portrait monitor (1080×1920), with no horizontal scroll and visible focus states.

---

## 2. Page structure and copy (use as written)

### Hero (`--steel-900`, blueprint grid)

- Label: `// JUSTIN WIMMER`
- Headline: **I build tools that solve real problems.**
- Subline: *Technical support and software development. Ten years of taking care of people, now backed by code.*
- Meta: `Roanoke, VA · Open to remote work`
- Buttons: **See the work** (scrolls to Featured Builds) · **Download resume** (`/assets/Justin-Wimmer-Resume.pdf`)
- Proof chips (`--steel-600` background): `100+ API endpoints shipped` · `$1.2M+ sold in one season` · `U.S. Navy veteran`

### `// 01 FEATURED BUILDS` (`--steel-800`, the main attraction)

Title: **Featured Builds**
Intro: *Real software I use every day, built from scratch and still growing.*

Each project gets a **large split layout**, with the screenshot frame on one side and text on the other, alternating sides. Each one shows its number (in `--sand`), name, tagline, overview, a "What it does" list, an "Under the hood" code-card panel, stack chips, the `Private build · runs locally` label, and its case-study link.

---

**01 — Z**
*Tagline:* **My AI operating system. It runs my day.**

*Overview:* Z is a personal command center that lives on my PC. One dashboard handles chat, planning, scheduling, notes and system health, and a local AI model ties it together. No cloud, no subscription, and nothing leaves the machine.

*What it does:*
- **Talk to it:** streaming AI chat with voice input and spoken replies.
- **Plan the day:** a built-in daily planner (my C.O.O.L. system), calendar and project map.
- **Remember things:** semantic search over past notes and conversations.
- **Keep the PC healthy:** live system stats, cleanup and safe-delete tools.
- **Write code, safely:** a coding agent that proposes changes as diffs and waits for my "yes."

*Under the hood:* a FastAPI backend with 100+ REST endpoints over SQLite, a React + Vite + Tailwind front end, and local language models through Ollama, tuned to run on a 4 GB GPU. Covered by unit tests and built in planned phases.

*Chips:* `PYTHON` `FASTAPI` `REACT` `TAILWIND` `SQLITE` `OLLAMA` `WHISPER` `PIPER`
*Links:* **Read the case study** (`projects/z-ai-assistant.html`) · **Live demo walkthrough** (`z-showcase.html`, pending Justin's answer in Step 0)

---

**02 — Sports Pro**
*Tagline:* **Sports research, minus the noise.**

*Overview:* Sports Pro turns piles of stats into a quick, clear read. Each sport gets its own page, built around career numbers and matchups, with the heavy lifting done behind the scenes.

*What it does:*
- **Four sports, one hub:** golf, NBA, NHL and football.
- **Player-first:** career stats and matchup context for every player profile.
- **Key findings up front:** the answer on screen, with the detail one click away.
- **Golf done right:** course-of-the-week breakdowns and player profiles.

*Under the hood:* Python collects and shapes the data, and a lightweight HTML/CSS/JS front end presents it. Hosted locally and designed to grow sport by sport.

*Chips:* `PYTHON` `JAVASCRIPT` `HTML` `CSS` `DATA ANALYSIS`
*Link:* **Read the case study** (`sports-pro.html`)

---

**03 — Z-CORE**
*Tagline:* **The front door to Z.**

*Overview:* An animated live wallpaper for Windows: a glowing Z emblem with orbiting lights over an underwater art-deco city. Double-click the core and the Z dashboard opens.

*Under the hood:* HTML, CSS and JavaScript animation running in Lively Wallpaper, wired to launch the local dashboard.

*Chips:* `JAVASCRIPT` `CSS ANIMATION` `LIVELY`

---

End: `Next: The Lab ↓`

### `// 02 THE LAB` (white)

Title: **The Lab**
Intro: *Twenty focused builds. Each one tackles a real security, support or networking problem.*

**Home page:** a 6-card grid (2 per row on desktop) with filter chips `All · Security · IT Support · Networking · Automation`, then **View all 20 labs →** linking to `labs.html`. Home picks: Network Scanner, SIEM Log Analyzer, Device Troubleshooting Toolkit, Network Monitoring Dashboard, Device Configuration Utility, REST API Backend.

**`labs.html`:** the full 20-card grid with the same filters and card style. Restyle each lab page to match, keeping its content.

One-liners (match them to the existing projects):

- **Network Scanner:** multithreaded scans that map open ports and running services.
- **SIEM Log Analyzer:** parses logs, flags anomalies, and correlates events like a blue team would.
- **Vulnerability Toolkit:** checks installed software against known CVEs and reports the risk.
- **Password Cracking Lab:** tests hashing and password policies in a controlled lab.
- **OWASP Juice Shop Testing:** hands-on web app testing against the OWASP Top 10.
- **Device Troubleshooting Toolkit:** a GUI that diagnoses CPU, RAM, disk, driver and network problems.
- **Messaging Diagnostic Simulator:** tests RCS/SMS fallback and message delivery issues.
- **System Health Checker:** one scan for updates, drivers, storage and network config.
- **Network Diagnostic Utility:** ping, traceroute, DNS and latency checks in one tool.
- **Support Automation Scripts:** automates help-desk chores like log collection and cleanup.
- **Network Monitoring Dashboard:** SNMP-powered uptime, latency and bandwidth at a glance.
- **Ping & Latency Analyzer:** continuous multi-host checks that catch packet loss.
- **Subnet Calculator:** CIDR ranges, host counts and boundaries, instantly.
- **Network Inventory Tool:** pulls device info from APIs into a structured database.
- **Device Configuration Utility:** pushes and validates router and switch configs over SSH.
- **REST API Backend:** FastAPI with JWT authentication and full CRUD.
- **Personal Dashboard App:** live system, weather and network data through REST APIs.
- **File Automation Toolkit:** organizes, renames, compresses and syncs folders automatically.
- **Portfolio Website:** this site.

If the site has a 20th project not on this list, keep its current description and tell Justin.

End: `Next: How I work ↓`

### `// 03 APPROACH` (`--ice-50`)

Title: **How I Work**

Three cards:

1. **Listen first.** Every fix starts with understanding the person who has the problem.
2. **Fix it right.** I troubleshoot step by step until I find the root cause, not just the symptom.
3. **Explain it plain.** If it's technical, I make it make sense. No jargon walls.

End: `Next: Track record ↓`

### `// 04 EXPERIENCE` (white)

Title: **Track Record**
Intro: *A decade of serving members, guests and buyers, plus service in the U.S. Navy.*

Stat tiles (`--steel-800` background, white numbers):
- **$1.2M+** sold in one season at Webster Marine
- **10+ years** of customer-facing work
- **U.S. Navy:** Hospital Corpsman

Timeline, one line each (all six rows must show):
- **Ballyhack Golf Club** · Golf Caddie · Mar–Jul 2026
- **Webster Marine** · Sales Associate · May–Dec 2025
- **Willow Oaks Country Club** · Pro-Shop Manager · Oct 2024–Apr 2025
- **Sycamore Creek Golf Course** · Pro-Shop Manager · Apr–Oct 2024
- **U.S. Navy** · Hospital Corpsman, Dental Laboratory · Sep 2022–Mar 2024
- **Kiawah Island Ocean Course** · Golf Caddie · Jul 2021–Jun 2022

Then **Full resume →**, followed by the education line: **B.A., International Relations, University of Lynchburg** · Student Government Director of Administration

### `// 05 CONTACT` (`--steel-900`)

- Title: **Got a problem worth solving?**
- Line: *I'm looking for remote work in technical support, customer support or junior development. Let's talk.*
- Buttons: **Email me** (`mailto:justin.soc@outlook.com`) · **Download resume**
- Small line: `(804) 508-9664 · github.com/grey-ghost-1`

### Footer (`--navy-950`)

`© 2026 Justin Wimmer · Built by hand in Roanoke, VA`

### Meta

- `<title>`: **Justin Wimmer | Technical Support & Software Development**
- Description: *Technical support and software developer. Featured builds: Z, an AI operating system, and Sports Pro, a sports research platform.*
- Social preview image: a `--steel-900` background with the name and the headline in white.

---

## 3. Steps (stop for Justin's OK after each)

| Step | What | Done when |
|---|---|---|
| 0 | Confirm findings + plan | Justin approves |
| 1 | Fix the blank-gap bug; color tokens, fonts, sticky nav with Resume button, scroll bar, section rhythm and new order; remove the repeats | Nothing is hidden, and the shell matches the new look on desktop and mobile |
| 2 | Hero + Featured Builds (Z, Sports Pro, Z-CORE): screenshot frames, code-card panels, case-study links | The projects look finished; screenshot placeholders are marked |
| 3 | The Lab: 6-card preview on home, full grid on `labs.html`; restyle case-study and lab pages | All pages load, the filters work, and the look is consistent |
| 4 | How I Work, Track Record, Contact, footer, meta | All copy matches this brief |
| 5 | Polish: motion, contrast on steel, accessibility, Lighthouse | Accessibility and Best Practices ≥ 90; nothing breaks at 375px |

**Screenshots:** Justin will provide them for Z, Sports Pro and Z-CORE. Until then, use marked placeholders inside the frames.
