<div align="center">

# 🦸 Community Hero

### Hyperlocal Civic Issue Reporting & Autonomous Triage Platform

**Vibe2Ship Hackathon — Solo Submission by Nandan Kabra**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
![Built with Gemini](https://img.shields.io/badge/AI-Gemini%202.5%20Flash-4285F4)
![Platform](https://img.shields.io/badge/Built%20on-Google%20AI%20Studio-orange)
![Status](https://img.shields.io/badge/status-active-success)

[Live Demo](https://community-hero-462930236954.us-west1.run.app) · [Report Bug](https://github.com/n-a-n-d-a-n/community-hero/issues) · [Request Feature](https://github.com/n-a-n-d-a-n/community-hero/issues)

</div>

---

## Table of Contents

- [Problem Statement](#problem-statement-ps2-community-hero)
- [Solution Overview](#solution-overview)
- [Key Features](#key-features)
- [Tech Stack](#tech-stack)
- [Architecture](#architecture)
- [Google Technology Usage](#google-technology-usage)
- [Impact](#impact)
- [Live Demo](#live-demo)
- [License](#license)
- [Author](#author)

---

## Problem Statement (PS2: Community Hero)

Civic issues — potholes, garbage accumulation, broken streetlights, waterlogging, damaged signage — go unreported or under-reported because the process is tedious: citizens don't know who to contact, duplicate complaints flood municipal systems with no deduplication, and there's no visibility into whether anything is actually being done. Issues sit unresolved for weeks with no accountability loop.

## Solution Overview

Community Hero turns issue reporting into a one-tap action and replaces a static complaint form with an **autonomous AI triage pipeline**. A citizen photographs a problem, and from that single photo the system classifies it, checks for duplicates, routes it to the correct department, tracks it through resolution, and — without any human intervention — escalates it automatically if it breaches its SLA window.

The core differentiator is that this isn't a chatbot wrapper. It's a multi-stage agentic pipeline where each stage hands structured state to the next.

## Architecture

```
Photo Upload → Vision Classification Agent → Deduplication Agent
   → Auto-Routing → Status Tracking → Autonomous SLA Escalation Agent
```

| Stage | Responsibility |
|---|---|
| Vision Classification | Gemini 2.5 Flash multimodal call → category, severity, description, department |
| Deduplication | Haversine-based proximity check (100m radius) + Gemini semantic match (50m) |
| Auto-Routing | Ticket routed to responsible department on creation |
| Status Tracking | Milestone timeline — Reported → Acknowledged → In Progress → Resolved |
| SLA Escalation | Background agent flags SLA breaches and drafts escalation notes autonomously |

## Key Features

- **AI Photo Triage** — Citizen uploads a photo + GPS location; Gemini 2.5 Flash classifies category, severity, generates a description, and assigns the responsible municipal department — all in one multimodal call.
- **Deduplication Agent** — Before creating a new ticket, the system checks existing reports within 100m using the Haversine formula. If a same-category issue exists within 50m, Gemini confirms semantic duplication; matched reports are merged via upvote instead of creating redundant tickets — keeping the database clean.
- **Auto-Routing & Status Timeline** — Every report is automatically routed to its department on creation, with a full milestone history (Reported → Acknowledged → In Progress → Resolved) visible per ticket.
- **Autonomous SLA Escalation Agent** — A background agent continuously monitors open tickets against severity-based SLA thresholds (Critical: 24h, High: 3 days, Medium: 7 days, Low: 14 days). Breaching tickets are auto-flagged and Gemini generates a professional escalation note addressed to the relevant department — with zero human prompting.
- **Map + Feed Views** — Severity-color-coded map pins (Leaflet/OpenStreetMap) and a searchable, filterable community feed.
- **Admin Dashboard** — Municipal-side view to track and resolve tickets by priority, with live stats (Total Reports, Critical Open, Escalated, Resolved Today).
- **Community Upvoting** — Citizens reinforce existing reports rather than duplicating them, surfacing real community priority signals.

## Tech Stack

| Layer | Technology |
|---|---|
| AI / Core Engine | **Google Gemini 2.5 Flash** (multimodal) via `@google/genai` SDK |
| Build Platform | **Google AI Studio** (built and deployed) |
| Frontend | React + TypeScript, Leaflet/OpenStreetMap for mapping |
| Backend | Express (`server.ts`) — secure server-side proxy for Gemini calls |
| Persistence | Browser local storage (demo-scope; designed for DB migration) |
| Geolocation | Browser Geolocation API |
| Deployment | Google Cloud Run |

## Google Technology Usage

Gemini 2.5 Flash is used as the reasoning engine for **three distinct agent roles** in the same app — not a single classification call:

1. **Vision triage** — image → category/severity/department (multimodal input)
2. **Semantic deduplication** — comparing two natural-language descriptions for real-world equivalence
3. **Autonomous escalation writing** — generating contextual, policy-toned text without human drafting

All Gemini calls are routed through a secure Express backend, so API keys are never exposed client-side. The entire application was built and deployed using Google AI Studio, satisfying the core platform requirement.

## Impact

Community Hero reduces the friction of civic reporting to a single photo, eliminates duplicate complaint noise that overwhelms municipal systems, and — critically — removes the dependency on a human dispatcher to notice when a ticket has gone stale. The escalation agent means issues don't silently disappear into a queue; the system actively re-surfaces them until resolved.

## Live Demo

🔗 **[community-hero-462930236954.us-west1.run.app](https://community-hero-462930236954.us-west1.run.app)**

## License

Distributed under the MIT License. See [`LICENSE`](LICENSE) for details.

## Author

**Nandan Kabra**
- GitHub: [@n-a-n-d-a-n](https://github.com/n-a-n-d-a-n)

---

<div align="center">

If this project interests you, consider giving it a ⭐

</div>
