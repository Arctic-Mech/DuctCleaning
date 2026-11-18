# Arctic Duct Cleaning

iPhone-first web app for Arctic's duct cleaning field inspections. Live at
**https://arctic-mech.github.io/DuctCleaning/** (served from `index.html` on `main`).

## What it does
- **Jobs**: name, number, optional address.
- **Plans**: upload a PDF and name it. A multi-page PDF becomes one plan per page.
  **Replace PDF (keep tags)** swaps in a clean copy of the same drawing without moving any pins.
- **Reports**: tap the plan to drop an auto-numbered pin. Each report has type
  (Supply / Return / Exhaust / Other), status, re-visit time frame, serviced equipment,
  inspected area, and before/after photos. Reports can also be opened from the job screen.
- **Quick / HD**: the field view uses a fast preview image; the **HD** button renders the
  on-screen area from the PDF at full resolution.
- **Markup** (internal planning, web view only, never exported):
  - **Exhaust** and **Cleaning access** markers with an optional note, access door size,
    and quantity. The job screen totals every access door needed by size.
  - **Draw**: pen (pressure-sensitive with Apple Pencil), highlighter, eraser, colors,
    sizes, undo. With a Pencil, the Pencil draws and fingers move the plan.
- **Export**: one interactive PDF. Each plan is a full-resolution vector page with numbered
  pins, and tapping a pin jumps to that report's page.

## Data: Firebase Firestore only (no auth, no billing)
Everything saves to the `duct-cleaning-cb58f` Firestore database and syncs across devices.
Firebase Storage is not used, so the project stays on the free Spark plan.

| Collection  | Holds |
|-------------|-------|
| `jobs`, `drawings`, `reports` | Core records (loaded at startup) |
| `photos`    | One compressed photo per document (~1280px), loaded when a report opens |
| `pdfchunks` | Plan PDFs as base64 chunks under the 1 MiB/document limit, shared across a PDF's pages |
| `markers`   | Exhaust / cleaning-access markers, door size and quantity (loaded at startup) |
| `strokes`   | One freehand markup stroke per document, loaded when a plan opens |

### One-time setup
Because there is no login, the Firestore rules must allow open access:
Firebase console → **Firestore Database → Rules** → paste `firebase/firestore.rules` → **Publish**.

> ⚠️ Open rules make the database world-readable and world-writable. Anyone with the URL
> can read or change everything. Add Firebase Auth later if you need to lock it down.

### Free-tier limits and offloading
Spark gives **1 GiB storage** and **50K reads / 20K writes / 20K deletes per day**. When a
job is finished, export the PDF, file it, then **delete the job** (job menu → Delete job).
That removes its plans, PDFs, reports, photos, markers and drawings and frees the space.

## Development
`index.html` is a single self-contained file. Push to `main` and GitHub Pages redeploys in
about a minute.
