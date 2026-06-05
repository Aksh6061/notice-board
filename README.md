# Notice Board — Reno Platforms Internship Assignment

A full-stack Notice Board application built with Next.js (Pages Router), Prisma, and a hosted MySQL database. Supports creating, reading, updating, and deleting notices with server-side validation, urgent-first ordering, and a responsive UI.

---

## Live Demo

> Add your Vercel URL here after deploying

---

## Tech Stack

| Layer | Choice |
|---|---|
| Framework | Next.js 14 — Pages Router |
| Database ORM | Prisma |
| Database | TiDB Cloud (free, MySQL-compatible) |
| Hosting | Vercel (Hobby) |
| Styling | CSS Modules + custom design system |

---

## Running Locally

### 1. Clone the repo

```bash
git clone https://github.com/YOUR_USERNAME/notice-board.git
cd notice-board
```

### 2. Install dependencies

```bash
npm install
```

### 3. Set up the database

Create a free MySQL-compatible database on [TiDB Cloud](https://tidbcloud.com) (recommended), [Neon](https://neon.tech), or [Supabase](https://supabase.com).

Copy the environment file and fill in your connection string:

```bash
cp .env.example .env.local
```

Edit `.env.local`:

```
DATABASE_URL="mysql://user:password@host:port/noticeboard?sslaccept=strict"
```

> If using Neon or Supabase (Postgres), change `provider = "mysql"` to `provider = "postgresql"` in `prisma/schema.prisma`.

### 4. Push the schema to your database

```bash
npx prisma db push
```

### 5. Start the dev server

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000).

---

## Deploying to Vercel

1. Push your repo to GitHub (make sure it's **public**).
2. Import the repo at [vercel.com/new](https://vercel.com/new).
3. Add the `DATABASE_URL` environment variable in the Vercel project settings.
4. Deploy. Vercel will run `prisma generate` automatically via the `postinstall` script.

---

## API Routes

| Method | Route | Description |
|---|---|---|
| GET | `/api/notices` | List all notices (Urgent first, then by date) |
| POST | `/api/notices` | Create a new notice |
| GET | `/api/notices/:id` | Get a single notice |
| PUT | `/api/notices/:id` | Update a notice |
| DELETE | `/api/notices/:id` | Delete a notice |

All mutating routes validate input on the server and return `422` with field-level error messages on validation failure.

---

## What I Would Improve with More Time

**Image uploads via Cloudinary or Vercel Blob.** Currently the image field accepts a URL, which works but isn't ideal. With more time I'd add a proper file upload input that stores images in object storage and saves only the URL in the database — making it genuinely self-contained.

---

## AI Usage

Claude (Anthropic) was used to generate the initial project scaffolding — the full file structure, API routes, component code, and CSS. The Prisma schema and Next.js Pages Router architecture were designed based on the assignment spec. All code was reviewed for correctness; the server-side validation logic, Prisma `orderBy` for Urgent-first sorting, and the confirmation-before-delete flow were verified to match the requirements exactly.
