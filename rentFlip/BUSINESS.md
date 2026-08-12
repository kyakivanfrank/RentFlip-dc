# RentFlip — Business Rules (Source of Truth)

> Authoritative business-logic reference for RentFlip. Pairs with `DESIGN.md` (visual
> system) and the Claude prototype (`RentFlip.dc.html`), which is the approved UX direction.
> Items marked **(proposed)** were raised in architecture discussion and are **not final** —
> confirm before building. Each section notes the prototype screen that expresses it.

---

## 1. Core philosophy
RentFlip **never handles, holds, or routes funds.** It is a **ledger, verification, and
digital-evidence layer.** Every real payment — rent, utilities, broker commissions — happens
peer-to-peer **outside** the app (mobile money, bank, cash). The single exception is the
platform fee (§5), billed by STK Push.

→ *Prototype:* the tenant **Log a Payment** screen says this explicitly ("RentFlip records
your payment — it never moves money").

## 2. Accounts
- **Auth = phone number + SMS OTP only.** No email/password. *(Screens: Verify phone → Enter OTP.)*
- Every verified phone owns a **Landlord profile and a Tenant profile simultaneously**, from
  signup, regardless of which role was picked first during onboarding.
- A settings toggle switches which profile (and theme) the user is acting in at any time.
  *(Screen: Profile → "Switch as Tenant/Landlord" — flips accent purple ↔ amber.)*
- **Asset hierarchy:** Property Group → individual Rental Unit. A landlord invites a tenant via
  a **cryptographically unique deep link tied to one specific vacant unit**; opening it binds
  that tenant's profile to that unit's ledger. *(Screen: **Invite Tenant** — single-use link,
  7-day expiry, regenerate to invalidate.)*

## 3. The verification loop (LOCKED)
The spine of the product. *(Screens: tenant **Log a Payment** → **Awaiting verification**;
landlord **Verify Payment** → **Approved**.)*
- Tenant logs the **amount paid** + the **Carrier Transaction ID** (or attaches a compressed
  receipt photo, <300KB). Entry enters **`pending_verification`**, visible on both dashboards.
- Landlord cross-checks against their own SMS/bank records and either taps **Approve** or does
  nothing.
- **There is no Reject, Deny, or Delete** anywhere in this flow. A wrong/fraudulent entry simply
  stays `pending_verification` forever; the burden of proof to resolve it stays with the tenant.
  *(Prototype: the only actions are **Approve payment** and **Leave pending**.)*
- **Approval triggers, in order:** balance update → mark period clear → automated receipt
  generation → SMS confirmation to tenant via the EgoSMS webhook pipeline.

## 4. Maintenance & miscellaneous costs (NOT a dedicated feature)
- **No maintenance ticket object, no ticket lifecycle, no maintenance chat thread.**
- Maintenance and misc costs (water, electricity tokens, garbage, security, repairs) are **plain
  line items a landlord adds for their own record-keeping.** They show as an itemised breakdown
  and roll into the **same combined monthly total** shown alongside rent. *(Screen: **Costs ·
  January** — Rent + Costs = Combined monthly total; itemised list; "+ Add line item".)*
- They trigger **no** notifications, threads, or tenant-facing workflow beyond appearing in that
  combined breakdown.
- **Messaging consequence:** the **only** persistent chat surface anywhere in the app is the
  Paste Board deal-closing thread (§6). No general-purpose or maintenance-anchored messaging.

## 5. Platform fee (LOCKED, corrected from earlier draft)
*(Screen: **Platform Invoice**.)*
- **0.5% of a landlord's total cleared and approved collection volume** for the 30-day cycle.
- **Uncapped.** (An earlier 30,000 UGX monthly ceiling was a mistake — removed. No ceiling at
  any volume.)
- Billed via **STK Push** — the **one Native Gateway Exception** in the whole app — at cycle close.
- **Small-invoice rule:** if a calculated invoice is under ~2,000–3,000 UGX, **don't** run the STK
  push — roll it into the next cycle (avoids paying a merchant fee to collect barely more than the fee).
- **Gate 1 (unpaid invoice):** strict **72-hour grace period** before lockdown engages (§7).
- *Watch-for signal (not a rule to build):* if top accounts' logged volume drops right after an
  uncapped invoice generates, that's the indicator the uncapped rate needs revisiting — not a
  preemptive guess.

## 6. Paste Board (LOCKED core mechanics)
Ambient feature, accessible from either profile. **No separate broker account type.**
*(Screens: **Paste Board · Feed**, **Broker Link**, **Deal chat**.)*
- **Visibility tiers:** **Private Contact Feed** (free — landlord's phone contacts + current
  verified tenants only) and **Global Regional Feed** (paid micro-fee, public within a district).
  *(Prototype: segmented Private/Global with a tier caption.)*
- **Identity masking:** a broker's generated marketing link strips the landlord's name, number,
  building ID and coordinates. The public sees only the **broker's name, rating, and contact
  options.** *(Screen: Broker Link → "Public sees / Hidden from public".)*
- The landlord can **Revoke Broker** on any active link at any time, instantly invalidating it.
- **Deal-closing chat** is the one persistent chat surface: **500-character limit, max one photo
  per message (compressed <300KB), no other attachment types, no emoji picker.** *(Screen: Deal
  chat — composer shows "1 photo · 500 characters · no other attachments".)*

### 6a. Paste Board monetization **(proposed — confirm before building)**
- Tiered public listing pricing instead of one flat boost fee: **Standard** regional boost /
  **Featured** (guaranteed top-of-feed for N days) / **Re-bump** (push a still-vacant listing back
  to the top). *(Prototype hints at this with a "FEATURED" pill on global-feed cards.)*
- **Tenant-side search alerts** (budget, area, unit type) so a boosted listing reaches matching
  people — this is what justifies the Featured tier's price.
- Paid **"Top Broker"** placement for high-reliability brokers when a landlord browses brokers.
- All reuse the existing STK Push mechanism. No new payment integration.

### 6b. Broker–landlord trust mechanics **(proposed — confirm before building)**
- Every marketing link stores an **immutable, timestamped commission snapshot** (unit, agreed
  amount/%, date) both sides can reference in a dispute. *(Prototype: Broker Link → "Commission
  snapshot · IMMUTABLE".)*
- A broker's dispute flag triggers a **48-hour notice** to the landlord before it affects their
  public reliability score — not an instant, irreversible penalty.
- Brokers can flag a concern on a deal that **fell through before closing**, not only completed deals.
- *Launch recommendation (not code):* hand-vet and onboard the first ~20 brokers to seed a
  trustworthy track record before opening the marketplace broadly.

## 7. Dual lockdown gates (LOCKED, with a flagged risk)
*(Screen: **Lockdown gate** — un-dismissible overlay, toggle between Gate 1 / Gate 2.)*
- **Gate 1 — unpaid platform invoice:** 72-hour grace, then **hard lockdown**.
- **Gate 2 — no successful server sync for 72 consecutive hours:** hard lockdown — conceals all
  cached historical data, blocks all CRUD, shows an un-dismissible overlay.
- **⚠ Flagged risk (resolve before Phase 4):** Uganda's telecom regulator has previously ordered
  nationwide internet shutdowns during contested elections. A repeat — or any multi-day regional
  outage — would trigger Gate 2 for a large share of users at once, through no fault of their own.
  Decide before Phase 4 whether Gate 2 should **degrade gracefully** (keep read access to cached
  data, only block new-record creation) rather than mirroring Gate 1's full lockdown. This file
  intentionally does not pre-decide that — see `docs/build-roadmap.md` Phase 4.

## 8. Explicitly out of scope for v1
- **Vendor/contractor lead-gen** tied to maintenance tickets — shelved (tickets don't exist as a
  surface). Could resurface attached to a property page later.
- **Delegate/agent access** — letting someone other than the owner manage a landlord's properties.
  Noted as a future distribution lever (caretakers/agents managing several landlords at once), not v1.
- **Premium tax-ready export reports** — possible later, but must stay strictly private and opt-in.
  Rental-income tax is sensitive for many Ugandan landlords; a feature reading as "helps you report
  to URA" would suppress adoption rather than help it.

---

## Screen ↔ rule map (prototype: `RentFlip.dc.html`)

| Business rule | Screen(s) |
|---|---|
| §1 ledger-not-funds philosophy | Tenant · Log a Payment (banner) |
| §2 phone+OTP auth | Verify phone, Enter OTP |
| §2 dual profile + theme switch | Profile (Switch as …) |
| §2 unit-bound invite deep link | Invite Tenant |
| §3 verification loop | Log a Payment → Awaiting verification; Verify Payment → Approved |
| §4 maintenance/misc costs | Costs · January |
| §5 platform fee / STK Push | Platform Invoice |
| §6 Paste Board tiers + masking | Paste Board · Feed, Broker Link |
| §6 deal-closing chat | Deal chat |
| §6a Featured tier (proposed) | "FEATURED" pill on global feed |
| §6b commission snapshot (proposed) | Broker Link · Commission snapshot |
| §7 dual lockdown gates | Lockdown gate |

> **Not yet built (deliberately):** the small-invoice roll-forward (§5), tenant search alerts
> (§6a), Top-Broker placement (§6a), the 48-hour dispute-notice flow (§6b), and graceful Gate 2
> degradation (§7). These are logic/decision items, not screens — wire them when confirmed.
