# Prisma Commands | Prisma Workflow 

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

## 8. Force-sync schema without migration files

```bash
npx prisma db push
```

Writes the `schema.prisma` to the DB directly **without** creating migration files. Handy for prototyping but **not** recommended for production workflows where migration history is important.

---

## 9. Reset your development DB

```bash
npx prisma migrate reset
```

Drops all data, re-applies all migrations, and (optionally) runs the seed script. Useful to get a clean local DB.

---

## 10. Production: apply existing migrations

```bash
npx prisma migrate deploy
```

Applies the already-committed migrations to the target (staging/production) database. **Does not** create new migrations. This command is what your CI/CD or deployment scripts should run.

---

## 11. Generate a SQL diff (advanced)

```bash
npx prisma migrate diff --from-schema-datamodel prisma/schema.prisma --to-schema-datamodel other_schema.prisma --script
```

Creates a SQL diff between two schemas or between a schema and a live DB. Useful for advanced auditing or custom migration pipelines.

---

## 12. Best practices (short)

- **Always commit** `prisma/migrations/` to version control. Migrations are your schema history.
- Run `prisma generate` as part of your build step so the Prisma Client is up-to-date.
- Use `migrate dev` in development, `migrate deploy` in production. Avoid `db push` in production.
- Add `prisma db seed` to CI if tests require seeded data.
- Backup production DB before running migrations and test migrations in staging first.

---
