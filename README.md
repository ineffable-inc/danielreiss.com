# danielreiss.com — Deployment Guide

## What's in this folder

```
deploy/
├── index.html          ← The site (single file, all CSS inline)
├── admin/
│   ├── index.html      ← Decap CMS admin panel
│   └── config.yml      ← CMS field definitions
└── images/
    ├── yung-daniel.jpg  ← Hero photo (baby in suit)
    └── chimp-photo.jpg  ← Chimp photo (Meanwhile section)
```

## Quick Deploy (no CMS, just the site)

1. Push this entire `deploy/` folder to your existing GitHub repo for danielreiss.com
2. On Netlify, set the publish directory to the repo root (or wherever these files land)
3. Deploy. Done. The site is fully static — no build step needed.

## To Enable the CMS (edit copy in your browser)

The CMS lets you go to `danielreiss.com/admin` and edit all your copy in form fields. Here's how to set it up:

### Step 1: Enable Netlify Identity
1. In your Netlify dashboard → Site settings → Identity → Enable Identity
2. Under Registration, set to "Invite only"
3. Under Services → Git Gateway, click "Enable Git Gateway"

### Step 2: Invite yourself
1. Go to Identity tab in Netlify dashboard
2. Click "Invite users" → enter your email
3. Check your email, accept the invite, set a password

### Step 3: Use it
1. Go to `danielreiss.com/admin`
2. Log in with your Netlify Identity credentials
3. Edit content in the CMS forms
4. Click "Publish" — changes commit to your Git repo

### Important caveat
Right now this is a static HTML file — the CMS will save your content edits as JSON/markdown files in the repo, but the **index.html won't auto-update** from those files without a build step. 

**Two paths forward:**

**Path A (Recommended):** Add Eleventy as a build step. The `/danielreiss/` project folder (also in the zip) has the full Eleventy setup — templates, content files, config. Set Netlify's build command to `npx @11ty/eleventy` and the publish directory to `_site`. Then CMS edits auto-build and deploy.

**Path B (Quick & dirty):** Use the CMS as a nice editor to draft copy, then manually update index.html. Still way better than editing raw HTML because you get a clean writing interface.

## Editing the HTML directly

If you just want to tweak copy without the CMS, the index.html is cleanly structured with HTML comments marking each section. Search for:
- `<!-- HERO -->` — name, tagline, descriptor
- `<!-- LOGO MARQUEE -->` — company logos and awards
- `<!-- STORIES -->` — the main editorial blocks
- `<!-- MIC DROP -->` — the names list
- `<!-- HUMAN / IMPACT -->` — fellowship/impact work
- `<!-- CONTACT -->` — email and sign-off

## Adding real logos

The logo marquee currently uses text placeholders. To upgrade:
1. Download SVGs from worldvectorlogo.com or company sites
2. Normalize them: convert to single color (use the ink color #1A1A18), set consistent height (~24px)
3. Replace the `<span class="marquee-logo">` elements with `<img>` tags
