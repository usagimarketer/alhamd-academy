# AlHamd Online Academy - Project Notes

> Naye Claude chat ya account mein sirf yeh file paste karein aur kahein:
> "Yeh mera project hai. Yahan se aage chalo." Phir jis file par kaam karna ho woh file paste karein.

Last updated: 2026-11-10

---

## 1. Project kya hai
Ek single-file website (HTML + CSS + JS, sab ek hi file mein) jo **AlHamd Online Academy** ki hai.
Is mein ek **Paper Maker** tool hai jis se MCQ aur long/short question papers print ke liye banaye jate hain.

- Hosting: **GitHub repo -> Netlify** (auto deploy, jab bhi push ho site update hoti hai)
- Koi framework ya build step nahi. Bas `index.html`.

## 2. Files

| File | Kaam |
|---|---|
| `index.html` | **Live website.** Netlify yehi serve karta hai. Paper Maker access code se locked. |
| `website-ARTIFACT-claude-link.html` | Claude link wali copy (Claude account se request/manzoori wala lock). |
| `website-standalone-no-lock.html` | Naya home page, bina kisi lock ke. |
| `paper-backup.json` | Paper data: 15 MCQs, logo, settings. App ke **Restore** se wapas aata hai. |
| `README.txt` | Backup ki purani ittela. |
| Fonts (`.ttf`) | Alag sambhale hue hain, repo mein nahi. |

Note: `index.html` aur `website-for-hosting-index.html` bilkul same file hain.

## 3. Website ka structure (`index.html`)
Har page ek `<section class="pg" id="p-...">` hai, `go('name')` function se badalta hai.

| Section id | Page |
|---|---|
| `p-home` | Home page (AlHamd Online Academy) |
| `p-paper` | Paper Maker (main tool) |
| `p-layout` | Layout / page settings |
| `p-gate` | Access code wali screen |
| `p-info` | Institute / info |
| `p-latex` | LaTeX compiler |
| `p-q1` | Questions editor |
| `p-prev` | Preview / print |

### Zaroori functions
- Navigation: `go`, `gateIt`
- Lock: `applyLock`, `renderGate`, `sha` (code ka SHA hash `CODE_HASH` se compare hota hai)
- Paper: `renderPaper`, `renderSecs`, `renderQ`, `addQ`, `addSec`, `printOnly`, `xpage`
- Data: `save` (localStorage key `pm2`), `norm`, `hydrate`, `loadSample`
- LaTeX: `lxCompile`, `lxSample`, `lxCopy`
- Fonts: `addFont`, `regFont`

### Bahar se kya load hota hai
- Google Fonts: Noto Nastaliq Urdu, Amiri, Noto Naskh Arabic, Carlito, Caladea, EB Garamond, Old Standard TT, Poppins
- MathJax 3.2.2 (cdnjs) math/LaTeX ke liye

## 4. Paper Maker ka data (`paper-backup.json`)
Keys: `lang, lx, secs, inst, logo, logoSize, layout, mcq, det, style, font, ufont, stu, q`

- `q` = MCQs ki list. Har item: `t` (sawal, LaTeX `$...$` chalta hai), `o` (4 options), `a` (sahi option ka index), `m` marks, `img`
- `inst` = institute name/campus/branch/address + unke font sizes
- `layout` = page size, orientation, margin, copies, border, watermark, font size, OMR, key waghera
- `secs` = long/short sections (heading, marks, attempt, items)
- `stu` = student details fields (name, roll, class, section)

## 5. Access code (lock)
- Paper Maker kholne ke liye code chahiye, baqi site sab dekh sakte hain.
- Code ka sirf **hash** `index.html` mein hai, code khud nahi.
- Browser mein unlock `localStorage` key `pm_unlock` mein yaad rehta hai.
- **Code yahan mat likhein, khaaskar agar repo public ho.**
- Yeh lock sirf client-side hai. "View Source" se kamzor ho sakta hai. Asal security nahi.
- Code kho jaye to Claude se naya code banwa kar `CODE_HASH` badal dein.

## 6. Deploy ka tareeqa
1. Change `index.html` mein karein
2. Local mein browser mein khol kar check karein
3. GitHub par commit + push
4. Netlify khud deploy kar dega (Deploys tab mein status dekhein)

Repo ka suggested layout:
```
/index.html          <- live site
/NOTES.md            <- yeh file
/backup/             <- baqi backups (private repo mein behtar)
```

## 7. Ab tak ka kaam (DONE)
- [x] Home page + Paper Maker bana
- [x] MCQ, long/short sections, LaTeX support
- [x] Urdu/English fonts, logo, institute header
- [x] Access code lock
- [x] 15 MCQs ka sample data
- [x] Backup v2 (2026-11-09)
- [x] GitHub Claude se connect (2026-11-10), ab Claude seedha repo mein push kar sakta hai
- [x] Upar wali brand patti (logo + naam + "Study with USama") hata di (2026-11-10). Hero banner mein logo/naam rehta hai
- [x] Hero banner ki neeche wali line ("Study with USama • Notes, Guess Papers...") hata di (2026-11-10)
- [x] Hero banner: logo 150px (mobile 110px) aur naam 48px (mobile 34px) bara kiya (2026-11-10)
- [x] Backup v3 (2026-11-10)
- [x] Hero banner se 6 quick-link buttons hata diye; ab social buttons (WhatsApp, TikTok, Instagram, Facebook, Contact) hain, asli links ke saath (2026-11-11)
- [x] "Guess Papers" ka naam "Test Series" kiya; "Punjab Notes" ka naam "Notes"; Test Series ka icon 📝 (2026-11-11)
- [x] Notes browser: class kholne par subject cards (rang wale boxes); khali section ka message (2026-11-11)
- [x] Home par Categories sidebar (accordion): hero upar poori width, neeche sidebar + content. Smart Syllabus Exam 2027 mein 9th aur 11th ke asli Drive links (2026-11-11)
- [x] 9th Class Pairing aur 9th Text Book ke subjects: Urdu, English, Mathematics, Islamiat, Physics, Chemistry, Biology, Computer, Tarjuma-tul-Quran (baqi classes mein Science/Pak Studies pehle jaise) (2026-11-12/13)
- [x] 9th Pairing > Mathematics: pairing scheme link naye tab mein (2026-11-12)
- [x] Punjab Text Books: "Choose Your Class" glass-style cards (9-12) (2026-11-12)
- [x] Textbook detail page (Mathematics, 9th-12th): English text, metadata grid, 5-star rating, Indigo Download button, Related Textbooks, Copyright card; session 2025-27 (2026-11-12)
- [x] 9th Mathematics: asli cover (`images/9th-math-cover.jpg`), Drive download + read-online links; Views/Downloads counters (sirf usi browser mein, localStorage) (2026-11-13)
- [x] Text Books: `BOOKS` ab nested (Class -> Subject -> book); 9th-12th ke 8 subjects (Mathematics, Physics, Chemistry, Biology, English, Urdu, Islamiat, Computer) ke detail pages; related books ab usi class ke doosre subjects (2026-11-13)
- [x] 10th Text Book: Islamiat ki jagah Pakistan Studies (grid aur `BOOKS` dono mein); 9th, 11th, 12th mein Islamiat (2026-11-13)
- [x] Home cards (Text Books, Notes, Test Series, Pairing Schemes, Past Papers, Paper Maker cards) ka Glassmorphism design: blur+saturate, rim-of-light, glassy link buttons, glassy Trending pill, background orbs; light aur dark dono mode (2026-11-13)
- [x] Logo base64 se `images/logo.jpg` mein shift (index.html halki); SEO + og tags (GitHub Pages URL `https://usagimarketer.github.io/alhamd-academy`); `word-break` fix (2026-11-13)

## 8. Aage ka kaam (TODO)
- [ ] Netlify project public hone ki tasdeeq (incognito mein test)
- [ ] Paper ke short aur long questions add karna (75 marks ka poora paper)
- [ ] Notes, Text Books, Guess, Pairing, Past Papers pages mein title + link add/edit/delete ka option
- [ ] Har kitab ke PDF links (`url`/`view`) aur cover images `BOOKS` mein bharna (abhi sirf 9th Mathematics ka hai); Tarjuma-tul-Quran ke entries bhi `BOOKS` mein hain (links khali)
- [ ] Views/Downloads ki sab students ki total ginti ke liye backend/database (abhi har browser ki alag)
- [ ] Jahan ab bhi "Guess" likha ho (Netlify/purani copies) wahan bhi Test Series karna

## 9. Known masle / notes
- (yahan likhein)

## 10. Claude limit ke liye tareeqa
- Naya chat shuru karte waqt: yeh file + sirf wohi file paste karein jis mein change chahiye
- `index.html` bohat bari hai (~100 KB). Poori mat paste karein, sirf wohi function/section jo badalna hai
- Ek message mein poori request likhein
- Limit khatam hone se pehle kahein: "ab tak ka summary likho" aur sections 7-9 update kar lein
- Har bade change ke baad `index.html` ka backup le lein

- 2026-11-13: Home category cards redesigned in Neon / Gradient Glow (cyberpunk) style (dark #14141c card, blurred pink-cyan-purple glow, cyan hover on links). Replaces the earlier glassmorphism .hc2 styling. Data, text, links, icons and JS unchanged.
- 2026-11-13: GLOBAL Neon/Gradient Glow theme (CSS only, appended at end of <style>): dark :root vars, glowing body bg, glow on .card/.bt/.sm button/.sub-card/.cyc__card, glow box-shadow on .sidebar, cyan top/nav borders, gradient .btn/.bk-dl. .paper stays white/black (print safe). Dark theme is forced in all modes.
