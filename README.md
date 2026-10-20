# Hospital Appointment API

A TypeScript + Prisma 7 CRUD module for patients, doctors, and hospital appointments backed by PostgreSQL.

## Requirements

- Node.js 20+
- PostgreSQL
- npm

## Setup

1. Create a local database named `hospital_api`.
2. Run the DDL in `sql/schema.sql` against that database.
3. Copy `.env.example` to `.env` and set `DATABASE_URL` for your PostgreSQL credentials.
4. Install and generate the Prisma client:

   ```bash
   npm install
   npx prisma generate
   ```

The generated client is written to `generated/prisma` and is ignored by Git.

## Commands

```bash
npm run db:pull       # Introspect the existing database schema
npm run generate      # Generate Prisma Client
npm run db:seed       # Insert two doctors, two patients, and two appointments
npm run test:crud     # Exercise CRUD and relational queries
npm run typecheck     # TypeScript type check
```

The cleaned `prisma/schema.prisma` is checked in. `@map` and `@@map` map idiomatic Prisma names to the existing PostgreSQL column and table names; they do not alter the database.

## Implemented operations

- Patients: create, read one, search by name, update phone, delete.
- Doctors: create, read one, list by specialty, delete with a clear message for foreign-key restriction.
- Appointments: book using `connect` and return nested patient/doctor data, fetch full appointment, upcoming doctor schedule, set status, cancel all scheduled patient appointments, delete.
- Seed and end-to-end CRUD test scripts.

## Notes

- Patient deletion cascades to appointments as configured in the database.
- Doctor deletion is restricted while appointments reference that doctor.
- Do not commit `.env`; only `.env.example` belongs in version control.
- The CRUD test script requires a reachable PostgreSQL database with the tables from `sql/schema.sql`.
