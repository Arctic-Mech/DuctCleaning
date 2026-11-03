# DuctPro Field — Arctic Mechanical Duct Cleaning

iPhone-first web app for duct cleaning field inspections. Live at
**https://arctic-mech.github.io/DuctCleaning/** (served from `index.html` on `main`).

## What it does
- Start a **job** (name, number, optional address)
- Add **plans** (floor/area) by uploading a PDF — you name each one before it saves
- **Place reports** by tapping a spot on the plan; a numbered pin drops there
- Each report: name, type, status, assignee, recommended re-visit, serviced-equipment
  table, inspected area, and **before/after photos** (take with the camera or pick from library)
- **Report package** view assembles every plan + report to share

## Data — Firebase (no authentication)
All data saves to the `duct-cleaning-cb58f` Firebase project and syncs across devices.
- **Firestore** holds jobs, plans, and reports.
- **Storage** holds plan PDFs and photos.

### One-time setup (required)
Because there is no login, the security rules must allow open access:

1. **Firestore rules** — Firebase console → *Firestore Database* → *Rules* →
   paste `firebase/firestore.rules` → **Publish**.
2. **Storage rules** — Firebase console → *Storage* → *Rules* →
   paste `firebase/storage.rules` → **Publish**.

> ⚠️ These rules make the database world-readable and world-writable. Anyone with the
> URL can read or change everything. That matches the "no auth" requirement; add
> Firebase Auth later if you ever need to lock it down.

### Optional — sharpest plan zoom (CORS)
Plans always render from a high-res preview image. For *live* re-rendering straight from
the PDF at deep zoom, allow the site to fetch PDFs cross-origin:

```bash
gsutil cors set firebase/cors.json gs://duct-cleaning-cb58f.firebasestorage.app
```

Without this the app automatically falls back to the preview image, so it still works.

## Development
`index.html` is a single self-contained file. Edit and push to `main`; GitHub Pages
redeploys in ~30–60s.
