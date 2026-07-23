# Publishing & Updating This Website

Your site is a plain static website (HTML + CSS + images). No build step, no framework.
That makes it simple to host anywhere and easy to update.

This guide has three parts:
  1. One-time setup — put the site on GitHub and connect it to Netlify (auto-deploys forever after)
  2. Adding a new article — the repeatable workflow
  3. Using Claude Code to do it for you (recommended for "I'll update often")

────────────────────────────────────────────────────────
## PART 1 — ONE-TIME SETUP (GitHub + Netlify)
────────────────────────────────────────────────────────

Do this once. After it, every change you push to GitHub goes live automatically.

### Step 1 — Put the site in a GitHub repo
1. Create a free account at github.com if you don't have one.
2. Click "New repository". Name it e.g. `portfolio` or `atif-site`. Make it PUBLIC. Don't add a README (you already have files).
3. On the next screen, use "uploading an existing file".
4. Upload the CONTENTS of this `site` folder — meaning `index.html`, `style.css`, the `articles/` folder, and the `assets/` folder. 
   IMPORTANT: `index.html` must sit at the TOP level of the repo, not inside a `site/` subfolder.
5. Commit.

### Step 2 — Connect Netlify to the repo
1. Create a free account at netlify.com (you can sign in with GitHub — easiest).
2. "Add new site" → "Import an existing project" → choose GitHub → pick your repo.
3. Build settings: leave everything BLANK.
      - Build command: (empty)
      - Publish directory: (empty, or `.`)
   Because this is a plain static site, there's nothing to build.
4. Click "Deploy". In ~30 seconds you get a live URL like `something-random-1234.netlify.app`.

### Step 3 — Give it a nicer name (optional, free)
- In Netlify: Site settings → "Change site name" → set e.g. `atif-salman` → your URL becomes `atif-salman.netlify.app`.

### Step 4 — Custom domain (optional, ~$10–15/year)
- Buy a domain (Namecheap, Cloudflare, Google Domains, etc.), e.g. `atifsalman.com`.
- In Netlify: Domain settings → "Add a domain" → follow the DNS instructions (usually add a couple of records at your domain registrar).
- Netlify gives you free HTTPS automatically.

DONE. From now on, anything you push to the GitHub repo goes live within seconds.

────────────────────────────────────────────────────────
## PART 2 — ADDING A NEW ARTICLE (the repeatable workflow)
────────────────────────────────────────────────────────

Each new article is two edits: create the article page, then add a card linking to it on the homepage.

### A. Create the article file
1. Copy an existing article as your template — `articles/pooling.html` is a good one.
2. Save it as `articles/your-new-slug.html` (lowercase, hyphens, no spaces — e.g. `articles/dispatch-timing.html`).
3. In that new file, change:
      - The `<title>` and the `og:`/`twitter:` meta tags near the top
      - The `<div class="kicker">` (the small label above the headline)
      - The `<h1>` headline
      - The `<p class="dek">` (italic subtitle)
      - The body content
   Leave the top `<nav>`, the `← All writing` link, and the closing tags as they are — they make it match the rest of the site.

### B. Add a card on the homepage
Open `index.html`, find the `<div class="posts">` block inside the Writing section.
Copy one existing `<a class="post" ...>` block and paste it as the new first item. Change:
      - `href="articles/your-new-slug.html"`
      - the tag label(s) inside `<div class="meta">`
      - the `<h3>` title
      - the `<p>` description

Tag classes available (control the little coloured label):
      - `<span class="tag strat">Product & business strategy</span>`   (gold — your primary)
      - `<span class="tag exp">Experimentation</span>`                  (teal)
      - `<span class="tag metric">Metric definition</span>`            (terracotta)
      - `<span class="tag ai">Applied AI</span>`                        (purple)
      - `<span class="tag sub">Any secondary label</span>`             (quiet outline — use as the 2nd tag)
      - `<span class="tag alt">…</span>`                                (teal alt)
For an external (Medium) article, add `target="_blank" rel="noopener"` to the `<a>` and a `· Medium ↗` note like the Context Trap card.

### C. Publish
- If using GitHub web: edit/upload the files in the repo and commit → Netlify redeploys automatically.
- If using a local clone: `git add . && git commit -m "add article" && git push` → auto-deploys.

────────────────────────────────────────────────────────
## PART 3 — USING CLAUDE CODE (recommended if you update often)
────────────────────────────────────────────────────────

Claude Code runs in your project folder on your own machine and can do all of Part 2 for you,
including committing and pushing (which triggers the Netlify auto-deploy).

### One-time
1. Clone your repo locally:  `git clone https://github.com/<you>/<repo>.git`
2. Open that folder in Claude Code.

### Every new article
Just tell Claude Code something like:
      "Add a new article to my site titled '<title>'. Here's the content: <paste or point to a draft>.
       Use articles/pooling.html as the style template, create articles/<slug>.html, and add a
       matching card at the top of the Writing section in index.html with the tag '<Product & business strategy>'.
       Then commit and push."

Claude Code will create the file, wire up the homepage card consistently, and push — and your live
site updates within seconds. You never touch the deploy step.

TIP: keep each finished article's HTML consistent by always pointing Claude Code at an existing
article as the template. That keeps fonts, nav, and styling identical across the site.

────────────────────────────────────────────────────────
## FILE MAP (what's what)
────────────────────────────────────────────────────────
  index.html              → homepage (hero, focus areas, writing list, speaking, about, footer)
  style.css               → all styling for every page
  articles/*.html         → one file per full article (self-hosted ones)
  assets/atif.jpg         → hero photo
  assets/ksbl.jpg         → speaking-section photo
  assets/Atif_Salman_Sheikh_CV.pdf → the downloadable CV (footer link)

## BEFORE YOU SHARE THE LINK WIDELY
  - Confirm the footer email in index.html (currently atif.mansal@gmail.com).
  - Once you know your final URL/domain, change the og:image and twitter:image meta tags
    in index.html AND each article from the relative "assets/atif.jpg" to the absolute
    "https://YOURDOMAIN/assets/atif.jpg" — so LinkedIn/WhatsApp show your photo in link previews.
