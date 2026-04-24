# ClipTips

**Live video marketplace with real-time AI translation.**
Book a verified expert by the minute, ask your question on camera, hear the answer in your own language.

[![Status](https://img.shields.io/badge/status-pre--launch%20testing-818cf8?style=flat-square)](https://cliptips-mvp.vercel.app)
[![Next.js](https://img.shields.io/badge/Next.js-15-000000?style=flat-square&logo=next.js)](https://nextjs.org)
[![TypeScript](https://img.shields.io/badge/TypeScript-5-3178c6?style=flat-square&logo=typescript&logoColor=white)](https://typescriptlang.org)
[![Supabase](https://img.shields.io/badge/Supabase-Postgres-3ecf8e?style=flat-square&logo=supabase&logoColor=white)](https://supabase.com)
[![Stripe Connect](https://img.shields.io/badge/Stripe-Connect-635bff?style=flat-square&logo=stripe&logoColor=white)](https://stripe.com/connect)

![ClipTips landing](screenshots/hero.png)

## What is this

The person who can answer your question exists somewhere in the world. They just don't speak your language.

ClipTips closes that gap. An Italian tiler, a Japanese pastry chef, a Queensland lawyer, a Brazilian surgeon — anyone with verifiable expertise can take live video sessions from askers worldwide, in any of 100+ languages. Voice is cloned and re-dubbed into the asker's language with subtitles running in parallel. Both sides speak naturally. Both sides understand.

Paid per minute. No subscriptions. No hidden fees. 85% of every session goes to the Expert.

---

## How it works

### The three-sided flow

**Asker** signs up, tops up CLIP tokens (1000 CLIP = $10 USD flat), browses verified Experts by domain, books a session. During the call they see subtitles in their language. After the session they can publish the recording into the Knowledge Repository for other askers to find.

**Expert** submits credentials for review (degrees, certifications, licences), passes Stripe Identity verification, connects a bank account via Stripe Connect, sets their own per-minute CLIP rate. Sessions are taken live, earnings hit their wallet, cashout on demand. Pro tier cashes to real money. Scholar tier keeps Teaching Credits on-platform for academics.

**Platform** takes 15%. Handles escrow, verification, dispute resolution, translation pipeline, Stripe Connect orchestration.

![Browse Experts](screenshots/experts.png)
*Browse Experts. Per-minute rate visible. Verification tier on every card.*

---

## The translation pipeline

Two parallel layers. Voice and text run side by side with a small intentional buffer so the dubbed audio catches up cleanly.

**Voice layer.** The Expert's voice is cloned and re-synthesised into the asker's target language. Not a robotic read — the Expert's own vocal character, speaking the asker's language.

**Text layer.** Spoken dialogue is transcribed and machine-translated into the same 100+ languages as live subtitles. Both sides see them in real time.

**Post-session.** The full translated recording is regenerated from the complete transcript with higher-quality translation and re-dubbed cleanly, replacing the live version in the session record.

![Translation pipeline](screenshots/how-it-works.png)
*Voice + text layers run in parallel during every session.*

---

## Verification and trust

No follower-count-as-credential nonsense. ClipTips verifies the actual documents.

- **Stripe Identity** for every user. One passport, one account. Kills the bot-army and sock-puppet-review problem at the door.
- **Credential review** for every Expert. Degrees, professional licences, certifications — all reviewed by admin, permanently attached to the profile.
- **Gold Verified** tier for deeper trust. Optional one-time payment triggers a full background + credential audit. On approval, the badge lands on the public profile. Rejection is honest (refunded minus processing fees, no badge). Previously-approved Experts don't lose the badge if a later re-application is declined.

---

## The Knowledge Nexus

Every knowledge domain on the platform is rendered as an orbiting sphere on a live 3D starmap. Size scales with session activity. Click a domain to filter Experts. The taxonomy is expert-proposed and admin-reviewed so it stays clean as the platform grows.

![Knowledge Nexus](screenshots/nexus.png)
*141 domains seeded. Every sphere is a speciality with live Expert counts.*

---

## The Knowledge Repository

Post-session, the asker can choose to publish the full translated recording into the Knowledge Repository. Future askers searching the same question find the recording before they book a new session. The original Expert earns a passing bounty every time someone views the published answer. Translation runs automatically so a recording asked in English becomes a searchable Korean answer for a Korean viewer.

The marketplace gets better every time a session closes.

---

## Stack

Next.js 15 (App Router) · TypeScript · Supabase (Postgres + Realtime + Storage, RLS everywhere) · Clerk (auth) · Stripe + Stripe Connect Express + Stripe Identity · Jitsi Meet (live video, mid-migration to Daily.co) · HeyGen (voice clone + dubbing pipeline) · Resend (transactional email) · Vercel · Tailwind 4 · React Three Fiber for the Knowledge Nexus 3D map

---

## Status

**Live and end-to-end verified in pre-launch testing.** The platform is deployed. The translation pipeline works. The Stripe Connect flow is operational. The admin tools are complete. What's left is inviting the first real Expert cohort and running the first paid sessions with real users.

Launch is queued behind the first round of closed sessions landing cleanly.

---

## Links

- **Live app:** [cliptips-mvp.vercel.app](https://cliptips-mvp.vercel.app)
- **Project write-up:** [streamables.live/projects/cliptips.html](https://streamables.live/projects/cliptips.html)
- **Build log:** [How I Built ClipTips with Claude Code](https://streamables.live/articles/28-how-i-built-cliptips-with-claude-code.html)
- **Creator:** [Cameron J. Moir](https://github.com/C-Moir) · [@camjmoir](https://x.com/camjmoir)
- **Studio:** [Streamables.live](https://streamables.live)

---

## On the source code

The source code for ClipTips is kept in a private repository. The screenshots, write-ups, live app, and build log show what it is and how it was built. If you're evaluating the product, the live app is the canonical artefact.

Interested in partnering on the launch, becoming an early Expert, or exploring a white-label deployment? [Get in touch](https://streamables.live/#contact).

---

*Built solo in Brisbane. Claude Code is the IDE.*
