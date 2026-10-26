TIMERNOOK — STATIC SITE FOR VERCEL
==================================

WHAT THIS IS
------------
A fully static version of TimerNook: 331 real HTML pages (292 tools minus
1 flagship folded into the homepage, 21 category pages, 17 info/legal
pages, plus a homepage and an all-tools hub), built from your actual
generated content (chronly-content.xml) and using the real, working
JS engines — not a demo, not placeholders. It needs no PHP, no
database, and no build step, which is why it can run on Vercel (the
WordPress version genuinely cannot — Vercel has no PHP runtime or
database).

VERIFIED BEFORE DELIVERY (not just claimed)
--------------------------------------------
- 0 broken internal links, checked across all 331 pages against the
  real file tree (not sampled — every href, every page).
- 0 broken <script src> references.
- 0 malformed JSON-LD blocks (560 checked: WebApplication + FAQPage
  schema on tool pages, WebSite + FAQPage on the homepage).
- Correct script load order verified for every engine, including the
  two that depend on another file loading first (repeating-round.js
  needs countdown.js; calculator.js needs calculators.js).
- The 14 pages that don't have a matching engine yet (Metronome, Typing
  Speed Test, live Clock, etc. — same list as the WordPress build's
  content-coverage.md) render their content correctly and simply don't
  mount a tool widget — verified this doesn't throw a JS error.
- The 24 international placeholder-translation pages carry
  <meta name="robots" content="noindex,follow"> and are excluded from
  sitemap.xml, exactly like the WordPress build — this was actually
  missing on the first pass here and had to be fixed; noted so nothing
  is overstated as "always been right."

WHAT'S DIFFERENT FROM THE WORDPRESS VERSION — READ THIS
----------------------------------------------------------
This is a genuinely different site, not the same site running somewhere
else. Some things that only work with a real backend do not exist here:

- No admin panel. There's no way to log in and edit a page. To change
  anything, you edit chronly-content.xml or the generator script
  (build_static_site.py) and rebuild.
- No live database. All 331 pages are frozen HTML files as of when
  this was generated. Nothing updates itself.
- No working contact form. The "Contact" link is a plain mailto: link
  (opens the visitor's own email client) — there's no server to
  receive a form submission. This was a deliberate choice: a fake form
  that silently does nothing would be worse than an honest mailto link.
- No internal site search. WordPress's built-in search needs a
  database query; a static site has nothing to query. There is no
  search box on this build.
- Editing content means re-running the Python generator, not clicking
  "Update" in an admin screen.

If you need real content editing, a working contact form, or search,
those require an actual backend (WordPress on real hosting, or a
proper headless CMS + this frontend) — no static-site trick makes those
work without one.

HOW TO DEPLOY ON VERCEL
-------------------------
1. Do NOT run any build command — this is plain static HTML/CSS/JS.
   Leave the Build Command field blank in Vercel's project settings.
2. vercel.json already sets "outputDirectory": "public", so Vercel
   will not show the "No Output Directory" error again.
3. Option A (CLI): install the Vercel CLI (`npm install -g vercel`),
   cd into this folder (the one containing vercel.json and public/),
   run `vercel`, follow the prompts.
   Option B (dashboard): vercel.com/new → deploy this folder (as a Git
   repo or via drag-and-drop) → Vercel auto-detects vercel.json.
4. Before going live, replace the placeholder domain in build_static_site.py
   (SITE_URL = "https://example.com") with your real domain and
   rebuild, so canonical tags, sitemap.xml, and Open Graph URLs are
   correct — and replace hello@example.com in the generator with your
   real contact email.

REBUILDING AFTER A CONTENT CHANGE
-----------------------------------
  python3 build_static_site.py
This regenerates every page from chronly-content.xml. If you edit that
XML by hand (or regenerate it from the original content-generation
scripts), rerun this and redeploy.

REBRAND + VISUAL REFRESH (this pass)
--------------------------------------
- Renamed from "Chronly" to "TimerNook" everywhere user-visible: page
  titles, meta tags, schema names, header/footer, sitewide FAQ text.
  (Internal CSS class names still use a "chronly-" prefix — that's an
  invisible implementation detail, not shown anywhere on the site, so
  it was left alone rather than risk a much larger, purely-cosmetic
  rename across every file for zero visible benefit.)
- New color scheme: a bold burnt-amber accent (#C2410C) replacing the
  old blue, and a warm near-black (#1C1410) for dark mode instead of a
  cooler pure black — chosen to match "TimerNook"'s cozy-but-confident
  positioning rather than a generic blue SaaS look.
- UI polish: pill-shaped buttons, softer/larger card corners, a subtle
  warm gradient band behind the homepage hero, and a hover lift on
  tool cards.
- SITE_URL is now set to https://timernook.com and the contact email
  to hello@timernook.com — update inc/build_static_site.py further if
  either changes.
- Re-verified after every change: 0 broken links, 0 broken script
  tags, 0 malformed JSON-LD (560 blocks checked), across all 331 pages.
