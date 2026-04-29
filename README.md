# ClipTips

**Live video marketplace with real-time AI translation.**
Book a verified expert by the minute, ask your question on camera, hear the answer in your own language — in their cloned voice.

[![Status](https://img.shields.io/badge/status-live%20interpreter%20GA-22c55e?style=flat-square)](https://cliptips-mvp.vercel.app)
[![Next.js](https://img.shields.io/badge/Next.js-15-000000?style=flat-square&logo=next.js)](https://nextjs.org)
[![TypeScript](https://img.shields.io/badge/TypeScript-5-3178c6?style=flat-square&logo=typescript&logoColor=white)](https://typescriptlang.org)
[![Supabase](https://img.shields.io/badge/Supabase-Postgres-3ecf8e?style=flat-square&logo=supabase&logoColor=white)](https://supabase.com)
[![Stripe Connect](https://img.shields.io/badge/Stripe-Connect-635bff?style=flat-square&logo=stripe&logoColor=white)](https://stripe.com/connect)

![ClipTips landing](screenshots/hero.png)

## What is this

The person who can answer your question exists somewhere in the world. They just don't speak your language.

ClipTips closes that gap. An Italian tiler, a Japanese pastry chef, a Queensland lawyer, a Brazilian surgeon — anyone with verifiable expertise can take live video sessions from askers worldwide, in any of 100+ languages. Voice is cloned and re-dubbed into the asker's language with subtitles running in parallel. Both sides speak naturally. Both sides understand.

Paid per minute. No subscriptions. No hidden fees. 75% of every session goes to the Expert.

---

## How it works

### The three-sided flow

**Asker** signs up, tops up CLIP tokens (1000 CLIP = $10 USD flat), browses verified Experts by domain, books a session. During the call they see subtitles in their language and hear the Expert in their own cloned voice. After the session they can publish the recording into the Knowledge Repository for other askers to find.

**Expert** submits credentials for review (degrees, certifications, licences), passes Stripe Identity verification, connects a bank account via Stripe Connect, sets their own per-minute CLIP rate. Sessions are taken live, earnings hit their wallet, cashout on demand. Pro tier cashes to real money. Scholar tier keeps Teaching Credits on-platform for academics.

**Platform** takes 25%. Handles escrow, verification, dispute resolution, the translation pipeline (Deepgram + ElevenLabs + OpenRouter API costs), Stripe Connect orchestration.

![Browse Experts](screenshots/experts.png)
*Browse Experts. Per-minute rate visible. Verification tier on every card.*

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

Next.js 15 (App Router) · TypeScript · Supabase (Postgres + Realtime + Storage, RLS everywhere) · Clerk (auth) · Stripe + Stripe Connect Express + Stripe Identity · Daily.co + Jitsi Meet (live video, provider-abstracted) · ElevenLabs (voice cloning + Multilingual v2 + Flash v2.5 streaming TTS) · Deepgram Flux (streaming transcription, sub-300ms latency) · OpenRouter / Anthropic / DeepL (LLM translation, provider-abstracted) · MuseTalk (lipsync, V1.5) · Resend (transactional email) · Vercel · Tailwind 4 · React Three Fiber for the Knowledge Nexus 3D map

Vendor-portable by design. Video, translation, transcription, voice cloning, streaming TTS, and lipsync each sit behind a small provider interface so a single vendor outage or price hike never takes the platform offline.

---

## Status

**Live and end-to-end verified in pre-launch testing.** The platform is deployed. Translation pipeline works. Stripe Connect flow is operational. Admin tools are complete.

**Live Interpreter Mode is GA in production as of 2026-04-29.** Voice-cloned cross-language conversation runs at ~250-400ms end-to-end on real sessions. Premium pricing wired into the booking flow. Per-utterance recording infrastructure live, populating a private corpus of cross-language conversation pairs from every session.

**V1.5 video lipsync is the next milestone.** Free-tier infrastructure shipped (face baseline capture, utterance recording, lipsync UI scaffolding). The streaming-lipsync provider integration is the only remaining piece — ~half a day of work when API budget exists.

Launch is queued behind the first round of closed sessions landing cleanly with real Experts.

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
