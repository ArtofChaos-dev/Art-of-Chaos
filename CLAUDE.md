# Art of Chaos website: working notes for Claude

Public site for Art of Chaos, served by GitHub Pages at https://artofchaos-dev.github.io/Art-of-Chaos/ (repo renamed from The-Art-of-Chaos on 2026-11-10; GitHub never redirects the old Pages URL, so the old address is a 404).

## What this repo is

- This repo is only a slice of a bigger business folder. The source of truth is `Development/website/site/` inside the owner's private business folder, which has **no git remote on purpose**. Only that `site/` directory is pushed here.
- Before assuming this repo is current, check whether the business folder (or its monthly backup) has newer site files. Do not "fix" things here that may already be fixed there.
- Other products have their own repos (Aetheris, Echo). Do not mix them in.

## Stack and conventions

- Plain static HTML plus one shared `style.css`. No framework, no build step, no package manager. Hand-code changes.
- Pages: `index.html` (one-page home), `calculator.html`, `logbook.html`, `echo-privacy.html`. Fonts load from Google Fonts (Comfortaa, Red Hat Display/Text, Newsreader, Ovo).
- `.nojekyll` is present so Pages serves the files as-is. Keep it.
- Every new public page needs a `<url>` in `sitemap.xml`; update `<lastmod>` when a page changes.
- Mascot art in `img/` (Aspen, Francine) is licensed and not open source. Never reuse or redistribute it.
- The "Get it" button on the home page points to the Profit Tracker on Payhip (https://payhip.com/b/w7r5f). Keep it pointing there unless the owner says otherwise.

## Naming rule

- The company name is **"Art of Chaos"**, never "The Art Of Chaos". All-caps designs use "ART OF CHAOS".
- Do not rename URLs, handles, domains or folder paths.
- Known stale spots in this repo as of 2026-11-17: the old name appears in `README.md` and all four HTML pages, and `sitemap.xml` still lists the dead `vexxidecimal.github.io/The-Art-of-Chaos/` URLs. The business-folder rename sweep of 2026-11-14 is still a draft awaiting the owner's review, so check there before changing these.

## Workflow

- Work arrives as draft, then owner review, then publish. Do not treat finished work as approved. Label drafts as drafts in commit messages.
- Never put secrets, tokens, customer data or private business details in this repo. It is public.
- Keep pages free of anything about the owner's children or family.
- Direction as of 2026-11: lead with small tools and calculators that compound income. The own-site storefront is the hub, and marketplaces such as Payhip feed traffic back to it. Products should open a conversation with the audience, with a visible human contact.
