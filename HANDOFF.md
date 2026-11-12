# Handoff: improve kylehmitchell.com

Written 2026-11-12 by the session that rebuilt the task app. You are a new session picking
this up cold. Everything you need is here.

**Delete this file in your last commit. It must never reach `main`** (the repo root is the
live site, so anything in it is publicly served).

## The job

Kyle asked for every item in the list below to be done to his portfolio site, "full auto,
like the other work". Work through all of it without checking in. Push as you go.

Repo: `Kylemitchell64/portfolio`. The whole site is one file, `index.html` (575 lines, inline
CSS and a few lines of JS), plus `404.html`, `Kyle-Mitchell-Resume.pdf` and
`Kyle-Mitchell-Resume.docx`. No build step. Hosted on Vercel from `main` at kylehmitchell.com.

## Rules from Kyle that override anything else

1. **Keep the timeframe claims.** The hero stats (`<5mo` zero to AKS, `9mo` to hired) and the
   Oct 7 2025 start date stay. Kyle wrote "keep the time frame (6/9 months)"; the site says
   `<5mo` and `9mo`. Do not change the numbers to match his shorthand. Leave them as they are.
2. **Employer.** Blue Line Solutions may be named as his employer. Never add anything about
   the work he does there: no projects, no tech, no details. The existing line "The projects
   on this site are my own work, built on my own time" stays.
3. **Accuracy.** This is his public description of himself. Only claim what the repos show.
   When you describe the task app, describe what is in `my-task-app` on `main` today.
4. **Golf-cart site is conditional.** Include it only if both hold: (a) you confirm it works,
   and (b) it can be shown anonymously. See the golf-cart section. If either fails, leave it
   out and say why in your final report.

## Authority

Kyle said full auto. In the previous job that meant: commit and push to the session branch
freely, and merge to `main` (which deploys) only on his explicit word. Unless your kickoff
prompt says you may merge, finish everything on your branch, then ask once at the end.

Changes to the golf-cart demo repo are in scope only as described in that section.

## The list (do all of it)

### Broken or wrong

1. **Fonts do not load.** `index.html` links `./index_files/css2`, a leftover from "Save page
   as"; the file is not in the repo. `404.html` has the correct Google Fonts link pattern.
   Fonts used: Syne (400, 700, 800), DM Sans (300 plus whatever weights the CSS uses), DM Mono
   (300, 400). Prefer self-hosting the `woff2` files in the repo with `font-display: swap`;
   if the font host is not reachable from your sandbox, use the Google Fonts `<link>` with
   `preconnect` to both `fonts.googleapis.com` and `fonts.gstatic.com`.
2. **Task-app section is out of date.** Rewrite it from the current `my-task-app` README.
   It is now called Learning Tracker. Stale claims to remove or correct: "Cypress E2E",
   "30 req/min rate limiter", "100 KB request body cap", "Production Full-Stack Task
   Management System", and the `Cypress` tag. See "Task app facts" below.
3. **Timeline contradiction.** The page says both "Zero prior programming experience" and
   "after I resumed my journey in software engineering". They cannot both stand. Use the
   repo list as evidence (old private repos from 2020 and 2022 exist: `solus`, `FullName`,
   `Practice`) and reword so the two statements agree without changing the Oct 7 2025 start
   or the 9-month claim. Something like "started coding seriously" is honest; "zero prior
   experience" probably is not. Flag the final wording in your report.
4. **Footer says "Infrastructure provisioned with Terraform"** but the site is on Vercel.
   Fix it.
5. **Leftover junk:** the `<!-- saved from url=(0044)file:///C:/Users/Kyle/Downloads/index_3.html -->`
   comment (it also leaks a local path) and `<style type="text/css" id="operaUserStyle"></style>`.
6. **No mobile navigation.** Under 640px `.nav-links` is `display: none` with nothing in its
   place. Add a real menu (a button that opens the links; keyboard and screen-reader usable).

### Missing basics

7. **Meta description, Open Graph and Twitter tags, canonical URL, favicon.** Make a proper
   OG image (1200x630) and a favicon. Playwright can render them from HTML/SVG.
8. **Screenshots of both featured projects** (and the golf-cart site if it goes in). Capture
   them with Playwright at 2x. Optimise the files; use `width`/`height` and `loading="lazy"`.
   The task app can be run locally (see below). For the Turing game, add the repo with
   `add_repo` and run it locally, or capture the live site if your network allows.
9. **Nav skips the second project.** Add links so every project is reachable from the nav.
10. **Accessibility.** Add `<main>`, a skip link, `prefers-reduced-motion` handling, visible
    focus styles, and fix contrast: `--muted: #64748b` on `#090c10` looks below 4.5:1. Measure
    with axe (`@axe-core/playwright`) in every theme and fix what it reports. The inline script
    that hijacks anchor clicks should not break focus or the back button.
11. **External links:** add `rel="noopener noreferrer"` to every `target="_blank"`.

### Content and positioning

12. **Lead with what he built.** The hero is all speed stats. Keep the stats (rule 1) but
    make the first thing a visitor reads be the work. The task app's story (live attack, then
    a full security overhaul) is his signature and is currently bullet one of twelve.
13. **Cut the task-app bullets from twelve to about five,** grouped as product, security, ops.
14. **Reframe AKS as history.** The hero says he deploys "with Docker and Kubernetes" and
    manages "infrastructure on Azure", but everything live runs on Vercel and Render. Say he
    built and ran it on AKS, then migrated to zero-cost hosting. Both are true and the second
    is the stronger story.
15. **Trim the skills grid.** Drop filler such as VS Code, Git, "HTML5 / CSS3", PowerShell.
    Update testing tools to match the repos: Playwright, Vitest, xUnit, k6, axe. Cypress can
    stay only as past experience if it is framed that way.
16. **Résumé.** Read `Kyle-Mitchell-Resume.pdf`. Apply the same corrections as item 2 and 14.
    Regenerate both PDF and DOCX from one source so they match. Keep his layout.
17. **The `.docx` résumé is published but linked nowhere.** Either link it beside the PDF or
    remove it from the repo. Linking it is the better outcome if item 16 keeps them in sync.

### Bigger additions

18. **A short write-up page per project** (static HTML, same design): the problem, the key
    decisions, what broke, what he would do differently. Source material: each repo's README
    and code. For the task app: the local-first sync design and the security incident. For
    the Turing game: the AI impostor design and the anonymity threat model.
19. **Light theme and a one-click toggle,** following the system by default, with no flash
    on load. The task app's implementation is a good model: a tiny blocking script in
    `<head>` sets `data-theme` before paint, tokens are CSS custom properties, and the dark
    theme uses dark grey (not black), lighter surfaces for raised elements, and softened
    accents. See `my-task-app/my-todo-app/public/theme.js` and the top of
    `my-todo-app/src/styles/app.css`.
20. **Golf-cart client site.** See below.

## Golf-cart site

Repo: `Kylemitchell64/golf-cart-website` (public). Demo: golf-cart-website-demo.vercel.app.
It is real client work.

Do this in order:

1. `add_repo` it, read it, build it, run it locally, and drive it with Playwright. "Works"
   means: it builds clean, every page and link loads, forms behave, no console errors, and it
   holds up on a phone viewport. If you can reach the live demo, check that too.
2. Find every piece of identifying information: business name, owner or staff names, phone,
   email, street address, map embeds, logos, real photos of the premises or people, social
   links, domain names, analytics IDs, and anything in commit-visible config.
3. Decide which case you are in:
   - **The Vercel deployment is a demo, not the client's production site.** Replace the
     identifying details in the repo with clearly fictional ones (invented business name,
     `555` phone number, `example.com` email, no real address or map pin), keep it working,
     and push to a branch. Then feature it on the portfolio with a link and screenshots.
   - **It is, or feeds, the client's real site.** Do not change it. Feature it on the
     portfolio as an unnamed client project with no link, and only with screenshots that
     show nothing identifying (crop or blur). If that cannot be done cleanly, leave it out.
4. The repo is public and its git history may still hold the real details even after an
   edit. You cannot fix that by committing. Report it; do not rewrite history.
5. On the portfolio, describe it as work for "a local golf-cart dealership" or similar. No
   name, no town.

## Task app facts (for item 2 and the write-up)

All true of `my-task-app` on `main` at commit `214312f`:

- Name: Learning Tracker. Live at task-app-frontend-alpha.vercel.app.
- Local-first: data lives in the browser, the UI never waits on the server, works offline,
  installable (service worker). No account needed; sign-in only adds sync.
- One sync endpoint (`POST /api/sync`), last-write-wins per task, per-account version
  counter with a row lock so concurrent devices never miss a row.
- Features: one-line quick add with live parsing, Today / Upcoming / All / Done / Progress
  views, repeating tasks, drag reorder, undo, search, keyboard shortcuts, command palette,
  focus timer with a full-screen focus mode, streak and weekly chart, light and dark themes.
- Security: Google and GitHub OAuth, single-use sign-in code (no token in the URL),
  15-minute access tokens, rotating refresh tokens with reuse detection, per-user and per-IP
  rate limits, 1 MB body cap, server-side clamping of every field, CSP, account deletion.
- Stack: React 19, Vite 7, ASP.NET Core 8, EF Core 8, PostgreSQL, Workbox, dnd-kit.
- Tests at that commit: 57 API integration tests on real PostgreSQL (xUnit), 170 unit tests
  (Vitest), 56 browser tests (Playwright, including axe in both themes). GitHub Actions CI
  runs all three. Lighthouse scored 100 in all four categories on a local production build.
- History that is still true and worth keeping: built on Docker and AKS with Azure DevOps
  CI/CD, NGINX Ingress, ACR and Terraform, then migrated to Vercel + Render at zero cost.
- **How much of that Kyle wrote himself is his to state, not yours.** The rebuild above was
  done in an AI-assisted session. Write the portfolio copy so it is accurate about the
  project without making first-person claims you cannot back ("I hand-wrote..."). Flag this
  in your report so he can adjust the wording.

Re-read the README before writing: Kyle may have changed things since.

## Environment notes that will save you time

- **Network.** From the last sandbox, `*.vercel.app`, `*.onrender.com` and `dot.net` were
  blocked; npm, NuGet and apt worked. Check with `curl` before planning around live sites.
  Do not assume you can load kylehmitchell.com or the demos. Build and run things locally.
- **Playwright and Chromium are preinstalled** (`require('playwright')`, version 1.63.0).
  ESM scripts must live inside a project that has `playwright` in `node_modules`, or use
  `require`. Use `serviceWorkers: "block"` unless you are testing offline behaviour.
- **To run the task app locally** for screenshots: `apt-get install -y dotnet-sdk-8.0`,
  start PostgreSQL (`pg_ctlcluster 16 main start`; set the `postgres` password to `postgres`
  and create `tasks_dev`), `dotnet run` in `TodoApi` (port 8080), `npm ci && npm run dev` in
  `my-todo-app` (port 5173). Guest mode needs no API at all. The repo's own
  `npx playwright test` starts everything for you.
- **No Docker daemon** in the sandbox.
- **Extra repos** come in through `list_repos` then `add_repo` (`access: "push"` to write).
  Clone one at a time. After a first push with `-u`, a shallow clone may still report the
  commits as unpushed; adding the branch to `remote.origin.fetch` and fetching fixes it.
- **Serve the portfolio locally** with any static server (`npx serve` or `python3 -m
  http.server`) and test it with Playwright at 390, 768 and 1280 wide, in both themes.
- **Résumé files.** Check what tooling exists for PDF and DOCX before choosing an approach;
  rendering HTML to PDF with Playwright is a reliable way to get a PDF.
- The `code-review` skill forks a subagent and can exhaust the usage limit. Review inline.

## Definition of done

- Every numbered item is done, or has a stated reason it was left out (only item 20 may be).
- The page has no console errors, no broken links, no horizontal scroll at 390px, and axe
  reports no violations in both themes.
- Lighthouse on a local static serve: aim for 95+ in all four categories.
- A small Playwright check is committed (links resolve, nav works on mobile, theme toggle
  persists, axe clean) with a GitHub Actions workflow that runs it on push.
- `HANDOFF.md` is deleted.
- Final report to Kyle, short: what changed, what you could not verify, the exact wording
  you chose for item 3 and for the task-app authorship point, the golf-cart outcome, and the
  merge-to-`main` question if you were not pre-authorised.
