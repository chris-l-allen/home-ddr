# HANDOFF — HomeDDR + HomeServer

> Read this file first in any new session. It is the single source of truth for
> project state, decisions, and the next actions. Keep it current as work lands.

**Updated:** 2026-11-05
**Owner:** callen
**Repo:** `/Users/callen/home-ddr` (local git; remote optional)

---

## 1. Mission

Build a kid-friendly DDR/rhythm station for a **5-year-old girl** who loves
**dancing, singing, Alvin and the Chipmunks**, plus a tiny **HomeServer** that
publishes the song/media library on the home LAN. No console, no subscriptions.

Budget for the gift itself: **~$50–75 CAD**, but the DDR rig can total
**~$32–$60 CAD** (pad) + free software.

---

## 2. Current state (verified 2026-11-05)

- **FACT** Repo scaffolded: README, HANDOFF, AGENTS, docs, HomeServer, scripts,
  launchd plist. Nothing installed on the Mac yet.
- **FACT** Host Mac: Intel `x86_64`, macOS `26.5.2`, 16 GB RAM.
- **FACT** Available tools: Python `3.14.6`, Node `25.5.0`, git, `gh` (logged in as
  `chris-l-allen`, repo scope), Homebrew.
- **FACT** No Project OutFox / StepMania in `/Applications`.
- **FACT** OutFox site lists macOS builds (Intel + Apple Silicon), dance-pad
  support, `.sm`/`.ssc` loading. Latest dev **0.5.0 Final Alpha (2025-09-07)**;
  legacy **0.4.19 LTS** flagged outdated.
- **INFERENCE** OutFox will run on this Intel Mac; verify the Intel build exists at
  install time.
- **GUESS** OutFox works on macOS `26.5.2` — untested.

---

## 3. Decisions made

| # | Decision | Rationale |
|---|---|---|
| 1 | Use **Project OutFox**, not official DDR | Official DDR isn't on macOS; OutFox is free, cross-platform, supports pads |
| 2 | Buy a **USB dance pad**, not a console | Cheapest path to a real DDR rig; pad = the gift |
| 3 | Build HomeServer on **Python stdlib** | Zero dependencies; runs anywhere; trivial to maintain |
| 4 | Keep song packs/media **gitignored** | Large binaries; share via LAN or object storage instead |
| 5 | Follow existing homelab doc style | Consistency with `mac-studio-ai-homeserver` |

---

## 4. Open questions

1. **"Lou Williams"** — confirm identity (NBA player vs. someone local). If NBA,
   there is no meaningful kids' merch; treat as a theme, not a purchase.
2. **Pad tier** — cheap soft pad now, or metal L-TEK (~$150+, EU shipping)?
3. **Custom charts** — do we author Alvin & the Chipmunks charts (hours of manual
   work) or just use existing kid packs?
4. **Two pads** — single-player now, second pad later?
5. **Reverse proxy** — publish HomeServer via the existing Caddy stack or keep it
   standalone on `:8787`?
6. **Where it lives** — family Mac now; migrate to the Mac Studio when built?

---

## 5. Next actions (ordered)

1. Confirm the Lou Williams reference and pad tier.
2. `./scripts/install-outfox.sh` → install OutFox, launch it once on macOS 26.5.2.
3. Plug in the pad; confirm OutFox sees arrow input; play a default chart.
4. `./scripts/link-songpacks.sh`; drop 2–3 kid packs into `songpacks/`.
5. Verify low-difficulty charts (1–3 foot) are playable for a 5-year-old.
6. Start HomeServer (`./scripts/serve.sh`) and load it from a phone on the LAN.
7. Decide on custom Alvin charts; if yes, chart a short pack.
8. Add to `mac-studio-ai-homeserver` Caddy routing (future).

---

## 6. Key commands

```bash
cd /Users/callen/home-ddr

./scripts/serve.sh                     # HomeServer on 127.0.0.1:8787
HOMEDDR_HOST=0.0.0.0 ./scripts/serve.sh  # expose to LAN
./scripts/install-outfox.sh            # guided OutFox install
./scripts/link-songpacks.sh            # share song library with OutFox
```

---

## 7. Candidate purchases (Amazon.ca, price at time of writing)

| Item | Price (CAD) | Link |
|---|---|---|
| OSTENT USB StepMania dance mat | $31.99 | https://www.amazon.ca/dp/B00FJ2KTXC |
| Domary USB dance pad | $38.60 | https://www.amazon.ca/dp/B0H8YNZ3Q9 |
| CVERY USB dance pad | $52.22 | https://www.amazon.ca/dp/B08DHZFHDX |
| VTech Kidi Superstar Jr. karaoke | $59.99 | https://www.amazon.ca/dp/B0BS2SCS2W |
| VTech Sing It Out karaoke mic | $46.96 | https://www.amazon.ca/dp/B09MVV6V5P |

> Review counts were not readable by the scraper at research time; these are ranked
> by star rating + brand, not verified review volume. Re-check before buying.

---

## 8. Files of record

- `README.md` — what/why/architecture/layout/roadmap.
- `docs/ddr-setup.md` — OutFox, pad, kid difficulty, custom songs.
- `docs/homeserver.md` — server usage + LAN security notes.
- `homeserver/server.py` — the server.
- `scripts/*` — install/serve/link helpers.
- `launchd/com.local.homeddr.plist` — persistence.

---

## 9. Resume prompt

Paste this into a fresh terminal/session to continue:

```
Resume the HomeDDR + HomeServer project.

Repo: /Users/callen/home-ddr
Start by reading HANDOFF.md, then README.md and AGENTS.md.

Mission: a kid-friendly DDR/rhythm station on a family Mac (Project OutFox +
USB dance pad) for a 5-year-old girl who loves dancing, singing, and Alvin and
the Chipmunks, plus a tiny LAN HomeServer that publishes the song packs and
media.

Current state: repo scaffolded; nothing installed; host is an Intel Mac,
macOS 26.5.2, 16 GB, with Python 3.14.6, Node 25.5.0, git, gh, and Homebrew.

Do next, in order:
1. Ask me to confirm (a) the "Lou Williams" reference and (b) pad tier
   (cheap soft pad vs metal L-TEK).
2. Install Project OutFox on the Mac (verify the Intel build and macOS 26.5.2
   compatibility), then confirm it launches.
3. Verify the dance pad is detected as arrow input and a low-difficulty chart
   is playable.
4. Load 2-3 kid-friendly song packs via scripts/link-songpacks.sh.
5. Start HomeServer and confirm it loads from a phone on the LAN.

Rules: follow the evidence discipline in AGENTS.md — label FACT / INFERENCE /
GUESS, never claim something works until tested here, and ask before installing
system software or buying anything. Keep HANDOFF.md updated as you go.
```

---

## 10. Changelog

- **2026-11-05** — Repo scaffolded: README, HANDOFF, AGENTS, docs, HomeServer,
  scripts, launchd plist. Git initialized.
