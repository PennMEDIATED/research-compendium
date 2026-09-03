# Penn MEDIATED — Research Compendium

Penn research on the quantitative study of the information ecosystem and its impact on democracy, curated and translated for journalists, media leaders, civil society organisations and policymakers. 68 entries across seven themes.

This is the rebranded replacement for [`Penn-MEDIATED/Research-Compendium`](https://github.com/Penn-MEDIATED/Research-Compendium), the version currently live at infodem.upenn.edu/research-compendium. Content is carried over unchanged; everything about how it looks and behaves is rebuilt on the sitewide standards. See "What changed from the old page" below.

## What's in this repo

- `index.html` — page markup, styling **and** behaviour in one file. Like `llm-civic-discourse` (and unlike its other siblings) this page is a small React app: React + ReactDOM + Babel Standalone from cdnjs, JSX compiled in the browser. No build step and no `npm install` — just a `<script type="text/babel">` instead of a plain `<script>`.
- The entries live as an `ENTRIES` array at the top of that script. Design tokens are in the `<style>` block in `<head>`; page CSS follows them in the same block.

## Adding or editing an entry

Copy an existing object in `ENTRIES` and fill it in. Every field is required except `importance`:

| Field | What it holds |
| --- | --- |
| `id` | Slug, unique on the page. Used as the React key and the detail panel's `id`. |
| `title` | Paper title, plain text. |
| `url` | Where the paper lives. Opens in a new tab. |
| `faculty` | Penn faculty lead, exactly as it should read — this string also populates the faculty filter, so spelling must match across entries. |
| `date` | Display date, `M/D/YYYY`. |
| `year` | Integer. Drives the year filter and the default sort. |
| `themes` | Array of one or more theme names. **Must** match a key in `THEME_COLORS`, or the tag falls back to grey. |
| `takeaway` | One sentence, plain text. Shown collapsed. |
| `isNew` | `true` puts the "New" badge on the title. Remember to clear it on older entries. |
| `overview` | Trusted HTML — the long summary. |
| `importance` | Trusted HTML — the "Why is this important?" panel. Omit to hide the heading. |

`overview` and `importance` are injected with `dangerouslySetInnerHTML` so the Center's hand-written `<ol class="findings-list">` blocks and `<strong>` lead-ins survive. **That means these two fields are trusted input.** Paste only Center-authored copy into them; never anything a visitor or a third party supplied.

Adding a new theme means adding it to **both** `THEME_COLORS` and `THEME_ORDER` — the first gives it colours, the second puts it in the filter row.

## What changed from the old page

Content is identical. The presentation was rebuilt to the standards in these READMEs:

| | Old page | Here |
| --- | --- | --- |
| Type families | EB Garamond + **Roboto** | EB Garamond + **DM Sans**, the only two families sitewide |
| Type sizes | 15 hand-set sizes, four of them below 12px (9, 10, 11, 11.5) | The `--fs-*` scale, 12px floor |
| Palette | Penn navy `#011F5B`, gold `#f2c100`, link blue `#0055A4`, maroon eyebrow `#990000` | The brand tokens — `--c-accent`, `--c-red`, `--c-red-dark`, `--c-dark` |
| Links | Blue, `text-decoration: underline` | The five-category taxonomy below |
| Eyebrow | "RESEARCH" kicker above the page title | Removed — no eyebrow above hero headings, sitewide |
| Theme badges | Six ad-hoc colour pairs | The light-tint / saturated-border / dark-text trios `llm-civic-discourse` uses |
| Spacing | Hand-set px throughout | The `--space-*` 8px scale |
| Layout width | `max-width: 1280px`, 24px gutters | The shared 1440px cap with the 80/32/20px gutter scale |
| Dropdown marker | Browser default on `<select>` | The sitewide chevron, `appearance: none` |

The one thing carried over as-is: the auto-resize `postMessage`, which the old page already had.

## Overlap with `llm-civic-discourse` — unresolved

18 of these 68 entries carry the **LLMs & Civic Discourse** theme, and there is a separate `llm-civic-discourse` repo holding 87 papers on that same topic. Nothing is currently done about the duplication — the two pages are independent, with their own entry lists and their own theme vocabularies.

Decide before launch whether the Compendium should link out to that dashboard, drop the overlapping entries, or keep both. Whichever way it goes, the two entry lists are maintained by hand and will drift.

## Typography

Sitewide conventions, identical across every Penn MEDIATED repo:

- Two families only — `--f-serif` (EB Garamond) and `--f-sans` (DM Sans). No monospace face anywhere.
- Serif is for headings; running prose is sans. The page title, entry titles and the detail headings are the serif exceptions by design.
- Uppercase micro-labels ("Key takeaway", "Center newsletter", the theme chips) are DM Sans 700 uppercase at `--fs-micro`.
- **12px is the floor.** Nothing on the page ships smaller — the old page had four sizes below it.
- Heading scale at desktop: 56 / 40 / 24px (`--fs-h1` / `--fs-h2` / `--fs-h3`). The clamps interpolate across the viewport, so tablet needs no separate breakpoint.

## Layout

- One `.wrap` handles the page width: 1440px cap, 80px side padding, stepping to 32px under 900px and 20px under 480px.
- The filter strip sits on `--c-light-bg` and spans the full viewport width; the wrap goes inside it, never around it. Same rule as every coloured section sitewide.
- The entry row is a 4-column grid (title / faculty / date / takeaway) that collapses to a 2-column named-area layout under 1100px and a single column under 600px. Every descendant carries `min-width: 0`, or a long unbroken title pushes past the card edge.
- One entry is open at a time. The detail panel is unmounted when closed, so the page stays light with 68 entries on it.

## Embedding this page

WordPress renders the real site; this repo is the source. The launch plan is direct-to-disk deployment, which needs no iframe — but iframe embedding still works and is the documented fallback, so keep this snippet accurate if you rename the repo or change its Pages URL.

Paste into a **Custom HTML block** as one line. The site runs **Twenty Twenty-Five**, a block theme, and a Custom HTML block has no width control of its own — so wrap it in a **Group block set to Full width**. This is not optional for these pages: Twenty Twenty-Five's `theme.json` sets `contentSize: 645px` (`wideSize: 1340px`), so an unwrapped embed renders in a 645px column, and every full-bleed colour band in the design collapses with it:

```html
<iframe id="pm-research-compendium" src="https://pennmediated.github.io/research-compendium/" title="Research Compendium — Penn MEDIATED" loading="lazy" style="width:100%;height:14000px;border:0;display:block"></iframe><script>(function(){var f=document.getElementById('pm-research-compendium');window.addEventListener('message',function(e){if(e.source!==f.contentWindow)return;var d=e.data||{},h=d.frameHeight||(d.type==='partners-page-resize'?d.height:0);if(h)f.style.height=h+'px';});})();</script>
```

The `height` in the snippet is only the starting value. Every Penn MEDIATED page posts its real height to the parent as `{ frameHeight: <int> }` — on load, on resize, once webfonts settle, and on any `ResizeObserver` change, so expanding an entry resizes the frame. The listener in the snippet applies it. `grants-rfp` also emits an older `{ type: 'partners-page-resize', height }` message; the snippet accepts both.

The page checks `window.self === window.top` before posting, so opening it directly does nothing.

## Images and video

This applies to every image, GIF and video added to any Penn MEDIATED repo. It is written to be followed directly — by a person or by a Claude session — without further instruction.

### The one rule that is never optional

**Every `<img>` and `<video>` carries explicit `width` and `height` attributes, holding the file's real intrinsic pixel dimensions.**

```html
<img src="assets/example.webp" width="640" height="334" alt="…">
```

They do not set the display size — CSS does. They give the browser the aspect ratio *before* the file downloads, so it reserves a correctly shaped box instead of collapsing to nothing and shoving everything below it down the page as each file lands. That shift is measured by search engines (Cumulative Layout Shift) and is worse for a reader, who loses their place or clicks a link that just moved.

Every repo has a global `img, video { max-width: 100%; height: auto; display: block; }` reset, so the CSS keeps winning and the attributes only ever contribute the ratio. **Never guess the numbers** — read them off the file.

### Pick the format by what the file is

| Content | Format | Never use |
| --- | --- | --- |
| Photo, screenshot, artwork | **WebP**, quality 88 | PNG or JPEG at full camera resolution |
| Logo, wordmark, icon | **SVG** if you have it, else WebP | — |
| Anything that moves | **MP4** (H.264) + a WebP poster | **GIF, ever** |

GIF is the big one. It has no interframe compression, so a screen recording is roughly ten times the size it needs to be: `research-compendium.gif` was 11.3MB for 290 frames; the identical recording as H.264 is 1.2MB.

### Size it to the box it displays in, not to what you were sent

Find the CSS box the image renders into, then export at **2×** that width for retina. Anything beyond that is bytes the browser downloads and immediately throws away. (`gni-membership.png` was 7992px wide, rendering into a 319px box — a 470KB file doing a 33KB job.)

This repo currently ships no images. Its markup is JSX compiled in the browser by Babel, so if you add one, remember that attribute values in JSX inline styles must be quoted strings — and put `width`/`height` on the tag as usual.

If you are adding an image somewhere not listed, measure the box first (`getBoundingClientRect().width` in the browser, at a 1440px viewport) and double it.

### Commands

Stills — resize and convert in one pass:

```python
from PIL import Image
TARGET = 640                      # 2x the CSS box
im = Image.open('source.png')
w, h = im.size
if w > TARGET:
    im = im.resize((TARGET, round(h * TARGET / w)), Image.LANCZOS)
im.save('out.webp', quality=88, method=6)
print(im.size)                    # <- these are the width/height attributes
```

Animation — MP4 plus a poster frame:

```bash
ffmpeg -i source.gif -movflags +faststart -pix_fmt yuv420p \
       -vf "scale=1280:-2:flags=lanczos" -crf 24 out.mp4
ffmpeg -i source.gif -frames:v 1 -vf "scale=1280:-2:flags=lanczos" poster.png
python3 -c "from PIL import Image; Image.open('poster.png').convert('RGB').save('out-poster.webp', quality=80, method=6)"
ffprobe -v error -show_entries stream=width,height -of default=nw=1 out.mp4
```

`-crf 24` is a good default; raise it toward 30 for a smaller file, lower it toward 20 for a sharper one. `-pix_fmt yuv420p` is required for Safari and iOS.

### Markup for video

```html
<video src="assets/name.mp4" poster="assets/name-poster.webp" width="1280" height="622"
       autoplay muted loop playsinline preload="metadata" aria-label="…"></video>
```

Each attribute earns its place: `muted` is what permits autoplay at all, `playsinline` stops iOS opening it fullscreen, `poster` means the slot is never empty while the video loads, and `aria-label` replaces `alt` (a `<video>` has no `alt`).

CSS cannot stop autoplay, so **a page with video needs the reduced-motion script** at the end of `<body>`. If the page already has one, leave it alone; if you are adding the first video to a page, add it:

```html
<script>
  if (window.matchMedia('(prefers-reduced-motion: reduce)').matches) {
    document.querySelectorAll('video[autoplay]').forEach(function (v) {
      v.autoplay = false; v.pause(); v.currentTime = 0; v.removeAttribute('loop');
    });
  }
</script>
```

Also check the CSS: any rule that sizes or crops an image needs to name `video` too, or the video slot will not match the image slot it replaced (`.card__image img` becomes `.card__image img, .card__image video`).

### Before you call it done

- [ ] File is WebP, SVG or MP4 — no GIF, no full-resolution PNG or JPEG
- [ ] Its width is about 2× the CSS box it renders into
- [ ] `width`/`height` attributes match the file's real dimensions
- [ ] Real `alt` text (or `aria-label` on a video) that describes the image; empty `alt=""` only if it is purely decorative
- [ ] Lives in this repo's `assets/`, not hotlinked from another site
- [ ] Page opened in a browser at 1440px and ~400px — nothing overflows, nothing jumps on load
- [ ] Originals are not committed alongside the optimised file; git history is the backup

Do not commit an unoptimised original "just in case" — the previous commit already holds it, and a duplicate in the working tree also ships to the server.

## Hyperlinks

One taxonomy, five categories, shared by every page repo. Pick the category by what the link *is*, not by which repo you happen to be editing.

**1. In-text links** — embedded mid-sentence in flowing prose.

| ground | text | underline | hover |
| --- | --- | --- | --- |
| white / light | `--c-red-dark` | none | fade to `opacity: 0.7` |
| colour / gradient | `--c-white` | `border-bottom: 1px solid rgba(255, 255, 255, 0.5)` | fade to `opacity: 0.7` |

Both grounds use `font-weight: 500` and `transition: opacity 0.15s`, and both fade rather than change hue. On a white ground **colour is the affordance** — no underline; the underline is category 2's job. On a coloured ground the red is invisible, so the link goes white and takes the hairline rule instead. Where an underline is used it is a `border-bottom`, never `text-decoration`.

#### Why interactive red is `--c-red-dark`, not `--c-red`

`--c-red-dark` (`#df3611`) is the closing stop of `--c-gradient`, promoted to a token of its own and declared in all twelve repos.

`--c-red` (`#f03d1f`) measures roughly **3.9:1** against white — under the 4.5:1 WCAG AA threshold for body text, and the same 3.9:1 applies to white text sitting on a `--c-red` fill. `--c-red-dark` measures about **4.5:1** either way and clears it. The two are near-indistinguishable at text sizes, so this is a contrast fix, not a visual change.

**The rule: anything you click is `--c-red-dark`.** Links and buttons take it wherever they would otherwise be red-orange — as text colour, as a box fill, as a hover or active state, and on the markers inside them (disclosure chevrons and their labels). It applies in every category and every state.

**`--c-red` stays the brand accent for everything you don't click**: section headings, eyebrow and metadata labels, tag and pill backgrounds, accent bars and card borders, full-width colour bands, the `.card-arrow` hover gradient, and focus rings. These are either large text, non-text UI at the 3:1 threshold, or sit on a tinted rather than white ground.

The one deliberate hold-out is red link text on a **dark** ground (`home`'s `.footer__email`), where the darker red would *reduce* contrast rather than improve it. That link has a separate outstanding issue — on a dark ground the standard is white text with an opacity fade, not red at all.

**2. Independent links** — a standalone text link that isn't inside a sentence ("Learn More About the Center", "Download the Full Schedule"). Unlike category 1 these carry the underline and are set in the body colour, so they read as a control rather than as emphasis inside a sentence:

| ground | text | underline | hover |
| --- | --- | --- | --- |
| white / light | `--c-dark`, `font-weight: 600` | `border-bottom: 1px solid rgba(13, 13, 12, 0.35)` | text and underline both turn `--c-red-dark` (`transition: color 0.15s, border-color 0.15s`) |
| colour / gradient | `--c-white`, `font-weight: 600` | `border-bottom: 1px solid rgba(255, 255, 255, 0.5)` | fade to `opacity: 0.7` |

Plus a **thin arrow** `⟶` after the text. Use `⟶` (`&#10230;`), not the `↗` badge from category 4.

**3. Document buttons** — an independent link that opens a document (a PDF, a report). A filled button box, not text:

| ground | box | text |
| --- | --- | --- |
| white / light | `--c-red-dark` | `--c-white` |
| colour / gradient | `--c-white` | `--c-dark` |

Hover is **movement, not colour** — a lift or nudge. Do not darken or recolour the box.

**4. Links to another web page** — this site or an external one. The containing box carries the shared `.card-arrow`: a 26px dark circle with a white `↗`, in the box's top corner. On hover the arrow scales slightly and its background becomes a sliding purple-to-orange gradient (`@keyframes card-arrow-slide`), and the box itself animates. No separate text button — the whole box is the link.

**Exception:** a link to a research paper is category 2, not this — thin arrow, no badge.

*Corner:* the badge sits in the box's **top-right** corner in every repo (`about`, `home`, `data`, `team-leadership`, and this repo's convening block). A box carrying one reserves extra top padding so the badge clears its heading.

**5. Hyperlinked headings** — a heading that is itself a link (a post title, a card title). Sits in the body colour and shifts to `--c-red-dark` on hover (or fades, on a coloured ground), with **no arrow and no underline**.

### Dropdowns and disclosures

A dropdown, `<details>` block or expand/collapse control uses one affordance sitewide: a **chevron SVG** (`M2 5l5 5 5-5`, 13×13, `--c-red-dark` stroke, `stroke-width: 1.8`) beside a `--c-red-dark` label at `--fs-small`, rotating `180deg` on open with `transition: transform 0.25s`. See `llm-civic-discourse`'s "Full summary & details" toggle for the reference implementation.

Never leave the marker to the browser — style `<select>` with `appearance: none` and supply the chevron, and hide the native `<summary>` marker. The `↗` circle badge is category 4's language and does not belong on a disclosure control.

## Keeping the repos in sync

The design tokens at the top of the `<style>` block are duplicated across all thirteen repos, not shared — consistency is a discipline, not something enforced automatically. When you change a token here, check whether the same change belongs in the others before considering the task done. `home` is the style-guide reference.
