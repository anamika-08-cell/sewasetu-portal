# Build for Bharat Fellowship 2027 — Engineering take-home

## Your appointment

You have been appointed Digital Fellow in the Department of Social Welfare, Government of
Purvanchal. The **Sewa Setu Old Age Pension Portal** is live. Real citizens depend on it.
The vendor who built it is gone. The Deputy Commissioner of Sonapur district has written
recorded a short briefing for you (`dc-briefing.mp3`) — listen to it first; it is where the
citizens' complaints come from.

This is not a toy project with bugs sprinkled in. It is a small but complete inherited
system: code, a production database of ~100,000 citizens, and six months of server logs.
Your job is what a public technologist does in their first month: get it running, find out
what is actually wrong, fix what matters most, and explain your choices.

## About AI

Use whatever AI tools you like. We use them too. We are not interested in whether you wrote
every line yourself; we are interested in your judgement. Commit your agent configuration and
prompts; you will be asked what your tools got wrong.

## What you receive

A download containing: the application code, `docker-compose.yml` (app + Postgres + a fake
SMS gateway whose console is served at `/__gateway/`), `seed/seed.sql` (the citizens), the
log archive (a `.tar.gz` in `logs/` — extract it), the DC's recorded briefing
(`dc-briefing.mp3`), and this brief.
`docker compose up --build` brings up the full system with its data.

## What you must do

1. **Deploy it** on your own VM or VPS, with the database restored. No domain needed.
2. **Investigate.** The DC's briefing gives you hints on what might be going on — start there,
   then explore the code and the data.
3. **Fix what matters.** Fix as many things as you like — but your reply to the DC (recorded
   as a Loom) must name your **top 5 fixes ranked by citizen impact, with reasons**, and their
   order matters. Each fix needs a test that fails before the fix and passes after it,
   committed in that order.
4. **Do not delete or alter existing citizen records** except where a fix requires it.
   This is production data. Treat the people in it accordingly.
5. **Keep it running.** Your deployment must stay up from the moment you submit until we email
   you that the assessment is complete (up to ~30 days).

## What you submit (in the application form)

- **Deployed public URL.** (Our automated assessor completes test applications against it. The
  SMS gateway is served through your app at `/__gateway/`, so keeping your app reachable is all
  we need — there is no separate gateway URL or port to expose.)
- **Repository — give us both:**
  1. a *private* GitHub repo URL with full commit history (do not squash); invite `harshnisar`
     as a read-only collaborator (accepted automatically within minutes); **and**
  2. a **zip of your repo including the `.git` folder**, so we have your full history even if the
     invite fails. You may exclude the large files we gave you (`seed/seed.sql` and the log
     archive) — we only need your code and its history, not our data.
- **Assessor credentials:** a working admin login for our assessor. You may rebuild the
  citizen experience however you like, but **keep the admin panel functional** — it is how we
  verify your fixes. (If you rotated the admin credentials, hand over the new ones — like you
  would to an auditor.)
- **A Loom to the DC (face + screen, 3 min max):** what the evidence showed, your top 5 fixes
  ranked by citizen impact with reasons, and what you chose *not* to do and why.

## How you will be assessed

An automated probe exercises your live deployment — it may run at any time after you submit,
possibly more than once. **Everything you claim must be true at your URL.** This is a test of
engineering, not of guessing what we check, so here is exactly what the probe does:

- **Liveness** — is the app up and serving.
- **Security** — attempts the things an attacker would: reading other citizens' data,
  injection on inputs, default/leaked credentials, acting as staff without authority.
- **Data integrity** — submits an application (marked with a probe token) with an
  Indian-language name and reads it back; checks that records are stored faithfully.
- **Citizen journeys** — simulates confused and non-ideal users completing the form, and
  reads the error messages they are shown.
- **Load** — replays a month-end traffic spike and measures whether the service survives.
- **Repository** — clones your repo and checks commit history, that tests fail before a fix
  and pass after, and that the deployment matches the code.
- **The data** — logs in as citizens who existed before you arrived and checks their records
  are correct now.

We are not scoring visual polish, feature count, or how many tools you installed. More
fixes are not better fixes.

## Ground rules

- Do not attack any infrastructure other than your own deployment.
- If something outside your control breaks, tell us at the time, not afterwards. How you
  handle it is part of what we are looking at.
