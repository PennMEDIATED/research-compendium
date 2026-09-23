# Penn MEDIATED — Research Compendium

Penn research on the quantitative study of the information ecosystem and its impact on democracy, curated and translated for journalists, media leaders, civil society organisations and policymakers. 68 entries across seven themes.

This is the rebranded replacement for [`Penn-MEDIATED/Research-Compendium`](https://github.com/Penn-MEDIATED/Research-Compendium), the version currently live at mediated.upenn.edu/research-compendium. Content is carried over unchanged; everything about how it looks and behaves is rebuilt on the sitewide standards. See "What changed from the old page" below.

## What's in this repo

- `index.html` — page markup and behaviour. Plain HTML and one plain `<script>`: no framework, no build step, no `npm install`.
- `styles.css` — design tokens first, then page CSS. Same split as `home`, `about` and `events`.
- The entries live as an `ENTRIES` array at the top of the script in `index.html`, followed by `THEME_ORDER` and `THEME_COLORS`.

Top to bottom the page is: title and intro with the newsletter panel beside it → two theme charts ("Entries by theme", "Themes over time") → the filter strip → the entry list. The charts follow the filters, and selecting a bar or a heatmap cell sets the theme (and year) filter.

## Adding or editing an entry

Copy an existing object in `ENTRIES` and fill it in. Every field is required except `importance`:

| Field | What it holds |
| --- | --- |
| `id` | Slug, unique on the page. **Also the entry's permanent link** — `mediated.upenn.edu/research-compendium/#<id>` opens that entry — so never rename it once the entry ships. |
| `title` | Paper title, plain text. |
| `url` | Where the paper lives. Drives the entry's "Read paper ⟶" link, which opens in a new tab. |
| `faculty` | Penn faculty lead, exactly as it should read. Co-leads are joined with ` & ` or ` and `; the faculty filter splits them, so each name must be spelled the same way across entries. |
| `date` | Display date, `M/D/YYYY`. |
| `year` | Integer. Drives the year filter and the default sort. |
| `themes` | Array of one or more theme names. **Must** match a key in `THEME_COLORS`, or the tag falls back to grey. |
| `takeaway` | One sentence, plain text. Shown collapsed. |
| `isNew` | `true` puts the "New" badge on the title. Remember to clear it on older entries. |
| `overview` | Trusted HTML — the long summary. |
| `importance` | Trusted HTML — the "Why is this important?" panel. Omit to hide the heading. |

`overview` and `importance` are injected as raw HTML so the Center's hand-written `<ol class="findings-list">` blocks and `<strong>` lead-ins survive. **That means these two fields are trusted input.** Paste only Center-authored copy into them; never anything a visitor or a third party supplied.

Adding a new theme means adding it to **both** `THEME_COLORS` and `THEME_ORDER` — the first gives it colours, the second puts it in the filter and the charts. A theme's `bg`, `border` and `text` are its tint, solid and text colours from the accent palette: the tag is the tint with a 1px solid border and dark text, and the solid is also the dot beside the theme in both charts.

Updating the newsletter panel: it lists the two most recent issues. Add the new one at the top of `.newsletter__list` and drop the oldest.

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

## Accent palette

The sitewide secondary colours, chosen for this page and meant to replace the per-page theme palettes in `llm-civic-discourse` and `grants-overview` (and the exploratory "Secondary colors" list in `grants`' README). Tokens are `--c-acc-N`, `--c-acc-N-tint` and `--c-acc-N-text` in `styles.css`.

| Slot | Name | Solid | Tint | Text on tint | Text on solid | Compendium theme |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | Purple (`--c-accent`) | `#5533ee` | `#ebe7fd` | `#3d3c86` | white | Political Polarization |
| 2 | Orange-red (`--c-red`) | `#f03d1f` | `#fce4dc` | `#7b2719` | black | Misinformation |
| 3 | Teal | `#2bccb4` | `#e6f9f6` | `#005b4a` | black | Social Media & Platforms |
| 4 | Magenta | `#d120a9` | `#f9e4f5` | `#6f285c` | white | Persuasion & Behavior Change |
| 5 | Berry | `#861d77` | `#f0e4ef` | `#6d2961` | white | 2020 Meta Election Project |
| 6 | Azure | `#268bfc` | `#e5f1ff` | `#0e4786` | black | LLMs & Civic Discourse |
| 7 | Green | `#1b9247` | `#e4f2e9` | `#005820` | black | Guiding the Field |
| 8 | Lilac | `#b7a0fb` | `#f6f4ff` | `#4d3680` | black | — (spare; `llm-civic-discourse` needs 8) |

- **Tag style: light, sitewide.** A tag is the tint as its fill, a 1px border in the solid, and the text colour — the same treatment as `llm-civic-discourse`. Use it for every tag in a list. Solid fills are only for a few highlight elements where there are only a handful on screen (chart dots and bars, a selected filter, `grants-overview`'s three pillar tabs); there, use the "Text on solid" column.
- **Take slots in order.** A page with three categories uses 1–3; one with eight uses all of them. That keeps the same colour meaning "first category" everywhere.
- **Tints** are each solid at 12% on white. Slots 1 and 2 land on the site's existing light purple and `--c-pale-orange`.
- **Text on a tint** clears 7:1. **Text on a solid** is white or `--c-dark`, whichever has more contrast — the "Text on solid" column.
- **Checked for colour-blind readers, every pair against every other**, not just neighbours, because an entry can carry any two themes side by side (dataviz palette validator, all-pairs: worst ΔE 9.2 under deuteranopia, 17.2 in normal vision — both pass). Don't swap one colour without re-running that check.
- Teal and lilac are pale as small marks on white (under 3:1). They pass here because every chart mark on this page sits next to its text label; don't use them as the only cue anywhere.
- `--c-red` (slot 2) is the non-clickable brand orange, so a slot-2 tag doesn't read as a link. Clickable things stay `--c-red-dark`.

## Overlap with `llm-civic-discourse` — unresolved

18 of these 68 entries carry the **LLMs & Civic Discourse** theme, and there is a separate `llm-civic-discourse` repo holding 87 papers on that same topic. Nothing is currently done about the duplication — the two pages are independent, with their own entry lists and their own theme vocabularies.

Decide before launch whether the Compendium should link out to that dashboard, drop the overlapping entries, or keep both. Whichever way it goes, the two entry lists are maintained by hand and will drift.

## Typography

Sitewide conventions, identical across every Penn MEDIATED repo:

- Two families only — `--f-serif` (EB Garamond) and `--f-sans` (DM Sans). No monospace face anywhere.
- **The split is by what the text *is*, not by heading level.** Serif takes page titles and the titles of works or names of people; sans takes section headings, card and UI labels, running prose, metadata and controls. **A section heading is not serif.** Here that means `.intro__title` (the page) and `.entry__title` (a paper — a work) are EB Garamond, while `.entry__detail h4` ("Overview", "Why is this important?") is DM Sans, because those label a section rather than name a work.
- **Serif titles are weight 600**, sitewide and without exception.
- **Measure is capped per container, and the numbers differ on purpose.** A `max-width` on body copy is a reading-comfort cap (~65-75 characters), not a layout width, so it depends on how wide the container already is — `events`' `.event-card__desc` caps at 560px because its grid is two columns, `blog`'s `.post-excerpt` at 720px because its feed is one full-width column. Both land the same line length. Don't "align" two such numbers.
- Uppercase micro-labels ("Key takeaway", "Center newsletter", the theme chips) are DM Sans 700 uppercase at `--fs-micro`.
- **12px is the floor.** Nothing on the page ships smaller — the old page had four sizes below it.
- Heading scale at desktop: 56 / 40 / 24px (`--fs-h1` / `--fs-h2` / `--fs-h3`). The clamps interpolate across the viewport, so tablet needs no separate breakpoint.

## Layout

- One `.wrap` handles the page width: 1440px cap, 80px side padding, stepping to 32px under 900px and 20px under 480px.
- The filter strip sits on `--c-light-bg` and spans the full viewport width; the wrap goes inside it, never around it. Same rule as every coloured section sitewide.
- The entry row is a 4-column grid (title / faculty / date / takeaway) that collapses to a 2-column named-area layout under 1100px and a single column under 600px. Every descendant carries `min-width: 0`, or a long unbroken title pushes past the card edge.
- An open entry's summary sits on `--c-light-bg` as three same-shaped cards: Overview on light purple (`--c-acc-1-tint`), "Why is this important?" on white with the brand-gradient top edge (its heading is EB Garamond 600 — a deliberate exception to the sans section-heading rule), and Key findings on `--c-pale-orange`; text is `--c-dark` in all three. The Overview/Why column split is set per entry from the two boxes' text lengths (`overviewShare()`, clamped 0.6–3×) so they end close in height, and the shorter one stretches to match; entries past the clamp keep natural heights rather than leave a mostly empty box. The Overview is on the left and "Why is this important?" as a raised card on the right, topped with the brand gradient (the card stacks below the Overview under 900px; entries without `importance` get the Overview full width). When an overview's list is introduced by a findings lead-in ("Key findings include:", "Here's what they found:", …), the list moves into its own full-width **Key findings** section below that row (one numbered column) and the lead-in sentence is dropped, since the heading replaces it; the pattern is `FINDINGS_LEAD` in the script. A list introduced any other way stays inside the Overview. Either way items are numbered in the sitewide ordinal style: `01`, DM Sans 800, `--c-red`, baseline-aligned (same as `grants` / `grants-rfp`).
- One entry is open at a time. The detail panel is only rendered while open, so the page stays light with 68 entries on it.
- A column header row ("Title / Penn faculty lead / Date / Key takeaway") sits above the list on the same 4-column grid as the entries. Under 1100px it's hidden and each entry shows small "Penn faculty lead" and "Date" labels above those values instead.
- Faculty names link to their profile on `team-faculty` (`mediated.upenn.edu/team-faculty/#<id>`, opened in a new tab). They're set in the body colour and turn `--c-red-dark` on hover. The name → id map is `FACULTY_IDS` in the script; **add a line there when a new faculty lead appears**, or their name shows as plain text. Co-leads link separately.
- The top of each entry is a plain container (it holds those links, and a link can't sit inside a `<button>`). Clicking anywhere in it still opens or closes the entry; the keyboard control is the footer's "Full summary & details" / "Show less" button.
- Each entry ends with a footer row: "Read paper ⟶" (category 2), "Copy link" and the "Full summary & details" toggle on the left, the theme tags on the right under the takeaway column (they drop below, left-aligned, on phones). Opening the entry puts the summary above that footer, so the same toggle — now "Show less" — stays at the bottom and closing it scrolls back to the top of the entry.
- The charts can be hidden with the "Hide theme charts" disclosure above them (sitewide chevron style). They're open by default; a visitor's choice is remembered in their browser (`localStorage`, key `pm-compendium-charts`) where storage is allowed, and the frame height follows automatically.
- The two charts sit side by side above 900px and stack below it (each capped at 720px so the bars don't stretch across a tablet). Under 600px their row labels wrap to fit a phone.
- The filter strip is a single row on desktop and becomes an even grid under 1100px (search on its own row, then the four dropdowns) and a two-column grid under 600px.
- No dark mode, on purpose: the page sits inside a white WordPress page, and a frame that followed the visitor's OS theme would render as a dark block in it.

## Embedding this page

WordPress renders the real site; this repo is the source. The launch plan is direct-to-disk deployment, which needs no iframe — but iframe embedding still works and is the documented fallback, so keep this snippet accurate if you rename the repo or change its Pages URL.

Paste into a **Code module** — not a Text module, which mangles iframes and scripts. Two things have to be set, and they deliberately live in different places.

**Per page, in the builder.** The site runs **Divi 5**, where width belongs to the row, not to the module. A Divi 5 row ships at **width 80%, max-width 1080px**, so an untouched embed renders in a narrow column and every full-bleed colour band in the design collapses with it. Set:

- Row → Design → Sizing → **Width 100%** and **Max Width `none`** — `none`, not 100%
- Section → Design → Spacing → **padding 0** top and bottom
- Row → Design → Spacing → **padding 0** top and bottom

These are design settings, so they belong where the next person will look for them. Putting the width in CSS instead leaves the builder showing 80% / 1080px while the page renders full width, and that mismatch costs someone an afternoon eventually.

**Once, sitewide.** Divi has no setting for the last problem: an `<iframe>` is `display: inline` by default, so it sits on a text baseline and leaves a 4–6px gap underneath that nothing in the builder accounts for. Add this once under Divi → Theme Options → Custom CSS and no page needs it again:

```css
.et_pb_code iframe { display: block; width: 100%; border: 0; }
```

It is keyed to `.et_pb_code` rather than a per-section class on purpose — every iframe on this site sits in a Code module, so there is no hook to add and nothing to remember when page fourteen arrives. Divi's own Video and Map modules don't use Code modules, so a collision is unlikely; if someone does add a Code-module embed that shouldn't be full width, give that one its own override rather than reintroducing a class here.

Divi caches its compiled CSS to a static file, so clear that cache (Divi → Theme Options → Builder → "Clear Divi Static CSS File Cache") after editing Custom CSS, or the change will not show for visitors.

On Divi 4 this was all different: a **Fullwidth Section** holding a **Fullwidth Code** module, with separate CSS ID and CSS Class fields on the Advanced tab. Divi 5 removed the section-type chooser (the add-section button offers flex and grid layout options now) and folded ID and class into Advanced → **Attributes**, so ignore Divi 4 tutorials on both points. The embed snippet itself:

```html
<iframe id="pm-research-compendium" data-src="https://pennmediated.github.io/research-compendium/" title="Research Compendium — Penn MEDIATED" scrolling="no" allow="clipboard-write" style="width:100%;height:14000px;border:0;display:block"></iframe><script>(function(){var f=document.getElementById('pm-research-compendium');f.src=f.getAttribute('data-src')+location.hash;window.addEventListener('message',function(e){if(e.source!==f.contentWindow)return;var d=e.data||{},h=d.frameHeight||(d.type==='partners-page-resize'?d.height:0);if(h)f.style.height=h+'px';if(typeof d.frameScrollTo==='number')window.scrollTo({top:f.getBoundingClientRect().top+window.pageYOffset+d.frameScrollTo-120});});window.addEventListener('hashchange',function(){f.contentWindow.postMessage({pmHash:location.hash},'*');});})();</script>
```

The `height` in the snippet is only the starting value. Every Penn MEDIATED page posts its real height to the parent as `{ frameHeight: <int> }` — on load, on resize, once webfonts settle, and on any `ResizeObserver` change, so expanding an entry resizes the frame. The listener in the snippet applies it. `grants-rfp` also emits an older `{ type: 'partners-page-resize', height }` message; the snippet accepts both.

The page checks `window.self === window.top` before posting, so opening it directly does nothing.

### Entry links ("Copy link")

"Copy link" copies `https://mediated.upenn.edu/research-compendium/#<entry id>` (the address is `PAGE_URL` in the script). Opening it expands that entry and scrolls to it. A cross-origin iframe can't see the WordPress page's address, so the snippet above does three extra things, and all three matter:

- `src` is set from `data-src` **plus the WordPress page's `#hash`**, so the frame loads already knowing which entry to open. (That is also why the snippet has no `loading="lazy"` — a lazy frame wouldn't load until scrolled to.)
- A later `#hash` change on the WordPress page is forwarded into the frame as `{ pmHash }`.
- When the page opens an entry it posts `{ frameScrollTo: <px> }`, and the snippet scrolls the WordPress page to it. The `- 120` leaves room for the site header; change it if the header height changes.

`allow="clipboard-write"` lets the frame use the Clipboard API; without it Chrome refuses clipboard writes from a cross-origin frame. The page also falls back to the older copy command, but keep the attribute.

**Replacing an older embed:** the previous snippet had none of this, so entry links opened the page at the top. Paste the whole new snippet over the old one in the Code module.

Opened directly (not embedded), the page reads its own `#hash`, so `pennmediated.github.io/research-compendium/#<id>` works too.

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

This repo currently ships no images. If you add one, put `width`/`height` on the tag as usual.

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
