# PROJECT_CONTEXT.md — AlHamd Online Academy (resume file)

Owner: Sir USama (MS Mathematics, Punjab). Languages: Roman Urdu + English.
Repo: `usagimarketer/alhamd-academy` (branch `main`) · Live: https://usagimarketer.github.io/alhamd-academy
Last updated: 2026-11-14 · Also see `NOTES.md` (running change log + TODO).

## 0. Latest changes (quick list, newest state)
- **UI/UX:** mobile speed optimised (no blur, solid white cards on mobile); home category cards are collapsible **accordions on all devices**; the **Sidebar is removed completely**; home cards match the top menu (Text Books, Notes, Pairing Schemes, Test Series, Past Papers, Results).
- **Features:** global **Search bar** on Home (searches Book titles + 9th–12th Class Notes; NOT Past Papers, no Enter key); **Paper Maker app deleted** (not just hidden) and replaced by a Top Nav dropdown: **Paid = WhatsApp link, Free = PaperDesk link**.
- **Pending:** real Google Drive links + cover images for the remaining books, and real Past Paper links (`PP_LINKS`, still `#` placeholders).

## 1. Project overview
- Single-file static site: **`index.html`** (plain HTML + CSS + JS, no frameworks), plus `images/` (`logo.jpg`, `9th-math-cover.jpg`, `10th-chemistry-cover.webp`), `NOTES.md`, `README.md`.
- Pages are `<section class="pg" id="p-...">`: `p-home`, `p-info`, `p-notes` (all Notes / Past Papers / Text Book pages render into `#nb`). `go(t)` switches pages.
- Design: **Light Frosted Glass** theme with **Royal Sapphire** accent (`--pr:#2563eb`, `--accent-light:#eff6ff`), blue hero gradient, soft blue background glow, glass cards. Light theme is forced in every mode. Home cards are compact **accordion tiles** in an auto-fill grid (the old Bento 2x2 span was removed on desktop; on mobile the first card spans 2 columns).
- Home = hero (logo, title, social buttons) → search bar → 6 category cards → footer. The Sidebar/Categories list was REMOVED (see below).

## 2. Completed features (current state)
- **Responsive layout**: desktop + mobile (`@media (max-width:768px)` blocks at the end of the CSS): sticky scrolling top menu, bottom nav removed, 44px touch targets, 2-col grids, compact hero (social buttons hidden on mobile), `html/body` overflow-x hidden, inputs 16px (iOS no-zoom).
- **Top menu (`NAV`)**: Text Books, Notes, Pairing Schemes, Test Series, Past Papers, Results, Paper Maker. Paper Maker dropdown (`PMF`): **Paid Service (WhatsApp)** → `https://wa.me/923040947667?text=...` (new tab); **Free Service** → `https://paperdesk.whisperperks.com/` (new tab).
- **Home cards (`SITE`)** in the same order as the top menu: Text Books, Notes, Pairing Schemes, Test Series, Past Papers, Results. Each is an **accordion** (`.hc2` + `.link-list` + `.toggle-icon`, `.expanded` class, click handler in `buildSite()`); links open the matching page. Icons come from the small `IC` object via `circ()` (keys: 📚 🎓 📝 📋 📑 📊 — a new card needs a new key here).
- **Search bar** (`#globalSearch`, `#searchResults`): the user's own document-level `input` listener. It searches **Text Book titles (BOOKS)** and the four "9th–12th Class Notes" names, min 2 characters, up to 8 hits. (There is NO Enter-key support and it does NOT search Past Papers — an earlier richer version exists in git commit `30dc509` if ever wanted.)
- **Past Papers** (`openPastPapers`, `renderPastPapersGrid`): clicking a subject inside "<class> Past Papers" is intercepted in `openNotes` and shows year tabs + a grid of boards, generated from `PP_YEARS = ['2026','2024','2023','2022','2021','2019','2018']` and `PP_BOARDS = ['BWP','LHR','SGD','GUJ','RWP','MTN','SWL','FBD','DGK']` for every class/subject (no per-paper objects). Real links go in **`PP_LINKS`** with key `'Class|Subject|Year|Board'` (e.g. `'9th|Urdu|2026|BWP'`); missing links show a dimmed card + toast "link jald add kiya jayega".
- **Text Books** (`openTextBooks` → class chooser → subject grid → `openBook(b)` detail page): cover, metadata, Read Online / Download PDF (Drive), related books, view/download counters in localStorage (per browser only). Data: **`BOOKS`** nested `BOOKS['<9th|10th|11th|12th> Text Book'][Subject] = {cls,title,cover,url,view,size,author,views,downloads,updated,year,session,rating,overview}`. Session is 2025-27. 10th has *Pakistan Studies* instead of Islamiat.
- **Notes browser** (`openNotes(p)`; data in **`NOTES`**): class → subject cards (rendered from `BOOKS['<class> Text Book']` subject keys, so they always match Text Books) → unit → exercise → question → Drive PDF preview. `NOTES['10th Class Notes']` has real data under key `'Mathematics'`. `INFO(name)()` opens any "<class> <kind>" page (Notes, Pairing, Test Series, Past Papers, Result).
- Other: hero social links (WhatsApp 923040947667, TikTok alhamd_online_academy, Instagram sirusamahanif, Facebook muhammadusamahanif1819, email alhamdonlineacademy30@gmail.com), SEO/og meta tags, lazy-loaded book covers, Google Fonts trimmed to Noto Nastaliq Urdu + Poppins + Inter.

## 3. Removed on purpose (do NOT bring back unless asked)
- **Paper Maker app is DELETED, not hidden** (all its sections, JS, access-code gate, MathJax, bottom nav, CSS; the file went from 147 KB to ~70 KB). Full old version: git commit `71ab0a4` (`git checkout 71ab0a4 -- index.html`). The old access code `AH-F7R9JN` and `paper-backup.json` are obsolete.
- **Sidebar / Categories list removed** (no `.sidebar`, `.cat-btn`, `.cat-sub`, `catData` any more).
- Neon/cyberpunk theme, glass-break click effect, Trending ticker (replaced by search), Smart Syllabus bar experiments.
- Consequence: **"Smart Syllabus Exam 2027" (9th and 11th Drive download links) existed only in the sidebar and is now gone from the site.** The links are in git history (commit `290bb0e`); re-add as a card/menu item if the owner wants it.

## 4. Pending tasks / what's next
1. Fill real **Google Drive links** (`url` + `view`) for the remaining Text Books in `BOOKS` (about 31 have empty links; the user is adding them manually; 9th/11th Math and 10th Chemistry etc. are done).
2. Add **cover images** to `images/` and set `cover:'./images/<name>.webp'` for all books (only 9th Math and 10th Chemistry have covers).
3. Fill **`PP_LINKS`** with real Past Paper links (everything is a `#` placeholder now).
4. Possibly re-add Smart Syllabus Exam 2027 (see section 3). Optional: global view/download counters (needs a backend), Free Service page.

## 5. CRITICAL RULES (always follow)
- Replies short; show only changed lines. **Never send zip files or whole HTML files.**
- Workflow every time: `git pull origin main` first → patch with exact string replacement → JS syntax check → Playwright test (desktop 1200px + mobile 390px, no JS errors, no horizontal overflow) → append a line to `NOTES.md` → commit with trailers `Co-Authored-By: Claude Sonnet 5.5 <noreply@anthropic.com>` and `Claude-Session: ...` → `git push origin HEAD` automatically → sync the Project doc (`project_write path=index.html`).
- **Do not use heavy `backdrop-filter` on mobile** (it causes lag): mobile blocks use `backdrop-filter:none` and solid `#ffffff` cards. Keep the hero and the coloured `.sub-card` tiles on their own colours (a white background would hide their white text).
- **Do not modify the Search logic** (the user's own `globalSearch` listener) unless explicitly asked.
- If a Paper Maker/print layout is ever rebuilt: `.paper` must stay white background + black text for printing (the old `.paper` CSS no longer exists in the file). LaTeX papers: A4, 0.8 cm margins, 12 pt, `\dfrac` never `\frac`.
- The user's handwritten notes/formulas must be used exactly as written. Do not invent data (leave blank / placeholder). If a pasted prompt has unfilled placeholders, ask once.
- Data on the live site (counters, saved items) is per-browser (localStorage) only.
- Pasted code from the user may be cut off or use class names that do not exist (e.g. `.link-btn`, `.top-nav`); check the real names in `index.html` first and tell the user what was adapted.
