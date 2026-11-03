# DuctPro Field — Arctic Mechanical Duct Cleaning

iPhone-first web app for duct cleaning field inspections. Live at
**https://arctic-mech.github.io/DuctCleaning/** (served from `index.html` on `main`).

## What it does
- Start a **job** (name, number, optional address)
- Add **plans** (floor/area) by uploading a PDF — you name each one before it saves
- **Place reports** by tapping a spot on the plan; a numbered pin drops there
- Each report: name, type, status, assignee, recommended re-visit, serviced-equipment
  table, inspected area, and **before/after photos** (camera or library)
- **Report package** view assembles every plan + report; **Save / Print** makes a PDF

## Data — Firebase Firestore only (no auth, no billing)
Everything saves to the `duct-cleaning-cb58f` **Firestore** database and syncs across
devices. **Firebase Storage is not used**, so the project stays on the free Spark plan
with no pay-as-you-go required.

- Jobs, plans, and reports are Firestore documents.
- Each **plan PDF is stored in Firestore** as base64 chunks (one collection, `pdfchunks`,
  each chunk under the 1 MiB-per-document limit). The viewer loads those chunks, rebuilds
  the PDF, and **renders only the on-screen area at device resolution on demand** — so a
  huge E-size vector sheet stays crisp at any zoom without storing giant images.
- A small preview image is kept on the plan for thumbnails, the instant base layer, and
  the export. Photos are compressed and stored inline, one per `photos` document (~1280px).

### One-time setup (required)
Because there is no login, the Firestore rules must allow open access:

1. Firebase console → **Firestore Database** → create the database if you haven't.
2. **Firestore Database → Rules** → paste `firebase/firestore.rules` → **Publish**.

> ⚠️ Open rules make the database world-readable and world-writable. Anyone with the URL
> can read or change everything. That matches the "no auth" requirement; add Firebase
> Auth later if you ever need to lock it down.

### Free-tier limits & the "offload when done" workflow
Spark free tier gives **1 GiB total storage** and **50K reads / 20K writes / 20K deletes
per day**. The app only loads photos when you open a report or the report package (not on
every launch), to stay well under the daily read cap.

When a job is finished: **Save / Print the report package to a PDF, file it, then delete
the job** in the app (job menu → Delete job). Deleting a job removes its plans, reports,
and every photo from Firestore, which frees that storage back up. Roughly ~2,000 photos
fit in 1 GiB, so offloading completed jobs keeps you comfortably inside the free tier.

## Development
`index.html` is a single self-contained file. Edit and push to `main`; GitHub Pages
redeploys in ~30–60s.
