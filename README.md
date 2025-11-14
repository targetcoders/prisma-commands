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
