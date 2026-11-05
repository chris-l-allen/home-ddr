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

Budget: the original **~$50–75 CAD** gift target is obsolete now that the owner
chose a metal L-TEK plus a refurbished Mac. Current researched prices: **L-TEK
Core CAD 389 + ~$64 import**, **refurb Mac mini $929 CAD** (see §7.1). No purchases
made; budget not yet set.

---

## 2. Current state (verified 2026-11-05)

- **FACT** Repo scaffolded: README, HANDOFF, AGENTS, docs, HomeServer, scripts,
  launchd plist. Nothing installed on the Mac yet.
- **FACT** Host Mac: Intel `x86_64`, macOS `26.5.2`, 16 GB RAM.
- **FACT** Available tools: Python `3.14.6`, Node `25.5.0`, git, `gh` (logged in as
  `chris-l-allen`, repo scope), Homebrew.
- **FACT** No Project OutFox / StepMania in `/Applications`.
- **FACT** OutFox site lists macOS builds (Universal DMG, Intel + Apple Silicon),
  dance-pad support, `.sm`/`.ssc` loading. Latest dev **0.5.0 Final Alpha
  (2025-09-07)**; legacy **0.4.19 LTS** flagged outdated.
- **FACT** (2026-11-05) Owner **declined** installing OutFox on the current Intel
  family Mac. The DDR engine is to run on a dedicated **HomeServer box** — a
  refurbished **Mac Studio or Mac mini** — which has **not been purchased yet**.
- **INFERENCE** OutFox will run on the eventual Mac Studio/mini; verify the build
  architecture and OS version on that box at install time.
- **GUESS** OutFox works on macOS `26.5.2` — untested here. The future box may
  ship with a different macOS version; re-verify there.
- **FACT** Per owner (2026-11-05), HomeServer is verified to run on this Mac.

---

## 3. Decisions made

| # | Decision | Rationale |
|---|---|---|
| 1 | Use **Project OutFox**, not official DDR | Official DDR isn't on macOS; OutFox is free, cross-platform, supports pads |
| 2 | Buy a **metal L-TEK Core USB dance pad** (owner choice, 2026-11-05) | Durable arcade feel; CAD 389 goods + ~$64 import, ships from Poland. No purchase yet |
| 3 | Build HomeServer on **Python stdlib** | Zero dependencies; runs anywhere; trivial to maintain |
| 4 | Keep song packs/media **gitignored** | Large binaries; share via LAN or object storage instead |
| 5 | Follow existing homelab doc style | Consistency with `mac-studio-ai-homeserver` |
| 6 | Run OutFox on a **dedicated HomeServer box** (refurbished Mac Studio/mini), **not** the current family Mac (owner, 2026-11-05) | Owner's call; keeps the DDR station on the server. Hardware not yet bought |
| 7 | **Recommended buy (pending approval):** refurb **Mac mini M4 16GB/256GB ($929 CAD)** + **L-TEK Core (CAD 389)**; ship to **Toronto, ON** | Cheapest researched combo that meets the workload; no bar needed for a 5-year-old. Street address and full postal code deliberately kept out of the repo |

---

## 4. Open questions

1. **Hardware** — which refurbished box: **Mac mini** (cheaper, low power) or
   **Mac Studio** (more headroom)? What budget, and Intel vs Apple Silicon?
   OutFox's macOS build is Universal, so either arch works in principle.
   **Recommendation (INFERENCE, not tested):** refurb **Mac mini M4 16GB/256GB at
   $929 CAD** is ample for OutFox + the static server; the cheapest refurb Mac
   Studio seen was $2,729 CAD (M4 Max), which is overkill here. 256GB may need an
   external SSD later for a big song/media library.
2. **Custom charts** — do we author Alvin & the Chipmunks charts (hours of manual
   work) or just use existing kid packs?
3. **Two pads** — single-player now, second pad later?
4. **Reverse proxy** — publish HomeServer via the existing Caddy stack or keep it
   standalone on `:8787`?

---

## 5. Next actions (ordered)

1. **Hardware decision** — recommendation recorded: refurb **Mac mini M4 16/256
   ($929 CAD)** + **L-TEK Core (CAD 389)**, ship to Toronto, ON. Waiting on the owner's
   explicit purchase approval; no purchase without it.
2. **Pad purchase** — metal L-TEK **Core** (CAD 389 goods + ~$64 Ontario import;
   shipping cart-only). No bar needed for a 5-year-old. No purchase without owner
   go-ahead.
3. On the new box: `./scripts/install-outfox.sh` → install OutFox, launch once;
   confirm the Universal build runs on that macOS version.
4. Plug in the L-TEK; confirm OutFox sees arrow input; play a default chart.
5. `./scripts/link-songpacks.sh`; drop 2–3 kid packs into `songpacks/`.
6. Verify low-difficulty charts (1–3 foot) are playable for a 5-year-old.
7. Start HomeServer (`./scripts/serve.sh`) and load it from a phone on the LAN.
8. Decide on custom Alvin charts; if yes, chart a short pack.
9. Add to `mac-studio-ai-homeserver` Caddy routing (future).

> **Blocked/deferred:** steps 3–6 wait on the new hardware; step 7 can be tested on
> the current Mac with owner permission (it is network-facing).

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

## 7. Candidate purchases (prices checked 2026-11-05)

| Item | Price (CAD) | Link |
|---|---|---|
| **L-TEK Core (chosen model)** | CAD 389 regular (240€ page) | https://www.iamats.com/shop/dance-mat-ltek-core/ |
| L-TEK Core via US reseller | $639 CAD (sold out) | https://ddrpad.com/en-ca/products/l-tek-core-dance-pad |
| VTech Kidi Superstar Jr. karaoke | $59.99 | https://www.amazon.ca/dp/B0BS2SCS2W |
| VTech Sing It Out karaoke mic | $46.96 | https://www.amazon.ca/dp/B09MVV6V5P |

> **Superseded:** the soft-pad options below are no longer the plan. Owner chose a
> metal L-TEK (2026-11-05). Nothing has been purchased.

| Soft-pad options (superseded) | Price (CAD) | Link |
|---|---|---|
| OSTENT USB StepMania dance mat | $31.99 | https://www.amazon.ca/dp/B00FJ2KTXC |
| Domary USB dance pad | $38.60 | https://www.amazon.ca/dp/B0H8YNZ3Q9 |
| CVERY USB dance pad | $52.22 | https://www.amazon.ca/dp/B08DHZFHDX |

> Review counts were not readable by the scraper at research time; these are ranked
> by star rating + brand, not verified review volume. Re-check before buying.

### 7.1 Hardware research (2026-11-05)

**Apple Certified Refurbished (apple.com/ca, CAD, fetched 2026-11-05):**

| Item | Price | Notes |
|---|---|---|
| Mac mini M4, 10-core CPU/GPU, **16GB / 256GB**, Gigabit | **$929** (was $1,099) | Specs verified on product page; 1-yr warranty, 15-day returns |
| Mac mini M4, 10-core CPU/GPU, Gigabit | $1,189 (was $1,399) | RAM/storage not verified |
| Mac mini M4 Pro, 12-core CPU/16-core GPU, Gigabit | $1,949 (was $2,299) | RAM/storage not verified |
| Mac Studio M4 Max, 14-core CPU/32-core GPU | $2,729 (was $3,499) | RAM/storage not verified |

Refurb stock is limited and changes often.

**L-TEK / iAmats (official, Poland; CAD prices are the vendor's own Canada reference):**

| Model | Price | Notes |
|---|---|---|
| **Core** | **CAD 389 regular** (240€ on product page) | 4 arrows, PRO panels, USB; **recommended** |
| Prime | CAD 486 regular (300€) | Illuminated Start/Select, switchable profiles |
| PRO X | from 279€ | All 9 panels printed |
| Core + Handbar | from 461€ | Bar is for advanced play; not needed for a 5-year-old |
| Handbar PRO alone | from 340€ | — |

- **FACT:** iAmats' own Canada guidance (verified 2026-09-13) lists the **Core at
  CAD 389** and Prime at CAD 486. Ships from Poland; 8–12 working days dispatch,
  then up to ~5 days courier. 2-year warranty, 14-day returns.
- **FACT:** official product page says the LTEK Edition software download is
  Windows-only, but the pad is plain USB and works with OutFox on macOS; verify
  with the actual unit.
- **FACT (Canada duty):** these pads classify under **9504.50.00.80**, where both
  MFN and CEUT rates are **Free** — **0% duty**, no CETA paperwork needed.
- **FACT (Ontario tax):** HST is **13%** on the goods' customs value. Qualifying
  international transport is excluded from that tax base (this corrects my earlier
  note that said "goods + shipping").
- **FACT (UPS fees):** disbursement is the greater of **3.7%** of advanced
  duties/taxes or **CAD 12**, plus 13% tax on that fee.
- **FACT (worked Core import estimate):** HST CAD 389 × 13% = **$50.57**;
  disbursement hits the **$12** minimum; tax on the fee **$1.56** →
  **≈ $64.13 CAD import payment** if paid online before delivery (add ~$6 ICOD if
  paid at the door).
- **FACT (shipping):** Canadian rates are weight-based and shown only in the cart.
  The US reference for one 18 kg pad is USD 151 (≈ CAD 210); **Canada differs**, so
  no Canadian shipping figure is quoted here.

**DDRPad.com (US reseller, en-ca storefront in CAD, fetched 2026-11-05):**

| Item | Price | Stock |
|---|---|---|
| L-TEK Core | $639 CAD | **Sold out** |
| L-TEK Prime + Bar | $1,335 CAD (sale; reg. $1,363) | 1 (USB + PS adapter) |

- Ships from Athens, Ohio; worldwide shipping; import taxes/duties may apply;
  30-day returns; shipping at checkout.

**Recommendation (INFERENCE / GUESS, no purchase made):**

- **Mac mini M4 16/256 @ $929 CAD** — best value for OutFox + static server.
  The $2,729 Studio is ~3x for no DDR benefit; only choose it if the box also
  needs to run heavy AI/other workloads.
- **L-TEK Core, no bar** — right size and durability for a 5-year-old. Buy from
  the official store for the 2-year warranty, or DDRPad when in stock for faster
  US shipping. Goods + import ≈ **$453 CAD**; shipping is the open variable. A
  **GUESS** of ~$150–210 shipping puts the Core at **~$600–665 CAD landed** —
  re-quote in the cart.

**Shipping destination (owner, 2026-11-05): Toronto, Ontario, Canada.** The full
postal code was derived and used only for the shipping estimate; it is deliberately
**not recorded** in the repo. Only the FSA **M6H** is stored, and the street
address is excluded.

**Combined budget (GUESS, not a quote):** Mac mini $929 + 13% HST ≈ $1,050; Core
landed ≈ $600–665 → **roughly $1,650–1,715 CAD all-in**. Apple's refurb price also
excludes HST. Re-quote both carts before buying.

**Documented recommendation:** buy the **Mac mini M4 16/256 ($929 CAD)** and the
**L-TEK Core (CAD 389)**. The decision is pending the owner's explicit purchase
approval; nothing has been ordered.

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

Current state: repo scaffolded. OutFox is NOT to be installed on the current Intel
family Mac; owner wants it on a dedicated HomeServer box (refurbished Mac Studio or
Mac mini) that has not been purchased yet. Pad choice: metal L-TEK (not purchased).
Current Mac: Intel x86_64, macOS 26.5.2, 16 GB, Python 3.14.6, Node 25.5.0, git, gh,
Homebrew.

Do next, in order:
1. Confirm the hardware budget: researched picks are a refurb Mac mini M4 16/256
   ($929 CAD) and an L-TEK Core pad (CAD 389 goods + ~$64 import). Do not buy anything
   without an explicit go-ahead.
2. Once the box exists: install Project OutFox (Universal DMG), verify it launches
   on that macOS version.
3. Verify the L-TEK pad is detected as arrow input and a low-difficulty chart is
   playable.
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
- **2026-11-05** — Doc cleanup; recorded owner's need for a refurbished Mac Studio
  or Mac mini (separate).
- **2026-11-05** — Owner chose a **metal L-TEK** pad and **declined** installing
  OutFox on the current Mac; DDR engine moves to the future HomeServer box.
  OutFox install and pad tests are now blocked on hardware purchase.
- **2026-11-05** — Added hardware research (§7.1): refurb Mac mini M4 16/256 at
  $929 CAD recommended; L-TEK Core at CAD 389 recommended. Nothing purchased.
- **2026-11-05** — Documented the recommendation as decision #7; shipping region
  Ontario, Canada (street address excluded from repo). Awaiting purchase approval.
