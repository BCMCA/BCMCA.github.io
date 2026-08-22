# Berrien County MCA — site redesign handoff

This is a redesign of the public site: same content, new look. Everything below
is plain HTML/CSS/JS — no build step, no framework, nothing to install. It works
the same way the site already works today.

## What changed

- The old homepage (three big link cards) is gone. **Announcements is now the
  homepage.**
- Navigation moved from cards into a **left sidebar** that's always visible,
  with the full original description text under each link (not summarized).
- A large header with the seal and the Authority's name sits across the top of
  every page.
- **Protocols** still lives at `/protocols/` and was **not touched** — the
  sidebar just links out to it normally, like any other page.
- On phones, the sidebar collapses into a tappable accordion instead of a long
  scroll.
- **/announcements/** (the old dedicated page) now just redirects to the
  homepage, in case that old link is bookmarked or printed anywhere.

## What did *not* change

- `proposed/proposed.json` and `announcements/announcements.json` — same
  format, same fields. You publish new items exactly the way the README
  already describes.
- The Web3Forms comment intake key in `proposed/index.html` — untouched,
  still wired to comments@berrienmca.org.
- `CNAME`, `robots.txt`, the seal image files — untouched.
- The PDFs in `proposed/pdfs/` — untouched.

## How to apply this

1. Unzip this into your local copy of the repo, **overwriting** the existing
   `index.html`, `about/index.html`, `proposed/index.html`, and
   `announcements/index.html`.
2. Leave `proposed/proposed.json`, `announcements/announcements.json`,
   `proposed/pdfs/`, `CNAME`, `robots.txt`, and the seal files as they already
   are in your repo (this zip includes copies of them too, so a full overwrite
   is also safe — nothing in them was changed).
3. Commit and push as usual. GitHub Pages will pick it up the same way it
   always has.

If you'd rather not overwrite everything at once, the only files that actually
changed are:
```
index.html
about/index.html
proposed/index.html
announcements/index.html   (now just a redirect to /)
```

## Editing this later with Claude

Every page repeats the same block of CSS in its own `<style>` tag (the site
has no shared stylesheet — that's how it was already built, this keeps that
pattern). If you want to change something site-wide — a color, the header
height, the fonts — you'll need to make the same edit in all three real pages
(`index.html`, `about/index.html`, `proposed/index.html`). Tell Claude
something like:

> "In all three pages, change --gold to #___" — Claude can find and update it
> in each file.

The sidebar navigation, the header, and the logic that makes the sidebar
collapse into an accordion on mobile are close to identical across all three
pages too, so the same approach works for nav changes.

Page-specific content lives in the `<main>` section of each file:
- `index.html` — pulls announcement text from `announcements/announcements.json`
  automatically. You don't need to touch the HTML to add a new announcement.
- `proposed/index.html` — pulls protocol groups from `proposed/proposed.json`
  the same way.
- `about/index.html` — the About text is written directly in the HTML (no
  JSON file), so edits there mean editing the paragraphs in that file.

If anything looks broken after an edit, the safest thing to tell Claude is
just: open the file, describe what looks wrong (with a screenshot if you
have one), and ask for a fix — that's exactly how this version was built.
