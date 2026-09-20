# TinyTums V1 — Penpot UI mocks

Customer-share UI for **V1 core (F-001–F-036)** plus **ABDM/ABHA customer screens (F-046)**: warm **iOS** mother/caregiver app + **teal/navy web** hospital portal.

Open the connected Penpot file. Rename it to **TinyTums V1** in the Penpot UI if it still says `New File 1` (API cannot rename).

**Flow in repo** (same boards as Penpot):
- [`flows/tinytums-v1-ui-map.json`](flows/tinytums-v1-ui-map.json) — screens, features, edges, `showIf` / `skipIf`
- [`flows/tinytums-v1-ui-flows.md`](flows/tinytums-v1-ui-flows.md) — Mermaid diagrams
- [`flows/tinytums-v1-ui-overview.mmd`](flows/tinytums-v1-ui-overview.mmd) — short overview
- [`flows/tinytums-v1-ui-nav-mesh.md`](flows/tinytums-v1-ui-nav-mesh.md) — **all screens + all actions** (gap finder + mermaid)
- [`flows/tinytums-v1-ui-nav-mesh.mmd`](flows/tinytums-v1-ui-nav-mesh.mmd) — paste into mermaid.live if preview is slow
- [`flows/tinytums-v1-prototype.json`](flows/tinytums-v1-prototype.json) — live Play interactions (wired vs skipped-cross-page)

## Pages (17)

| Page | Screens |
| --- | --- |
| `00 Cover + map` | Hero + V1/V2 fence + actors |
| `01 Design system` | Colors, type, badges, buttons |
| `02 iOS Onboarding + Home` | Splash, sign-in, OTP, create account, email optional, state, dashboards, **tasks due**, **notifications**, branch states |
| `03 iOS Mother journeys` | **You hub**, profile, lock/correction, privacy + ABDM row, logout, TTC, **period tracking**, pregnancy, postpartum |
| `04 iOS Track + mind` | Weight/BP/glucose + **log sheets**, **symptoms**, **reports library / view**, upload report, PND |
| `05 iOS Child` | List, **Add child**, home, growth, vaccines, milestones, activities |
| `06 iOS Care network` | Search, **hospital page**, **doctor profile**, **allied search**, **share with doctor**, invite, caregivers, book, **reschedule**, **admission team**, packet, messages, teleconsult |
| `07 iOS Caregiver` | Phone login, OTP, read-only home, edit denied |
| `08 Web Ops + patients` | Phone login, OTP, workspace picker/skip, ops, access denied, staff pending, pediatric + **allied workspace**, **monitoring plan** |
| `09 Web Encounter` | Factual summary + **view source**, **correction queue**, **18-section encounter TOC**, verify, Rx, **follow-up book**, inbox, teleconsult |
| `09b Encounter sections` | **§01–§18** labeled fields per [clinical encounter format](../plan/TinyTums%20-%20General%20Clinical%20encounter%20format.md) |
| `10 Web Admission + roles` | Admit, **planned admission**, **admission chart**, care team, discharge + **discharge summary**, nurse, junior, admin, **invite staff**, **verify queue**, **audit log**, **RBAC matrix + 6 role dashboards** |
| `11 iOS ABDM / ABHA` | Hub, create/link, KYC OTP, card, skip, child ABHA, discover, consent, revoke |
| `12 Web ABDM HIP / HIU` | HFR/HPR, link ABHA, care contexts, HIP QR/share, HIU request + outcomes, pick person |
| `13 Walk A mother` | **Play clones** — Home → BP → Book → Packet |
| `14 Walk B clinician` | **Play clones** — Ops → Summary → Encounter → Verify → Rx |
| `15 Walk C ABDM consent` | **Play clones** — OTP → ABHA link → consent → HIU granted |

Board count grows with gap pass; see Penpot for latest layout.

## Prototype (Play mode)

Same-page clicks are wired on the original pages (~79). Penpot cannot `navigate-to` a board on another page.

**Demo walks** (open the walk page, then Play from the start board):

- **Walk A** page `13 Walk A mother` — Dashboard hero → BP → Book → Pre-visit packet
- **Walk B** page `14 Walk B clinician` — Ops → Factual summary → Encounter TOC → Verify → Rx
- **Walk C** page `15 Walk C ABDM consent` — OTP → ABHA hub → Link → KYC → Linked → Discover → Consent → Approve → HIU granted

Walk boards are **detached copies**. Edit masters on pages 02–12; re-clone if a walk is stale. Full link inventory: [`flows/tinytums-v1-prototype.json`](flows/tinytums-v1-prototype.json).

## Auth and workspace

- **Phone + OTP** for iOS mother, caregiver, and web staff. Email optional on mother signup.
- **Workspace picker** (web only): `Role @ Institution`. Shown if 2+ rows; skipped if exactly one. Header switch reuses the same list.
- Mother app and staff portal stay **separate logins** (no Mother/Staff combo picker).

## V1 + ABDM copy rules on screens

- Trends = values, dates, counts, ranges. No auto abnormal/triage.
- Summaries have **View source**.
- Verified fields: lock + **Request correction** + version history.
- Caregiver read-only. Invite-doctor = lead, not a public profile.
- **TinyTums ID** is the product key; ABHA Number/Address and HFR/HPR are **external IDs**.
- ABDM: human consent and record views — **no raw FHIR JSON**. Mother ABHA ≠ child ABHA.
