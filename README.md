# Lingo

A Duolingo-style language learning web application built with Next.js 14. Supports structured courses with units, lessons, and interactive challenges — including a hearts system, XP progression, quests, leaderboard, and a shop.

Built for developers who want a production-ready, full-stack learning app as a reference or starting point.

---

## Features

- Interactive lessons with SELECT and ASSIST challenge types
- Hearts system with the ability to replenish via practice or shop
- XP / points system with quest milestones
- Leaderboard across all users
- Pro subscription tier (unlimited hearts) via Stripe
- Shop to exchange points for hearts
- Exit confirmation and out-of-hearts modals
- Admin dashboard (React Admin) for managing courses, units, lessons, and challenges
- Sound effects for correct / incorrect answers
- Landing page for unauthenticated users
- Mobile-responsive layout

---

## Tech Stack

| Layer        | Technology                              |
|--------------|-----------------------------------------|
| Framework    | Next.js 14 (App Router, Server Actions) |
| Language     | TypeScript                              |
| Auth         | Clerk                                   |
| Database     | NeonDB (PostgreSQL)                     |
| ORM          | Drizzle ORM                             |
| Payments     | Stripe                                  |
| UI           | Shadcn UI, Radix UI, Tailwind CSS       |
| State        | Zustand                                 |
| Admin        | React Admin                             |
| Deployment   | Vercel                                  |

---

## Getting Started

### Prerequisites

- Node.js 18+
- A [NeonDB](https://neon.tech) PostgreSQL database
- A [Clerk](https://clerk.com) application
- A [Stripe](https://stripe.com) account (for payments)

### Install

```bash
git clone https://github.com/JumboMiller/Language-Learning-App.git
cd Language-Learning-App
npm install
```

### Environment Variables

Create a `.env` file in the project root:

| Variable                          | Description                                 |
|-----------------------------------|---------------------------------------------|
| `DATABASE_URL`                    | NeonDB PostgreSQL connection string         |
| `NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY` | Clerk publishable key                     |
| `CLERK_SECRET_KEY`                | Clerk secret key                            |
| `STRIPE_API_KEY`                  | Stripe secret key                           |
| `STRIPE_WEBHOOK_SECRET`           | Stripe webhook signing secret               |
| `NEXT_PUBLIC_APP_URL`             | Public base URL (e.g. `http://localhost:3000`) |

### Database Setup

Push the schema to your database and seed initial data:

```bash
npm run db:push
npm run db:seed
```

### Run Locally

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000).

---

## Usage

Once running:

- `/` — Landing page (public)
- `/courses` — Select a language course
- `/learn` — Active lesson map
- `/leaderboard` — Rankings
- `/quests` — XP milestones
- `/shop` — Exchange points for hearts
- `/admin` — Admin dashboard (manage content)

### Admin Dashboard

The admin panel at `/admin` uses React Admin to manage courses, units, lessons, challenges, and challenge options directly via the REST API.

---

## Project Structure

```
app/
  (marketing)/        # Landing page (public routes)
  (main)/             # Authenticated app shell
    courses/          # Course selection
    learn/            # Lesson map
    leaderboard/
    quests/
    shop/
  admin/              # React Admin dashboard
  api/                # REST API routes (used by admin)
  lesson/             # Active lesson / quiz UI

components/           # Shared UI components
db/
  schema.ts           # Drizzle ORM table definitions
  queries.ts          # Server-side data access functions
lib/                  # Utility functions
scripts/              # DB management scripts
store/                # Zustand modal state
```

---

## Scripts

| Script         | Description                                  |
|----------------|----------------------------------------------|
| `npm run dev`      | Start development server                 |
| `npm run build`    | Production build                         |
| `npm run start`    | Start production server                  |
| `npm run lint`     | Run ESLint                               |
| `npm run db:push`  | Push Drizzle schema to database          |
| `npm run db:seed`  | Seed database with initial course data   |
| `npm run db:prod`  | Run production seed script               |
| `npm run db:reset` | Reset database                           |
| `npm run db:studio`| Open Drizzle Studio (DB browser UI)      |

---

## Configuration

- **Middleware** (`middleware.ts`): All routes are protected by Clerk auth by default. Only `/` and `/api/webhooks/stripe` are public.
- **Drizzle** (`drizzle.config.ts`): Schema is defined in `db/schema.ts`. Run `db:push` after any schema change.
- **Stripe Webhooks**: Configure your Stripe webhook to point to `<NEXT_PUBLIC_APP_URL>/api/webhooks/stripe`.

---

## Deployment

This app is designed to deploy on [Vercel](https://vercel.com).

1. Push to GitHub and import the repo in Vercel.
2. Set all environment variables in the Vercel project settings.
3. Run `npm run db:push` and `npm run db:seed` against your production database once.
4. Configure the Stripe webhook endpoint to your production URL.

---

## License

This project is open source. See [LICENSE](LICENSE) for details.
