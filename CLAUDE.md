# Art of Chaos website: working notes for Claude

Public site for Art of Chaos, served by GitHub Pages from `main` at https://artofchaos-dev.github.io/Art-of-Chaos/ (repo renamed from The-Art-of-Chaos on 2026-11-10; GitHub never redirects the old Pages URL, so the old address is a 404).

**This repo is public.** Everything in it, this file included, is world-readable. Open tasks and the next step live in `NEXT.md`.

## What this repo is

- This repo is only a slice of a bigger business folder. The source of truth is `Development/website/site/` inside the owner's private business folder, which has **no git remote on purpose** and lives on the owner's desktop server. Only that `site/` directory is pushed here.
- **Cloud sessions can't see the business folder.** Work here is limited to the public site. Anything that needs the business folder (bots, agents, the console, product builds, private notes) waits for a desktop session, or for the owner to decide on a private repo.
- Before assuming this repo is current, check whether the business folder (or its monthly backup) has newer site files. Do not "fix" things here that may already be fixed there. If you change a page here, say so in `NEXT.md`, so the desktop session copies it back into `site/` and the next sync doesn't overwrite it.
- Other products have their own repos (Aetheris, Echo, Chaos's links page). Do not mix them in.

## Stack and conventions

- Plain static HTML plus one shared `style.css`. No framework, no build step, no package manager. Hand-code changes.
- Pages: `index.html` (one-page home), `calculator.html`, `logbook.html` (QR target printed in the logbook, so never move or rename it), `echo-privacy.html` (linked from the Echo app's Play listing, so never move or rename it). Fonts load from Google Fonts (Comfortaa, Red Hat Display/Text, Newsreader, Ovo).
- `.nojekyll` is present so Pages serves the files as-is. Keep it.
- **After any `style.css` change, bump the `?v=` on the stylesheet link in every page.** Pages caches CSS for about 10 minutes, so visitors otherwise see the old look.
- Every new public page needs a `<url>` in `sitemap.xml`; update `<lastmod>` when a page changes. `robots.txt` only takes effect once the site moves to its own domain (crawlers read it at a domain's root); until then the sitemap is submitted in Search Console.
- Mascot art in `img/` (Cypress, formerly Aspen, and Francine) is licensed and not open source. Never reuse or redistribute it. No portrait of Chaos (Elizabeth) until she gives written OK.
- The "Get it" button on the home page points to the Profit Tracker on Payhip (https://payhip.com/b/w7r5f) with `rel="noopener"`. Keep it pointing there unless the owner says otherwise.
- No trackers, no cookies, no analytics scripts.
- `subscribe.html`/`.js` exist in the business folder but are **not published** (paid tiers not launched; copy awaiting approval). Don't recreate them here.

## Naming rule

- The company name is **"Art of Chaos"**, never "The Art Of Chaos". All-caps designs use "ART OF CHAOS".
- Do not rename URLs, handles, domains, folder paths or identifiers (e.g. `theartofchaosllc`, `theartofchaos.echo`).
- The 2026-11-14 name sweep and the sitemap/robots URL fix were reviewed and published on 2026-11-17.

## Pipeline: draft → review → approval → publish

Nothing reaches `main` (the live site) without both human gates.

1. **Draft (development):** code and page changes are built and checked by the development agent. Work goes on a `draft/...` branch; commit messages start with `DRAFT:`.
2. **Michael (Dyzzy) reviews** all development output. Finished work is never treated as approved until he says so.
3. **Sales polish:** after Michael's review, copy, brand fit and page presentation get a sales pass.
4. **Elizabeth (Chaos) approves** final output. Only approved work is published.
5. **Publish:** merge the reviewed branch to `main`. Pages redeploys in about a minute.

Only these two human gates stop work; other hand-offs between agents start on their own. Always human: money, policy changes (Michael, Elizabeth and Claude vote together), platform publish steps, and speaking as a founder. Sign work with name and role (e.g. `— Claude, Autonomic Chief`).

## Publishing from the business folder (desktop session)

The exact step from `site/` to GitHub, run by the development agent on the desktop server:

1. Working copy of this repo: `Development/website/.publish/` (git-ignored in the business folder; survives reboots).
2. Copy `Development/website/site/` into it, leaving out anything unapproved (today: `subscribe.html`, `subscribe.js`, `subscribe-config.js`). Keep `.nojekyll`, `README.md`, `CLAUDE.md`, `NEXT.md`. Delete images the pages no longer use.
3. Check: every local `src`/`href` resolves, `sitemap.xml` lists every public page, `?v=` bumped if CSS changed, secret scan clean.
4. Commit to a `draft/...` branch and push it. After Michael's review (and Elizabeth's approval where copy or brand changed), merge to `main`.
5. Push auth uses a **repo-only SSH deploy key** with absolute paths (relative ones break under `git -C`):
   `GIT_SSH_COMMAND="ssh -i <business-folder>/.secrets/github-website-deploy -o IdentitiesOnly=yes -o UserKnownHostsFile=<business-folder>/Development/website/.github_known_hosts -o StrictHostKeyChecking=yes"`
   GitHub's host key is pinned in `.github_known_hosts` (fingerprint `SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU`, checked 2026-11-03).

Cloud sessions push through the GitHub app connection instead, and never to `main`: open a branch and leave the merge to Michael.

### Deploy keys (names only; the keys never leave the owner's `.secrets/`)

| Key name | Repo |
|---|---|
| `github-website-deploy` | this repo (ArtofChaos-dev/Art-of-Chaos) |
| `github-chaos-deploy` | Chaos's links page |
| `github-aetheris-deploy` | Aetheris |
| `github-echo-deploy` | Echo |

Each key has write access to its own repo only. Never commit a key, token or `.env` file here.

## Content rules

- Never put secrets, tokens, customer data, finances or private business details in this repo.
- Keep pages free of anything about the owner's children or family.
- Third-party brands, characters or IP stay out of the site, except licensed art with its licence recorded.
- Direction as of 2026-11: lead with small tools and calculators that compound income. The own-site storefront is the hub, and marketplaces such as Payhip feed traffic back to it. Products should open a conversation with the audience, with a visible human contact. In promos, name the problem first, and leave the price for the page.

— Claude, Autonomic Chief (merged from the cloud session's draft and the desktop CLI's notes, 2026-11-17)
