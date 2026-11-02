# Apna Karigar — Launch Gate Checklist

Site folder: `~/workspace/apnakarigar/site/`
Domain: https://apnakarigar.org
Built: 31 Oct 2026, from the extracted app file `apk-extract/assets/ustaad-karigar.html` (single-file bilingual Urdu/English home-services app).
Status: **NOT deployed** (per instructions — no deployment, no accounts created). All checks below were run against the actual files in this folder.

## Pages

| # | File | Type | Result |
|---|------|------|--------|
| 1 | index.html | App (start screen + booking app) + SEO head | ✅ |
| 2 | about.html | Static page | ✅ |
| 3 | contact.html | Static page (generic form) | ✅ |
| 4 | privacy.html | Static page (AdSense disclosures included) | ✅ |
| 5 | sitemap.xml | 4 URLs on https://apnakarigar.org | ✅ valid XML |
| 6 | robots.txt | Allow all + Sitemap line | ✅ |

**Pages count: 4 HTML pages + sitemap.xml + robots.txt.**

## Gate items (verified from files)

- [x] **Rebrand complete** — every visible "Ustaad Karigar" / "استاد کاریگر" replaced with "Apna Karigar" / "اپنا کاریگر" (title tag, start-screen H1, hero image alt, app-bar appName EN/UR, demo footer note EN/UR). **Grep proof: `ustaad` (any case) = 0 and `استاد` = 0 in all 6 files.** Tagline word "استاد" (common noun, "ہر کام کا استاد") changed to "ماہر" (same meaning, "ہر کام کا ماہر") so no trace of the old brand remains. Domain `apnakarigar.org` referenced in footer notes, nav, footer, canonical/OG URLs, schema, sitemap.
- [x] **Functionality preserved** — index.html is the full source app with surgical edits only: start screen, app screen, services grid, booking overlay/sheet, language toggle (Urdu/English), dark mode (prefers-color-scheme), join-as-karigar form, toast all present; structural markers and `data-t` translation attributes identical to source (52 = 52); embedded images untouched; extracted app JavaScript passes `node --check` (syntax valid); HTML parses with no tag errors.
- [x] **Tailor service added** — SERVICES array: `{ id:"tailor", icon:"scissors", en:"Tailor", ur:"درزی", price:600 }` (placed after Beautician). `scissors` already exists in the file's icon set (no needle/thread icon exists). Because the grid, booking flow and join form all iterate the SERVICES array, Tailor appears in all three automatically.
- [x] **Auto Electrician service added** — `{ id:"auto-electrician", icon:"zap", en:"Auto Electrician", ur:"آٹو الیکٹریشن", price:800 }` (placed in the car section, after Car Wash; `zap` exists in the icon set).
- [x] **Service count: 16 → 18** (verified by parsing the SERVICES array in source vs. built index.html; all 16 originals unchanged, all icons used exist in the icon set).
- [x] **About / Contact / Privacy linked in header AND footer on every page** — index.html has a slim top nav bar above the app screens plus a site footer after the app screens; about/contact/privacy use the same header nav + footer. Verified by file check: all 4 pages contain links to about.html, contact.html and privacy.html in both the `site-nav` and `site-footer` blocks.
- [x] **Unique title + meta description per page** — verified all 4 pages (index: "Apna Karigar — اپنا کاریگر | Home Services in Faisalabad"; About / Contact / Privacy each distinct). OG tags (og:title, og:description, og:url, og:site_name) present on all 4 pages; canonical URLs on https://apnakarigar.org.
- [x] **One H1 per static page** — about.html = 1, contact.html = 1, privacy.html = 1 (verified). index.html has exactly 1 H1 as well (the app brand heading on the start screen).
- [x] **Privacy disclosures** — privacy.html covers: data collected (bookings, karigar registrations, contact messages), how it is used, sharing, **cookies**, **third-party advertising incl. Google AdSense** (third-party vendor cookies, personalised-ads explanation, opt-out links to Google Ads Settings and aboutads.info), analytics, retention/security, children, user choices, changes, contact.
- [x] **Contact page honesty** — generic contact form only; a clear note states bookings happen through the booking flow on the home page. **No phone or WhatsApp number invented anywhere** (checked: no phone numbers in any page).
- [x] **LocalBusiness schema** — index.html carries valid JSON-LD (`HomeAndConstructionBusiness`, a LocalBusiness subtype): name "Apna Karigar", url https://apnakarigar.org/, areaServed Faisalabad, address Faisalabad/Punjab/PK, offer catalog listing all 18 services. JSON parses cleanly.
- [x] **Bilingual app kept** — the app remains Urdu/English with the language toggle exactly as in the source (local Pakistani service). New static pages are in English with full SEO meta.
- [x] **Faisalabad-first positioning** — About page tells the Faisalabad launch + city-by-city expansion story; the app's services subtitle now reads "…karigars near you in Faisalabad" (EN) / "فیصل آباد میں…" (UR) instead of Lahore. Demo provider data (names/areas) left untouched, as it is sample data labelled as such in the app footer.

## Notes / follow-ups for launch (not done here)

- Deploy step pending (hosting + DNS for apnakarigar.org still to be wired at launch time).
- The app is still a **demo** (sample providers/prices/bookings, labelled in its own footer note) — real provider onboarding and a booking backend are the next phase before public launch.
- Contact form is front-end only (shows a thank-you note locally); it needs a form endpoint/mailbox before it can receive real messages.

## Improvements v2 — Ranking pattern + Locations/Distance (31 Oct 2026)

Scope: same single-file app in `index.html`, all existing functionality and Apna Karigar branding preserved; demo data stays demo (deterministic, seeded by service index + provider slot, so values are stable between renders). NOT deployed.

### A) Karigar ranking / profile pattern
- [x] PASS — Every provider card shows a 5-star visual (filled/empty stars from rating) + numeric rating + reviews count, followers count, and completed-jobs count (grep-verified in the card template: `starsHtml`, `t("reviews")`, `t("followers")`, jobs line all present).
- [x] PASS — New deterministic demo fields in `providersFor`: `followers` (25–924) and `reviews` (15–234), seeded from service index/provider slot exactly like the existing rating/jobs formulas.
- [x] PASS — Level badge on every card, computed by `levelIdx()` from jobs + rating + followers: New (نیا) → Verified (تصدیق شدہ) → Rising (ابھرتا ہوا) → Popular (مشہور) → Faisalabad's Favourite (فیصل آباد کا پسندیدہ), bilingual via the `LEVELS` table. Simulated distribution over all 54 demo providers: 1 New / 11 Verified / 20 Rising / 15 Popular / 7 Favourite — every level actually occurs.
- [x] PASS — Verified tick (`badgeCheck` pill) now shows only for providers at Verified level or above (EMAHIR-style earned badge — safe competitor touch #1).
- [x] PASS — Sort control above the provider list: Recommended (existing default order) / Top Rated (`rankScore` = rating + followers + jobs combined) / Nearest first (distance). Bilingual labels via STR keys.
- [x] PASS — Honesty note "Rankings are earned, never sold — based on customer ratings, followers and completed jobs" shown under the provider list (both languages) and under the app footer note, plus a "How ranking works" section added to `about.html` with the same line.
- [x] PASS — Upfront-pricing note (KaamKrew-style — safe competitor touch #2): "Visit fees are starting prices — the karigar confirms the final price before work begins" under the provider list, bilingual.

### B) Locations + distance
- [x] PASS — `AREA_COORDS` table covers all 8 areas in the app's `AREAS` list (8 = 8, grep-verified) with plausible Faisalabad lat/lng; each provider carries `areaIdx` alongside its area.
- [x] PASS — Real haversine distance replaces the old fake `km` field (`p.km` usages left: 0). Sanity check: Gulberg→Cantt ≈ 2.43 km, Gulberg→DHA ≈ 3.18 km, same area = 0.
- [x] PASS — Customer "Your area" selector (all 8 areas, bilingual) + optional "Use my location" button (`navigator.geolocation`, graceful fallback toast + selector stays in charge; picking an area again clears the GPS point).
- [x] PASS — Each provider card shows its area with approximate distance labelled "≈ X.X km away" (both languages).
- [x] PASS — "Nearest first" sort uses the computed distance.
- [x] PASS — Booking sheet shows distance in the provider sub-line and adds "Your area" + "Distance ≈ km" rows to the booking summary (so e.g. a Car Mechanic sees how far the job is); the confirmed booking stores the customer's area + distance and the My Bookings list displays them.

### Verification (3 rounds, from the actual files)
- [x] Round 1 — Extracted JS passes `node --check`; SERVICES still = 18; "Ustaad"/استاد count still 0.
- [x] Round 2 — All new STR keys exist in BOTH language dicts (14/14 keys ×2); control IDs unique (`my-area`, `sort-sel`, `geo-btn` ×1 each); AREA_COORDS (8) matches AREAS (8).
- [x] Round 3 — Level-distribution + haversine simulation run in Node against the exact formulas in the file (results above); old fake-distance code fully removed.

### Intentionally NOT added
- No real accounts, backend, payments or live GPS tracking — demo stays front-end only, per scope.
- No phone/WhatsApp numbers invented anywhere (existing demo "Call" toast behaviour unchanged).
- Karigar Portal request cards were left as-is: a request already shows the customer's area, and a distance there would need the karigar's own home area, which the demo portal does not set.

## v3 — Professional release cleanup (31 Oct 2026, user instruction)
- Removed ALL visible demo labelling: start-screen Demo pill (element removed), footerNote EN/UR rewritten as professional service note (starting-prices line), toastCall EN/UR rewritten ("Calls are opening soon"). Verified: visible demo/ڈیمو/sample text = 0 across all 4 pages (remaining "demo" hits are only the unused .demo-pill CSS class and emptied STR keys). JS node --check OK; services still 18.
