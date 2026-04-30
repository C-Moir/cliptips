# ClipTips

**Live video marketplace with real-time AI translation.**
Book a verified expert by the minute, ask your question on camera, hear the answer in your own language — in their cloned voice.

[![Status](https://img.shields.io/badge/status-live%20interpreter%20GA-22c55e?style=flat-square)](https://cliptips-mvp.vercel.app)
[![Next.js](https://img.shields.io/badge/Next.js-15-000000?style=flat-square&logo=next.js)](https://nextjs.org)
[![TypeScript](https://img.shields.io/badge/TypeScript-5-3178c6?style=flat-square&logo=typescript&logoColor=white)](https://typescriptlang.org)
[![Supabase](https://img.shields.io/badge/Supabase-Postgres-3ecf8e?style=flat-square&logo=supabase&logoColor=white)](https://supabase.com)
[![Stripe Connect](https://img.shields.io/badge/Stripe-Connect-635bff?style=flat-square&logo=stripe&logoColor=white)](https://stripe.com/connect)

![ClipTips landing](screenshots/hero.png)
*100+ languages. 75% creator payout. $10 per 1000 CLIP. 40+ knowledge domains. The Knowledge Map renders every domain as a sphere — click any to filter Experts.*

## What is this

The person who can answer your question exists somewhere in the world. They just don't speak your language.

ClipTips closes that gap. An Italian tiler, a Japanese pastry chef, a Queensland lawyer, a Brazilian surgeon — anyone with verifiable expertise can take live video sessions from askers worldwide, in any of 100+ languages. Voice is cloned and re-dubbed into the asker's language with subtitles running in parallel. Both sides speak naturally. Both sides understand.

Paid per minute. No subscriptions. No hidden fees. **75% of every session goes to the Expert.**

---

## How it works

### The three-sided flow

**Asker** signs up, tops up CLIP tokens (1000 CLIP = $10 USD flat), browses verified Experts by domain, books a session. During the call they see subtitles in their language and hear the Expert in their own cloned voice. After the session they can publish the recording into the Knowledge Repository for other askers to find.

**Expert** submits credentials for review (degrees, certifications, licences), passes Stripe Identity verification, connects a bank account via Stripe Connect, sets their own per-minute CLIP rate. Sessions are taken live, earnings hit their wallet, cashout on demand. **Pro tier** cashes to real money. **Scholar tier** keeps Teaching Credits on-platform for academics.

**Platform** takes 25%. Handles escrow, verification, dispute resolution, the translation pipeline (Deepgram + ElevenLabs + OpenRouter API costs), Stripe Connect orchestration.

![Browse Experts](screenshots/experts.png)
*Browse Experts. Per-minute rate visible. Verification tiers (Gold Verified, Pro, Scholar) on every card. Trust score sits next to the avatar — calculated from identity verification, credentials, completed sessions, ratings, and Gold subscription.*

---

## Live Interpreter Mode

**Voice-cloned, real-time cross-language conversation in production.**

Speaker A talks in English. Speaker B hears A's actual cloned voice — not a synth — speaking Vietnamese (or any of 100+ languages), with live captions running in parallel. End-to-end latency ~250-400ms thanks to Deepgram Flux streaming transcription + ElevenLabs Flash v2.5 voice synthesis. That's "feels truly conversational" territory.

Bookable as an opt-in toggle on any session. A modest premium covers the per-minute Deepgram + ElevenLabs + translation API costs; Experts still receive their normal effective rate from the platform's slice. The platform absorbs the AI cost so Experts never see it.

**Coming next: lipsync.** The speaker's video output gets mouth-region modified to match the translated audio so cross-language sessions stop feeling like dubbed foreign films. Built on MuseTalk (MIT-licensed Tencent 2024 model). Free-tier infrastructure shipped 2026-04-29 — face baseline capture, utterance recording, lipsync UI scaffolding all live in production. The streaming-lipsync provider integration is the only remaining piece, gated on lipsync-API budget.

---

## The translation pipeline

Two layers run in parallel during every session.

**Voice layer.** The Expert's voice is cloned (ElevenLabs Multilingual / Flash v2.5 with cloning) and re-synthesised into the asker's target language. Not a robotic read — the Expert's own vocal character, speaking the asker's language.

**Text layer.** Spoken dialogue is transcribed (Deepgram Flux nova-3 streaming) and machine-translated (OpenRouter / Anthropic models) into 100+ languages as live captions. Both sides see them in real time.

**Post-session.** The full translated recording is regenerated from the complete transcript with higher-fidelity translation and re-dubbed cleanly, replacing the live version in the session record.

![Translation showcase — AI draft + native speaker correction loop](screenshots/translation-showcase.png)
*The translation engine doesn't just MT-and-pray. AI proposes the textbook draft. Native speakers (here, Marco from Rome) correct it — "we say 'come si deve', not 'autentica'. That's textbook Italian — nobody says that." The corrected phrasing improves 23,000+ Italian cooking translations globally. Every native correction compounds across the whole platform.*

---

## Verification and trust

No follower-count-as-credential nonsense. ClipTips verifies the actual documents.

- **Stripe Identity** for every user. One passport, one account. Kills the bot-army and sock-puppet-review problem at the door.
- **Credential review** for every Expert. Degrees, professional licences, certifications — all reviewed by admin, permanently attached to the profile.
- **Gold Verified** tier for deeper trust. $99/year subscription triggers a full background + credential audit. On approval, the gold badge lands on the public profile + 5 lifetime credential uploads included. Rejection is honest (refunded minus processing fees, no badge). Previously-approved Experts don't lose the badge if a later re-application is declined.
- **Trust scores** are computed live from identity verification, credentials, completed sessions, rating averages, Gold subscription status, and profile completeness — visible on every Expert card.

---

## The Knowledge Nexus

Every knowledge domain on the platform is rendered as an orbiting sphere on a live 3D starmap. Size scales with session activity. Click a domain to filter Experts. The taxonomy is expert-proposed and admin-reviewed so it stays clean as the platform grows.

![Knowledge Nexus](screenshots/nexus.png)
*Live 3D map: 655 knowledge domains as orbiting spheres. WebGL via React Three Fiber on desktop, procedural SVG fallback on mobile. Domains are shaped + coloured by category, sized by activity. Click any sphere to drop into that domain's Expert list.*

---

## Simple pricing — pay for what you use

![Pricing page](screenshots/pricing.png)
*1000 CLIP = $10 USD flat. Tokens never expire. Three top-up packages — Starter / Standard (10% off) / Pro (20% off). Per-minute billing — when you end the session, billing stops immediately.*

No subscriptions. No monthly fees. Cross-language sessions add a small premium that funds the AI translation pipeline — Experts always receive their full effective rate from the platform's 25% slice.

---

## How a session unfolds

![How it works — full session flow](screenshots/how-it-works.png)
*Find the right Expert → top up CLIP → connect via live video → AI dubs the conversation in real time → recording optionally publishes to the Knowledge Repository. The Expert teaches in their language; you follow in yours.*

---

## The Knowledge Repository

Post-session, the asker can choose to publish the full translated recording into the Knowledge Repository. Future askers searching the same question find the recording before they book a new session. The original Expert earns a passing bounty every time someone views the published answer. Translation runs automatically so a recording asked in English becomes a searchable Korean answer for a Korean viewer.

The marketplace gets better every time a session closes.

---

## Stack

Next.js 15 (App Router) · TypeScript · Supabase (Postgres + Realtime + Storage, RLS everywhere) · Clerk (auth) · Stripe + Stripe Connect Express + Stripe Identity · Daily.co + Jitsi Meet (live video, provider-abstracted) · ElevenLabs (voice cloning + Multilingual v2 + Flash v2.5 streaming TTS) · Deepgram Flux (streaming transcription, sub-300ms latency) · OpenRouter / Anthropic / DeepL (LLM translation, provider-abstracted) · MuseTalk (lipsync, V1.5) · Resend (transactional email) · Vercel · Tailwind 4 · React Three Fiber for the Knowledge Nexus 3D map

Vendor-portable by design. Video, translation, transcription, voice cloning, streaming TTS, and lipsync each sit behind a small provider interface so a single vendor outage or price hike never takes the platform offline.

---

## Status

**Live and end-to-end verified in pre-launch testing.** The platform is deployed. Translation pipeline works. Stripe Connect flow is operational. Admin tools are complete.

**Live Interpreter Mode is GA in production as of 2026-04-29.** Voice-cloned cross-language conversation runs at ~250-400ms end-to-end on real sessions. Premium pricing wired into the booking flow. Per-utterance recording infrastructure live, populating a private corpus of cross-language conversation pairs from every session — a competitive data asset that compounds with every paid session.

**V1.5 video lipsync is the next milestone.** Free-tier infrastructure shipped (face baseline capture, utterance recording, lipsync UI scaffolding). The streaming-lipsync provider integration is the only remaining piece — ~half a day of work when API budget exists.

Launch is queued behind the first round of closed sessions landing cleanly with real Experts.

---

## Links

- **Live app:** [cliptips-mvp.vercel.app](https://cliptips-mvp.vercel.app)
- **Browse Experts (live):** [cliptips-mvp.vercel.app/experts](https://cliptips-mvp.vercel.app/experts)
- **Knowledge Nexus (live):** [cliptips-mvp.vercel.app/nexus](https://cliptips-mvp.vercel.app/nexus)
- **Project write-up:** [streamables.live/projects/cliptips.html](https://streamables.live/projects/cliptips.html)
- **Build log:** [How I Built ClipTips with Claude Code](https://streamables.live/articles/28-how-i-built-cliptips-with-claude-code.html)
- **Creator:** [Cameron J. Moir](https://github.com/C-Moir) · [@camjmoir](https://x.com/camjmoir)
- **Studio:** [Streamables.live](https://streamables.live)

---

## On the source code

The source code for ClipTips is kept in a private repository. The screenshots, write-ups, live app, and build log show what it is and how it was built. If you're evaluating the product, the live app is the canonical artefact.

Interested in partnering on the launch, becoming an early Expert, or exploring a white-label deployment? [Get in touch](https://streamables.live/#contact).

---

*Built solo in Brisbane. Claude Code is the IDE. Screenshots captured 2026-04-30 from the live production deployment.*
