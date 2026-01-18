## Project name

[![Node.js](https://img.shields.io/badge/node-22.14.0-339933?logo=node.js&logoColor=white)](./.nvmrc)
[![Astro](https://img.shields.io/badge/astro-5-BC52EE?logo=astro&logoColor=white)](https://astro.build/)
[![React](https://img.shields.io/badge/react-19-149ECA?logo=react&logoColor=white)](https://react.dev/)
[![TypeScript](https://img.shields.io/badge/typescript-5-3178C6?logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![Tailwind CSS](https://img.shields.io/badge/tailwindcss-4-06B6D4?logo=tailwindcss&logoColor=white)](https://tailwindcss.com/)

**Foxite (MVP)** — a web app for airsoft (ASG) players to catalog replicas, track modifications, and monitor spending.

## Project description

Foxite is a web application designed for ASG (Airsoft) players to manage their replica arsenal, track modifications, and monitor spending on upgrades. It aims to replace fragmented tracking across spreadsheets, phone notes, and photo galleries with a single, centralized record per replica.

- **Primary target users**: ASG players
- **Languages**: Polish (primary) and English (secondary), planned from day 1
- **Key outcomes**: faster access to replica info, clear investment visibility, and a full change history of upgrades over time

### Table of contents

- [Project name](#project-name)
- [Project description](#project-description)
- [Tech stack](#tech-stack)
- [Getting started locally](#getting-started-locally)
- [Available scripts](#available-scripts)
- [Project scope](#project-scope)
- [Project status](#project-status)
- [License](#license)

### Product docs

- **PRD**: [`/.ai/foxite-prd.md`](.ai/foxite-prd.md)
- **Tech stack (design)**: [`/.ai/tech-stack.md`](.ai/tech-stack.md)

## Tech stack

Based on the PRD and `/.ai/tech-stack.md`, the MVP is intended to use:

- **Frontend**
  - **Astro 5** (server-rendered / content-focused pages)
  - **React 19** for interactive components
  - **TypeScript 5**
  - **Tailwind CSS 4**
  - **shadcn/ui** (Radix-based React components)
- **Backend**
  - **Supabase** (PostgreSQL database + Auth + SDK)
  - **Supabase Storage** for replica images
- **AI (planned)**
  - **OpenRouter** (`openrouter.ai`) as a gateway to multiple LLM providers/models
- **CI/CD & hosting (planned)**
  - **GitHub Actions** for CI/CD pipelines
  - **DigitalOcean** for hosting (Docker image)
- **Dev tooling (in this repo)**
  - **ESLint** + **Prettier**
  - **Husky** + **lint-staged** (pre-commit formatting/linting)

## Getting started locally

### Prerequisites

- **Node.js**: `22.14.0` (see [`.nvmrc`](.nvmrc))
- **npm**: comes with Node.js

### Setup

1. Install dependencies:

```bash
npm install
```

2. (If applicable) Create an environment file:
   - If `.env.example` exists, copy it to `.env` and fill in values.
   - Note: Supabase (Auth/DB/Storage) is part of the MVP requirements and will require Supabase project configuration and environment variables once wired into the app.

3. Start the dev server:

```bash
npm run dev
```

4. Build and preview production output:

```bash
npm run build
npm run preview
```

## Available scripts

From [`package.json`](package.json):

- **`npm run dev`**: start Astro dev server
- **`npm run build`**: production build
- **`npm run preview`**: preview the production build locally
- **`npm run astro`**: run the Astro CLI
- **`npm run lint`**: run ESLint across the repo
- **`npm run lint:fix`**: run ESLint and auto-fix issues where possible
- **`npm run format`**: format the repo using Prettier

## Project scope

The MVP scope is defined in the PRD (`/.ai/foxite-prd.md`).

### In scope (MVP)

- **Auth & profile**
  - Email/password registration and login
  - Email verification
  - Private profile (nickname, city, language preference)
- **Replica management**
  - Replica CRUD (soft-delete)
  - Replica fields including photos, status/reason, ROF, Joules, BB weight, round counter
  - Cost summary (purchase price and total modifications cost shown separately)
- **Modification management**
  - Modifications CRUD linked to replicas (soft-delete)
  - Predefined categories (final list TBD during implementation)
- **Round counter**
  - Per-replica counter with quick-add buttons: +10, +100, +1000, +2000
- **Power conversion**
  - Convert Joules to **FPS (0.2g equivalent)** on the fly (not stored)
  - Formula: \(FPS = \sqrt{2 \times Joules / 0.0002} \times 3.28084\)
- **Images**
  - Upload to Supabase Storage with **client-side compression**
  - Note: the PRD currently contains **inconsistent limits** (e.g. 3 vs 5 photos; 10MB vs 2MB file size). This should be resolved during implementation.
- **Security & data model**
  - Row Level Security (RLS) from day 1
  - Soft-delete pattern for all entities
  - Complete change history/audit trail for replicas and modifications
- **Internationalization**
  - Polish + English UI (including currency sign change in EN, per PRD)

### Out of scope (MVP)

- **AI features** (OCR receipts, auto-categorization, photo recognition, chatbot, recommendations)
- **Mobile/PWA** (native apps, push notifications, advanced device integrations)
- **Social/team/community features** (public profiles, sharing, squads, chat, gamification)
- **Events/locations** (maps, calendars, registrations)
- **Commerce/marketplace** (listings, payments, shop/service integrations)
- **Advanced arsenal & tracking** (compatibility DB, auto-upgrade suggestions, predictions, charts, integrations)
- **Other** (OAuth providers like Google, data export, advanced search/filters, SEO/thumbnail generation)

## Project status

- **PRD status**: Planning complete (last updated January 2026)
- **Repo state**: Early MVP implementation (current package version: `0.0.1`)
- **Open questions (from PRD)**: category list finalization, onboarding flow, error/validation UX, session management details, and language switching UX
- **MVP success metrics (qualitative, from PRD)**: personal utility (2+ weeks of regular use), team adoption (3+ teammates return to the app), and feature-demand feedback

## License

**MIT**. See [`LICENSE`](LICENSE).
