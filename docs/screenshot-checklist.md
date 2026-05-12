# Public Repo Screenshot Refresh Checklist

The screenshots in `screenshots/` are dated 2026-04-30 and predate Wave 34 + 35 product changes. The README marketing now claims features that don't show in the screenshots — credibility hit on the public landing.

This file lists exactly which shots to take. About 30 minutes of clicking.

---

## Setup (one-time)

1. **Browser**: Chrome or Edge at 1920x1080 (full HD). Use devtools device mode if your monitor isn't 1920px wide.
2. **Theme**: Dark mode (the platform default).
3. **Cleared state**:
   - Sign in to your admin account
   - `/dashboard` should look populated, not empty (run `npm run seed:test-scenario` first if needed)
4. **No browser chrome**: hide extensions toolbar, bookmarks bar. F11 for full-screen if it helps.
5. **Naming convention**: Use the EXACT filenames below — the README references them by name.

---

## Required screenshots

### `hero.png`
- **URL**: `/`
- **What**: Above-the-fold landing page hero with Marco-correction translation showcase
- **Crop**: Full viewport
- **Note**: Don't change unless the homepage has been redesigned. Existing one is probably still accurate.

### `experts.png`
- **URL**: `/experts`
- **What**: Marketplace listing with the **Native / Global / All** pool toggle visible at the top (Wave 34 addition)
- **Crop**: Top of page including the pool toggle + at least 3-4 Expert cards below
- **Critical**: Must show the language-tier toggle. If you don't see it, set `users.spoken_languages` on your account to a non-empty array first.
- **What's new in this shot vs the old one**: The Native/Global/All toggle row, the "speaks XX" or "+ translation included" pill on Expert cards near the rate.

### `pricing.png`
- **URL**: `/pricing`
- **What**: Pricing page top section + at least one package card
- **Crop**: Full pricing hero + the 3 package cards
- **Note**: Existing one is probably still accurate. Re-take if any pricing copy changed.

### `how-it-works.png`
- **URL**: `/how-it-works`
- **What**: Steps 1-5 of the session flow
- **Crop**: Show all 5 steps in one screenshot if possible, otherwise the first 3 + step 4 ("AI translates across languages" — Wave 35 copy update)
- **What's new**: Step 4 copy now mentions "Live Interpreter Mode auto-engages on cross-language bookings... ~250-400ms end-to-end". Old shot likely shows the older "30+/100+" language split framing.

### `nexus.png`
- **URL**: `/nexus`
- **What**: The 3D Knowledge Map with domain spheres
- **Crop**: Centred on the orb cluster, no UI chrome
- **Note**: Existing one is probably still accurate.

### `translation-showcase.png`
- **URL**: `/` (or wherever the Marco-correction loop is rendered)
- **What**: The native-speaker correction loop ("we say 'come si deve', not 'autentica'")
- **Crop**: The full panel
- **Note**: Existing one is probably still accurate. The fake stat got removed from the caption in the README; the screenshot itself doesn't need to change.

---

## New screenshot to add: `booking-tier.png`

The booking modal showing the cross-language premium calculation is a strong sales point that the public repo doesn't currently surface.

- **URL**: `/experts/<any-creator-id>` then click "Book a Session"
- **What**: The BookingModal with the language-tier badge ("Native" or "Global" + the premium calc) visible
- **Critical**: Must show a GLOBAL pool booking so the premium is visible. If your account speaks the Expert's language, set `users.spoken_languages` temporarily to something else, then revert after.
- **Crop**: The modal itself, with a bit of background context around it.

Add to README in the "Native vs Global Expert pools" section.

---

## New screenshot to add: `session-upgrade.png` (OPTIONAL)

The mid-session "Switch to translated" button is the user-facing form of Wave 35's biggest new feature.

- **URL**: `/session/<any-active-session-id>`
- **What**: The session header with the amber "Switch to translated" button visible
- **Difficulty**: Needs an ACTIVE same-language session. Seed via `npm run seed:test-scenario` or fake by running:

  ```sql
  UPDATE sessions SET status='active', live_interpreter_enabled=false,
                       started_at=NOW(), room_url='https://example.com'
  WHERE id='<some-test-session-id>';
  ```

- **Crop**: Header bar showing the Live indicator + duration + the upgrade button
- **Optional but high-value**: This is a unique platform feature.

If you skip this one, the README's mid-session upgrade section in "Native vs Global Expert pools" still reads fine.

---

## How to deliver

1. Save all PNGs to a local folder
2. Drop them into `D:\AI\cliptips-public\screenshots\` (overwriting the old ones)
3. Commit + push:

   ```bash
   cd D:/AI/cliptips-public
   git add screenshots/
   git commit -m "Refresh screenshots for Wave 34/35 features (Native/Global pools, mid-session upgrade)"
   git push
   ```

Or paste the file paths in chat and I'll do the commit + push.

---

## What NOT to include

- Admin surfaces (`/admin/*`) — internal moat, don't expose
- Dev workbenches (`/dev/*`) — internal moat
- Anything showing real user emails, real Stripe IDs, real Clerk IDs, or real wallet balances above the test top-up
- The Quality Judge / dubbing admin UI — internal moat

If a screenshot accidentally captures any of the above, blur/crop it before saving.
