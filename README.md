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

  Items show as a free column layout you arrange yourself: each cell has the checkbox, the name, who
  checked it and when, and status badges (**To order**, **Ordered**, **Overdue**, **Due**). In
  **Edit list** you drag items between columns (grip handle) — columns can hold different numbers of
  items, and dropping at the end starts a new column. Tapping an item opens an editor
  with a **Need to order new / more** toggle (a shopping-list flag, counted in the summary) plus the
  Replacement-ordered, tracking and replace-by options. **Edit list** adds items (type or paste a
  list), reorders them by dragging the handle, and can uncheck everything for a fresh check. Changes
  show up live on every phone.
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
- **Estimate** (low-key link in the home top bar): a measuring takeoff tool. Create an estimate
  (number + job name), upload drawings, then **set a scale** (tap two points and type the real
  length). **Measure run**: tap along a duct run following its bends (one tap at each turn is enough,
  even for a run across the whole sheet). On a CAD (vector) drawing two taps are enough — one at
  the start and one at the end, near the middle of the duct: the app finds the duct's own path between
  them through its elbows, offsets and dampers (if it can't, it says so; add a tap at each turn). The app then measures straight across the duct every 2 pt
  along the line, finds the duct's walls (long lines running alongside it, so tags, crossing walls,
  boxes and ducts drawn over it are looked past, and stretches where the walls are hidden take the
  size on either side), centers your line on the duct, and reads every size along it — a reducer in
  the middle of a segment splits into its sizes, each with its own width factor. Linear feet and
  area follow from that. Dashed/grid lines and lines drawn over the duct are not taken for its
  walls. When the PDF is a vector drawing (CAD output), the walls are read from the PDF's own lines,
  so positions are exact, and at each bend the app traces the fitting's own walls line by line
  (radius or mitered elbows and angled offsets alike), so the band's outline is the fitting's exact
  shape, the line runs along the midline between its walls and the area is the duct's own; square
  elbows and tees stay square. Reducers and other places where a wall steps in or out (a wider
  section, a box edge drawn just inside the wall) are traced the same way, so the band follows each
  taper line exactly, and through inline equipment (a silencer or VAV box between two sizes) it follows
  each box's stepped outline. When a building wall or another duct is drawn just inside a duct's wall,
  the pair of lines drawn as that duct's walls (they start and end together) is used. A branch that
  starts on its main ignores the stretch inside the main while finding its own walls. Tap a run and choose **Edit area (paint / erase)** to fix the area by hand anywhere the
  drawing is ambiguous (the brush starts from the measured band); the painted outline becomes the
  run's sq ft while the drawn line stays its linear footage, and **Reset area to measured** undoes it. The line you drew shows as a crisp centerline with end dots (your linear measurement)
  and the detected width as a translucent band out to the bold lines (the area); width can be
  overridden by hand. Runs are colored by duct type — medium-pressure supply orange, low-pressure
  supply yellow, return green, exhaust purple — chosen while measuring or in the run sheet, with a
  legend on the plan. Pinch, the zoom buttons, or the mouse wheel / trackpad zoom around the cursor.
  Per-run and per-estimate totals (linear ft / sq ft), counted as a union so the same run — or an
  overlapping branch tie-in — is never double-counted. Each run you start is **auto-labeled by duct
  type** (LPS 1, LPS 2, RET 1…) and can be renamed in its editor. A run is a group: its **branches**
  snap to the main (no tie-in dot) and belong to it. Hitting **Fill** asks what you're measuring —
  **start a new run** (choose the duct type) or **add fill to an existing run** — so a fill can begin
  a measurement or attach to a run you've already started; the fill takes that run's color and counts
  under it. **Fill** is a paint-bucket: tap inside an enclosed duct and it floods the area to the
  surrounding lines for the **square footage**; all of a run's pours render as one flat translucent
  shade (no darker overlaps, no borders), blending with the plan. For **linear footage** you then tap
  **Measure line** and lay down a continuous line — tap the start, any bends, then the end — which is
  exactly your line (no auto-guessing). You establish the main by measuring it first, then add taps as
  their own fills. Filling each duct separately also lets you measure ducts stacked on each other.
  When a wall or grid line crosses a duct and cuts it into pieces, tap each piece into the same run: the pieces
  are recognized as one duct (they share a full-width cut), measured across together for the duct width, and
  each piece's linear footage is its area ÷ that width, so cut elbows read their true size and length.
  Open a fill from its run editor to **Edit fill area** — Paint to add or Erase to remove, with an
  adjustable brush size — to fine-tune the square footage.
  Deleting a run segment offers **Delete this branch/fill** or **Delete
  the whole run** (the main with all its branches and fills). **Undo** (button in the measure bar, or
  Ctrl/⌘-Z) removes the most recent run or fill. A **branch load** accounts for branches being slower
  to clean than a straight run: Standards holds a flat *hours per branch*, toggled **On/Off** per
  estimate. When on, it folds into the hrs-by-lf and hrs-by-sf totals and also shows as its own
  "Branches (N)" figure on the estimate card.
  **Labor factors** (Standards): a multiplier per duct type (MPS / LPS / Return / Exhaust, e.g. Return ×1.05,
  supply ×0.98) and width rules ("wider than 24″ ×1.10", "narrower than 8″ ×1.15") applied to each piece's
  measured width (rounded to ½″). Factors multiply hrs by lf and hrs by sf; access doors use raw footage. A **Standards** screen sets hours per linear foot, hours per square foot, and one
  access door every N feet; because crews price labor two ways, each estimate shows **hours by lf**
  and **hours by sf** side by side (not summed) plus access doors — pick whichever your crew prices
  by. Estimating is desktop/laptop oriented (mouse wheel zooms); the drawing renders at high
  resolution for sharp zooming.
  **Standards tabs**: **Cleaning**, **Install** and **Shop fab** each have their own hours per lf,
  hours per sf, hours per branch, duct-type multipliers and **width-band multipliers** (under 6″,
  6–10″, 10–14″, 14–20″, 20–28″, 28–40″, 40″+), applied to each measured piece. **Display** picks
  which figures the estimate card shows (cleaning lf/sf, branches, access doors, install lf/sf, shop
  fab lf/sf, the branch switch, the factors line, notes, actual hours); install and fab are off until
  you turn them on.
  **Actual hours / fine-tune**: after a job, enter the hours it actually took (cleaning, install,
  shop fab) on the estimate and tick **Use this job to fine-tune**. Every checked job feeds one fit of
  every multiplier — rate, duct type, width bands and hours per branch — and with **Tune estimates
  automatically** (on by default) every estimate uses the tuned numbers right away ("tuned from N jobs"
  on the card). Your own numbers on the Cleaning / Install / Shop fab tabs stay as the starting point:
  the fit is always pulled toward them, never toward its own last answer, so jobs never count twice
  and each job checked off gives the real results more say (one job mostly moves the rate; a width
  band or duct type follows the jobs once enough of them have that size or type). A job that ran far
  over or under (more than ~35%) pulls no harder than that. The **Fine-tune** tab shows, per kind of
  labor, the jobs and lf behind it, the average miss with your numbers vs. tuned, the **expected miss
  on the next job** (each job estimated from the other jobs only; needs 3+ jobs), what lf backs each
  multiplier, and each job's miss. With automatic tuning off, estimates use your numbers and a button
  copies the tuned numbers into them.
- **Export**: choose what the PDF includes — **Reports**, **Markups**, or **Both**.
  - *Reports*: each plan is a full-resolution vector page with numbered pins; tapping a pin jumps to
    that report's page.
  - *Markups*: each plan page shows the exhaust / cleaning-access / note tags and freehand drawings.
  - *Both*: report pins and markups on the same plan pages, with report pages following.
  The source plan's own embedded annotations (e.g. old Bluebeam markups) are stripped for a clean export.
  When a job has more than one plan, a per-plan picker chooses which pages to include.
  When markups are included, a **Markups to show** selector picks the tag types (exhaust / access /
  notes) and freehand drawings to draw. The **Export** button is on the job screen whenever the job
  has at least one plan.

Browser/OS **Back** and the edge-swipe-back gesture (Safari, desktop, and when saved to the Home
Screen) step back one screen in the app — closing an open sheet first — instead of leaving the app.

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
| `estimates` | Estimate takeoffs: number + job name, actual hours and the fine-tune flag |
| `estdrawings` | Estimate drawings (PDF per page) with their scale calibration |
| `estruns` | Measured duct runs: centerline points, detected/entered width |

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
