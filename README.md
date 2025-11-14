# Prisma Commands | Prisma Workflow — step‑by‑step

A Practical Prisma Workflow Step by Step | Prisma ORM | Prisma All Commands
---

## Prerequisite: Install Prisma and Prisma Client

```bash
npm install prisma --save-dev
npm install @prisma/client
```

Installs the Prisma CLI and the Prisma Client library. The client is required for your app code to query the database.

---

## 1. Initialize Prisma in your project

```bash
npx prisma init
```

Creates the `prisma/` folder, a starter `schema.prisma`, and a `.env` template. Run this once when you first add Prisma to a project.

---
## 2. Edit `schema.prisma`

Open `prisma/schema.prisma` and define your `model` types, datasource (database connection), and generator (Prisma Client).

No command here — this is where you design your DB blueprint.

---

## 3. Generate Prisma Client

```bash
npx prisma generate
```

Generates (or regenerates) the Prisma Client JS/TS library used by your app to query the database. Run after changing `schema.prisma` or after installing/updating Prisma packages.

---

## 4. Create & apply a migration (development)

```bash
npx prisma migrate dev --name <descriptive-name>
```

**What it does:** compares `schema.prisma` with the current DB, creates a migration SQL file under `prisma/migrations/`, and applies it to your development database.

**When to use:** local development while building schema changes. The first migration is commonly named `init`. Like `npx prisma migrate dev --name init`

---

## 5. Seed the database (optional but common)

Add a seed script to `package.json`, for example:

```json
{
  "prisma": {
    "seed": "ts-node prisma/seed.ts"
  }
}
```

Then run:

```bash
npx prisma db seed
```

Seeds populate tables with initial or test data. Useful after a fresh migration or in CI for integration tests.

---

## 6. Inspect / work with the DB via GUI

```bash
npx prisma studio
```

Opens Prisma Studio — a lightweight UI to browse and edit data in your development DB.

---

## 7. Syncing an existing database (introspection)

```bash
npx prisma db pull
```

Reads the schema from an existing DB and updates `schema.prisma` (useful when adopting Prisma for an existing project).

---
