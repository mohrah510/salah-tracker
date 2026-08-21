# Project: Salah Tracker (working title)

## 1. Problem Statement
A personal prayer (salah) tracking app that helps a Muslim user log their five daily
prayers, see accurate prayer times for their location, and track consistency over
time via streaks and history — without relying on a third-party app that doesn't
fit their workflow.

## 2. Target User (v1)
Single-user, authenticated. No social/sharing features. Built for personal use,
architected the way a multi-user product would be (proper auth, per-user data
isolation) even though v1 doesn't expose social features.

## 3. In Scope (Project 1)
- User registration/login (JWT-based auth)
- Fetch daily prayer times for the user's location (via Aladhan API)
- Log each of the 5 daily prayers as: on-time / late / made-up / missed
- View prayer history (calendar or list view)
- Streak calculation (current streak, longest streak)
- Basic stats (weekly/monthly completion rate)
- Timezone-aware date handling

## 4. Explicitly Out of Scope (deferred to Project 1.5+)
- Masjid locator (geospatial search, maps)
- Push notifications / reminders
- Social features (sharing streaks, groups, leaderboards)
- Multiple calculation method support beyond a single default (revisit later)
- Mobile app (web-only for v1)
- CI/CD, caching layer, message queues, secondary database (Mongo) — all deferred
  to 1.5 as incremental production-hardening additions on top of a working v1

## 5. The "Hard Feature" (core technical challenge)
Streak and history logic:
- Correctly determining daily completion status across 5 prayers
- Timezone-correct day boundaries (a prayer logged at 11:58pm shouldn't break
  a streak due to a server/UTC mismatch)
- Handling missed vs. made-up prayers without breaking streak logic
- Efficient aggregation queries for stats (not recalculating from scratch on
  every request if avoidable)

## 6. Tech Stack
- Backend: Java, Spring Boot, Spring Data JPA, Spring Security (JWT)
- Database: PostgreSQL
- Frontend: React, TypeScript, Vite
- External API: Aladhan (prayer times)
- Testing: JUnit + Mockito (backend), Vitest/RTL (frontend, added later)
- Deployment: Render/Railway (backend + DB), Vercel/Netlify (frontend)

## 7. Success Criteria for v1
- Deployed, live URL, usable by an actual account (not just localhost)
- User can register, log in, see today's prayer times, log all 5 prayers,
  view history, and see a correct current/longest streak
- Core backend logic covered by tests
- Clean git history reflecting real, incremental feature branches — not one
  giant commit
