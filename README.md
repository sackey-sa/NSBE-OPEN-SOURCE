# NSBE-OPEN-SOURCE
# Fatherhood Collective Platform

A web application for [The Fatherhood Collective](#about-the-client), a nonprofit providing parenting and family resources to fathers through 12-week courses. Built and maintained by student engineers from NSBE, SHPE, and ColorStack.

> **Project status:** Early planning (pre-Sprint 1). Sections marked *planned* describe intended structure and will be updated as the code is written.

## Table of contents

- [About the client](#about-the-client)
- [Project goals](#project-goals)
- [V1 scope](#v1-scope)
- [Tech stack](#tech-stack)
- [Getting started](#getting-started)
- [Project structure](#project-structure)
- [How we work](#how-we-work)
- [Privacy and security](#privacy-and-security)
- [Team](#team)
- [Maintenance and handoff](#maintenance-and-handoff)

## About the client

The Fatherhood Collective is a nonprofit that provides parenting and family resources to fathers of all ages through courses and classes. Participants either sign up for courses or are assigned to them, and some assignments are court-mandated. Each course runs 12 weeks across 12 modules. Today, the mandated-course process runs on paper, so part of this project is replacing paper steps with digital ones that still satisfy the courts, agencies, or funders who rely on those records.

## Project goals

1. Help participants see which courses they're enrolled in and how far along they are.
2. Help staff enroll participants and track completion without paper forms.
3. Give the student team real full-stack experience building and maintaining a system that real people depend on.

We are committed to maintaining this application for at least one year after launch.

## V1 scope

Features are confirmed with the client before they are built. See the project board for current status.

**Core**
- Participant and staff login with role-based access
- Course dashboard showing enrolled and assigned courses
- Progress tracking across the 12 modules, with a progress bar
- Staff view to enroll or assign participants and see completion

**Planned, pending confirmation**
- Calendar support through standard `.ics` files and subscription links, compatible with Google, Apple, and Yahoo calendars
- Digital proof of attendance or completion, replacing paper sign-in sheets and completion letters (format depends on what courts or agencies require)

**Paper-to-digital approach**
- Understand each paper step first, then produce an equivalent before trying to improve on it
- Run in parallel with paper during the pilot so no participant loses credit if the app has a problem
- Design for low tech comfort: phone-first, simple screens, and staff able to enter information on a participant's behalf

**Deliberately deferred**
- Live two-way sync with external calendar providers
- Storing probation, provider, or court-date information in the application

## Tech stack

*Provisional. Final choices are recorded in `docs/decisions.md`.*

| Layer | Choice |
|---|---|
| Backend | Python with FastAPI |
| ORM and database | SQLAlchemy with a relational database (PostgreSQL or MySQL, to be decided) |
| Frontend | React |
| Authentication | Managed auth service (to be decided) |
| Hosting | To be decided, prioritizing low cost and low maintenance |

The frontend and backend are separate programs that communicate through an API. Each feature starts with an agreed contract describing the requests and responses, so both sides can be built in parallel. FastAPI generates interactive API documentation automatically, available at `/docs` when the backend is running.

## Getting started

*Planned. These commands assume the standard layout below and will be verified once the project is scaffolded.*

### Prerequisites

- Python 3.11 or newer
- Node.js 20 or newer
- A local database (see `docs/setup.md` once available)
- Git

### Backend

```bash
cd backend
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
cp .env.example .env             # then fill in your own values
uvicorn app.main:app --reload
```

The API runs at `http://localhost:8000`, with documentation at `http://localhost:8000/docs`.

### Frontend

```bash
cd frontend
npm install
cp .env.example .env             # then fill in your own values
npm run dev
```

### Environment variables

Real secrets are never committed. Each of `backend/` and `frontend/` has a `.env.example` listing the variable names with no values. Copy it to `.env` and fill in your own. `.env` is listed in `.gitignore`.

## Project structure

*Planned.*

```
.
├── backend/
│   ├── app/
│   │   ├── main.py          # FastAPI entry point
│   │   ├── routers/         # API endpoints, grouped by feature
│   │   ├── models/          # Database models
│   │   ├── schemas/         # Request and response shapes (the contract)
│   │   └── services/        # Business logic
│   ├── tests/
│   ├── requirements.txt
│   └── .env.example
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   ├── pages/
│   │   └── api/             # Calls to the backend
│   ├── package.json
│   └── .env.example
├── docs/
│   ├── decisions.md         # Decision log
│   ├── setup.md             # Detailed setup guide
│   └── admin-guide.md       # For client staff
└── README.md
```

## How we work

We use an agile process with two-week sprints. All work is tracked on the GitHub Projects board with the columns Backlog, This Sprint, In Progress, In Review, and Done.

### Workflow

1. Pick a card from **This Sprint**. Every card has exactly one owner.
2. Create a branch from `main`: `feature/short-description` or `fix/short-description`.
3. Commit in small steps with clear messages.
4. Open a pull request that references the issue (for example, `Closes #12`) so the board updates automatically.
5. Another team member reviews it. The author does not merge their own work without review.
6. Someone other than the author tests it.
7. Merge to `main`.

### Definition of done

- Works on both phone and computer screens
- Code reviewed by another team member
- Tested by someone other than the author
- Documentation updated
- Deployed or ready to demo

### Vertical slices

Each person owns a whole feature from database to screen, with agreed API contracts written first. Pair stronger and newer developers on each slice so knowledge spreads.

### Decisions

Meaningful technical and product decisions are recorded with the date and reasoning in `docs/decisions.md`.

## Privacy and security

Some participants have court or probation obligations, so this application is handled with extra care.

- Collect only the data we need. Do not store probation, provider, or court-date details.
- Use a managed service for authentication. Never write our own password handling.
- Enforce role-based access. A participant can only see their own records.
- Serve everything over HTTPS.
- Never commit secrets, credentials, or real participant data. Use fake data for development and testing.
- Validate all input on the backend, regardless of what the frontend does.
- Keep backups and document how to restore them.
- Report any suspected security problem to the project lead right away.

The team is not providing legal advice. The client should confirm any legal or contractual data requirements, and we will seek guidance before launch.

## Team

Student engineers from NSBE, SHPE, and ColorStack. Everyone writes code, reviews code, and contributes to documentation.

## Maintenance and handoff

The team is committed to maintaining this application for at least one year. To keep that realistic as members graduate or change roles:

- The domain, hosting, and service accounts are owned by the client, with team members as administrators.
- Documentation is kept current, including setup, deployment, and an admin guide for staff.
- Decisions are logged so new members understand why things are built the way they are.
- New members are onboarded through pairing on a real task.

## License

To be decided with the client before launch.