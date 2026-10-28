# mateo-site

Mateo Robles's personal site: one static page for hiring managers in support,
implementation, solutions and creative-technologist roles. Plain HTML and CSS, two
self-hosted fonts, no build step. The only script is the email copy button.

## Where the words come from

Every sentence about Mateo comes from `truth/` in the private `SyberLabs/mateo-career`
repo: project cards from `truth/projects.md`, everything else from `keep` and `rewrite`
rows in `truth/claims.md`, `truth/roles.md` and the defaults in
`truth/open-questions.md`. That repo's `site/trace.json` maps each fragment of this page
to its source, and its `scripts/trace_site.py` checks the page:

```sh
python3 ../mateo-career/scripts/trace_site.py index.html   # must end "untraced: 0"
```

Change a sentence here only after changing the truth it comes from, then update
`site/trace.json`.

## Files

| path | what |
|---|---|
| `index.html` | the page, with its CSS inline |
| `img/mateo-robles-*.webp` | the photo at 320, 480 and 640 px (source: `mateo-career/assets/photo.jpg`) |
| `img/og.jpg` | the 1200×630 link preview |
| `resumes/*.pdf` | the three role-family résumés |
| `fonts/` | Young Serif and Atkinson Hyperlegible Next (SIL Open Font License) |
| `404.html` | not-found page |

## Updating

**Résumés.** Build them in `mateo-career` (`resumes/README.md`), then copy:
`A-support-implementation-qa.pdf` to `resumes/mateo-robles-resume-support-implementation-qa.pdf`,
`B-solutions-devrel-creative.pdf` to `resumes/mateo-robles-resume-solutions-devrel-creative.pdf`,
`C-ai-automation-operations.pdf` to `resumes/mateo-robles-resume-ai-automation.pdf`.
These public copies leave the phone number off; the email and links are on them.

**Intro video.** The page has a marked slot (`#intro-video`) until
`mateo-career/media/intro.mp4` exists. To fill it, add `media/intro.mp4`, a poster frame
`media/intro-poster.jpg` and captions `media/intro.en.vtt`, then replace the
`<div class="video-slot" id="intro-video">` block with:

```html
<figure class="intro-video" id="intro-video">
  <video controls preload="none" playsinline poster="media/intro-poster.jpg" width="1280" height="720">
    <source src="media/intro.mp4" type="video/mp4">
    <track kind="captions" src="media/intro.en.vtt" srclang="en" label="English" default>
  </video>
</figure>
```

The CSS for that block is already in the page. Video doesn't count toward the 1 MB budget,
but keep it short; `preload="none"` keeps it off the first load.

**Photo.** Replace `mateo-career/assets/photo.jpg`, then regenerate the three WebP sizes
(square, quality 80).

## Checks before publishing

- Lighthouse, mobile: performance, accessibility and SEO at 90 or higher.
- A link checker over the page, PDFs and anchors: `npx linkinator <url> --check-fragments`.
- No sideways scrolling at 390 px; screenshots at 390 and 1440 px go to `mateo-career/site/`.
- The trace check above.

## Deploying

GitHub Pages, from the `main` branch root, live at https://syberlabs.space/mateo-site/ (the SyberLabs organization's Pages site uses the custom domain `syberlabs.space`, so project sites are served under it). `.nojekyll` tells Pages to serve the files as they are.

## Design

Light runs through Mateo's projects: PorchLight, RISE's "light and sound", Gyre's trails of
light. So the page is a porch at dusk with one warm lamp. Dusk `#131d33`, moonlight text
`#eef1f7`, haze `#a6b1c9`, lamp `#ffb547`. The lamp colour is used for the light itself, the
availability line, focus rings and link underlines, and the "What I did" row of each project:
it lights up Mateo's own part. Projects are laid out as credits: who did what, and how it was
checked.
