# Arctic Duct Cleaning

iPhone-first web app for Arctic's duct cleaning field inspections. Live at
**https://arctic-mech.github.io/DuctCleaning/** (served from `index.html` on `main`).

## What it does
- **Truck checklist** (top of the home screen, collapsed until you tap the summary): a shared list
  of what should be in the truck. The **box** checks an item off and stamps the person's name and
  the time. **Tapping the item** opens its editor:
  - **Replacement ordered** (with the order date and who marked it). Checking the item off later
    clears it.
  - **Track when it's replaced** (on automatically for anything named "filter"): log replacements
    for today or a past date, see "Replaced Oct 3 · 46 days ago", and keep a history.
  - **Needs replacing**: a replace-by date, optionally repeating every 1–12 months from the last
    replacement. Due within two weeks shows orange; overdue shows red and in the summary.
  - Rename or remove the item.

  **Edit list** adds items (type or paste a list), reorders them by dragging the handle, and can
  uncheck everything for a fresh check. Changes show up live on every phone.
- **Jobs**: name, number, optional address.
- **Plans**: upload a PDF and name it. A multi-page PDF becomes one plan per page.
  **Replace PDF (keep tags)** swaps in a clean copy of the same drawing without moving any pins.
- **Reports**: tap the plan to drop an auto-numbered pin. Each report has type
  (Supply / Return / Exhaust / Other), status, re-visit time frame, serviced equipment,
  inspected area, and before/after photos. Reports can also be opened from the job screen.
- **Quick / HD**: the field view uses a fast preview image; the **HD** button renders the
  on-screen area from the PDF at full resolution.
- **Markup** (internal planning, web view only, never exported):
  - **Exhaust**, **Cleaning access** and **Note** tags. Access/exhaust take an optional
    note, door size and quantity. Switch what you're placing from the placing bar.
  - **Draw**: pen (pressure-sensitive with Apple Pencil), highlighter, eraser, lasso
    select/move, colors, sizes, undo. Two fingers pan and zoom.
  - **People and groups**: you give your first and last name once per device (the same
    name is the same account). Markups record who made them and go into your active group
    (e.g. Precon vs Actual). Show/hide by group or by person; with more than one set
    showing, each set is drawn in its own color.
  - Tag numbers close up after a delete (delete 24 and 25 becomes 24).
- **Job lists**: reports, cleaning access tags, exhaust tags, notes, and access doors needed
  (filterable by group, copyable).
- **Export**: choose what the PDF includes — **Reports**, **Markups**, or **Both**.
  - *Reports*: each plan is a full-resolution vector page with numbered pins; tapping a pin jumps to
    that report's page.
  - *Markups*: each plan page shows the exhaust / cleaning-access / note tags and freehand drawings.
  - *Both*: report pins and markups on the same plan pages, with report pages following.
  The source plan's own embedded annotations (e.g. old Bluebeam markups) are stripped for a clean export.

## Data: Firebase Firestore only (no auth, no billing)
Everything saves to the `duct-cleaning-cb58f` Firestore database and syncs across devices.
Firebase Storage is not used, so the project stays on the free Spark plan.

| Collection  | Holds |
|-------------|-------|
| `jobs`, `drawings`, `reports` | Core records (loaded at startup) |
| `photos`    | One compressed photo per document (~1280px), loaded when a report opens |
| `pdfchunks` | Plan PDFs as base64 chunks under the 1 MiB/document limit, shared across a PDF's pages |
| `markers`   | Exhaust / cleaning-access / note tags with author and group (loaded at startup) |
| `strokes`   | One freehand markup stroke per document, with author and group, loaded when a plan opens |
| `users`     | People, keyed by name (`u_first_last`) |
| `mkgroups`  | Markup groups, owned by a person, with their set color |
| `checklist` | Truck checklist items: who checked each one and when, replacement order, replacement history and replace-by date |

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
