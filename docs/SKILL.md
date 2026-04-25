---
name: tahoma-css
description: Reference for tahoma.css, a pure-CSS 2000s corporate web design system. Use when building or styling an HTML page with tahoma.css — picking class names, composing the page chrome, choosing the right webpart variant, or diagnosing why output doesn't look like a 2003 SharePoint portal.
---

# tahoma.css — AI usage guide

Pure-CSS design system that makes plain HTML look like a 2003 corporate
intranet portal. Tahoma 11px body, navy gradient banners, gold CTAs, beveled
buttons, zebra tables, web parts. **No JavaScript.** No build step.

## Setup

One line in `<head>`:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title>...</title>
    <link rel="stylesheet" href="style.css" />
  </head>
  <body>
    ...
  </body>
</html>
```

Plain HTML elements (`h1`–`h6`, `p`, `a`, `table`, `input`, `button`, `pre`,
`blockquote`, `code`, `kbd`, `hr`, `fieldset`, `legend`) are styled out of
the box. Reach for the class helpers below for richer components.

## Page anatomy

A canonical tahoma.css page stacks horizontal slabs, then a 3-column grid:

```
.banner                      ← navy gradient titlebar with logo + search + user
.subnav                      ← tabs
.breadcrumb                  ← location + clock
.welcome-banner              ← optional gold greeting block
.wrap                        ← 10px outer padding
  .layout                    ← grid: 220px | 1fr | 240px
    .left-col                ← nav-list, favorites, tags
    .main-col                ← .webpart panels in a 2-up sub-grid
    .right-col               ← side webparts
.footer                      ← grey strip with copyright + meta
```

Use `.layout.two-col` (220px / 1fr) or `.layout.flipped` (1fr / 240px) for
2-column variants, or `.layout.wide` for a single full-width column.

Inside `.main-col`, webparts default to 2 columns. Add `.full` to a child to
make it span both. Add `.main-col.single-col` to stack everything.

## Component cheatsheet

| You want…           | Use                                                                                                       | Notes                                    |
| ------------------- | --------------------------------------------------------------------------------------------------------- | ---------------------------------------- |
| Top titlebar        | `.banner` + `.logo` + `.title-area` + `.banner-search` + `.user-area`                                     | One-letter logo in a gold square         |
| Tabs under banner   | `.subnav` > `.tab` (one with `.active`)                                                                   | First tab is "Home" by convention        |
| Breadcrumb          | `.breadcrumb` (use `.breadcrumb-right` floated meta)                                                      | Last segment uses `.current`             |
| Hero greeting       | `.welcome-banner` + `.w-icon` + `.w-text` + `.w-right`                                                    | Gold gradient                            |
| Footer              | `.footer` (two `<div>` children, justified)                                                               | "Best viewed in IE 6.0+" recommended     |
| Content panel       | `.webpart` > `.webpart-header` + `.webpart-body`                                                          | Default navy header                      |
| Coloured panel      | Add `.wp-orange` / `.wp-green` / `.wp-red` / `.wp-gold` / `.wp-plum` to `.webpart`                        | See "tone" below                         |
| Collapsible panel   | `<details class="webpart" open>` + `<summary class="webpart-header">`                                     | Auto `[ + ]`/`[ − ]` indicator           |
| Section divider     | `.section-heading`                                                                                        | Thin blue strip with ▸ prefix            |
| Inline notice       | `.announce` (default yellow) + optional `.red` / `.green` / `.blue` / `.gray`                             | Use inside webpart-body                  |
| Block callout       | `.callout` + same colour modifiers                                                                        | Heavier than `.announce`                 |
| Data grid           | `.corp-table` (`<table>` with `<thead>`/`<tbody>`/`<tfoot>`)                                              | Zebra rows, hover highlight              |
| Activity feed       | `.activity-table` with `<td>`s of class `.ic` `.verb` `.ttl` `.when`                                      | `.ttl > .ctx` for sub-meta               |
| Property sheet      | `.factsheet` > `.prop-table` (2-column)                                                                   | Label / value rows                       |
| Sidebar nav         | `.nav-list` with `<li class="section">` headers and `<li><a class="current">` items                       | Arrow bullets baked in                   |
| Folder tree         | `.tree-list` + `.indent-1` / `.indent-2` per `<li>`                                                       |                                          |
| To-do list          | `.task-list` > `<li>` with `.chk` (`.done` for ticked) and `.prio.hi/.med/.low`                           | Add `.done` to `<li>` for strikethrough  |
| Agenda / events     | `.event-list` > `<li>` starting with `<span class="date">` (or `.date.urgent`)                            |                                          |
| Question feed       | `.q-list` > `<li>` with `.qic`, `.q-src`, `.age`                                                          |                                          |
| Primary button      | `<button class="btn btn-primary">`                                                                        | Blue gradient                            |
| Gold CTA            | `.btn.btn-go`                                                                                             | "Go ▸" buttons                           |
| Secondary button    | `.btn` (default)                                                                                          |                                          |
| Destructive         | `.btn.btn-danger`                                                                                         |                                          |
| Toolbar icon        | `.wbtn` inside `.wysiwyg-bar`                                                                             | Hover reveals border                     |
| Table action button | `.tbtn` inside `.toolbar`                                                                                 |                                          |
| Inline blue button  | `.cbtn` (or `.cbtn.ghost`)                                                                                | For capture boxes                        |
| Form input          | bare `<input>`, `<select>`, `<textarea>`                                                                  | All styled by element selector           |
| Form layout         | `<fieldset>` > `<legend>` + `.form-row` (140px label / 1fr control)                                       | Label gets `.req` for asterisk           |
| Inline tag          | `.tag` + optional `.gold` / `.green` / `.red` / `.plum` / `.gray`                                         | UPPERCASE micro-type                     |
| Status pill         | `.status-lozenge.open` / `.pending` / `.closed` / `.danger`                                               |                                          |
| Priority pill       | `.prio.hi` / `.prio.med` / `.prio.low`                                                                    | Used in task lists                       |
| Filter chip         | `.chip` with optional `<a class="x">×</a>` to remove                                                      |                                          |
| KPI dashboard       | `.stat-grid` (4-up by default) > `.stat-cell` > `.n` (number) + `.l` (label) + `.d` (delta)               | `.cols-2/3/5` variants                   |
| Card grid           | `.shelf-grid` > `.shelf-card` > `.ic` (emoji) + `.t` (title) + `.meta`                                    | `.archived` / `.dashed` modifiers        |
| Calendar            | `.cal-head` + `.cal-table` (`<th>` weekday, `<td>` day, `.today` / `.event` / `.event.deadline` / `.off`) |                                          |
| Sparkline rows      | `.usage-table` with `<td class="bar-cell">` containing `<span class="bar" style="width:N%">`              | `.bar.gold/.green/.red/.gray`            |
| Progress bar        | `<div class="progress"><span style="width:N%"></span></div>`                                              | Inset chrome                             |
| Pull quote          | `<blockquote>` with `<cite>` (auto-styled) or `.quote`                                                    | Italic Georgia                           |
| Equation            | `.formula-block` (centred) with optional `<span class="label">`                                           |                                          |
| ASCII diagram       | `.rxn` (monospace, `white-space: pre`)                                                                    |                                          |
| Wiki cross-link     | `<a class="wikilink">` (`.broken` for missing pages)                                                      |                                          |
| Image attachment    | `.attachment` (border + drop shadow + `.filename`)                                                        |                                          |
| Comment thread      | `.comment` > `.who` + `.when`; nest with `margin-left`                                                    |                                          |
| Version history     | `.vhist` (4-col grid: version / date / who / actions)                                                     |                                          |
| Backlink list       | `.backlink-item` > anchor + `.ctx` snippet                                                                | Pair with `<mark class="hl">` highlights |
| Search hero         | `.search-hero` > `.search-bar` (`<input>` + `<button>`) + `.search-opts`                                  |                                          |
| Search facet        | `.facet` > `.facet-title` + `.facet-list` (with `.cnt` per item)                                          |                                          |
| Search result       | `.result` > `.title` + `.snippet` (`<mark>`) + `.meta`; `.featured` for hero                              |                                          |
| Pagination          | `.pagination` > `<a>`/`<span>`; `.current` for active, `.disabled` for ends                               |                                          |
| Modal-style box     | `.dialog` > `.dialog-head` (with `.x` close button) + `.dialog-body` + `.dialog-foot`                     |                                          |
| Tooltip             | `<span data-tip="text">term</span>`                                                                       | Pure CSS, hover only                     |
| Recent indicator    | `<span class="recent-dot"></span>`                                                                        | Red 8px dot                              |

## Tone & colour — when to pick which variant

**Webpart headers:**

| Variant        | Use for                                      |
| -------------- | -------------------------------------------- |
| default (navy) | Most panels — neutral content, lists, tables |
| `.wp-orange`   | Announcements, tips, news, welcome blocks    |
| `.wp-green`    | Success, completed work, positive deltas     |
| `.wp-red`      | Warnings, urgent items, deadlines, errors    |
| `.wp-gold`     | Featured / hero side panels                  |
| `.wp-plum`     | Off-menu / miscellaneous                     |

**Inline announcements:**

| Variant                    | Use for                      |
| -------------------------- | ---------------------------- |
| default (yellow `#fffce0`) | Low-urgency notes            |
| `.red`                     | Urgent, blocking, error      |
| `.green`                   | Confirmation, success        |
| `.blue`                    | Informational, system notice |
| `.gray`                    | Stale, muted, deprecated     |

## Typography

- **Body:** Tahoma 11px — applied to `<body>` automatically. Don't override.
- **Headings:** Trebuchet MS bold with subtle white text-shadow, navy ink. `h1`=22, `h2`=18, `h3`=16, `h4`=14, `h5/h6` are uppercase labels.
- **Display numbers:** wrap in `<span class="num">` for serif Georgia bold (used in stat cells, streak counters).
- **Code/keys:** `<code>`, `<kbd>`, `<pre>`, `<samp>` — Courier New 11px on cream chips.
- **Quotes:** `<blockquote>` is italic Georgia with a navy left rule.
- Don't use any web font. The point is system fonts only.

## Layout patterns

```html
<!-- Standard 3-col dashboard -->
<div class="banner">…</div>
<div class="subnav">…</div>
<div class="breadcrumb">…</div>
<div class="welcome-banner">…</div>
<div class="wrap">
  <div class="layout">
    <div class="left-col">
      <div class="webpart">…</div>
    </div>
    <div class="main-col">
      <div class="webpart full">…</div>
      <!-- spans both sub-cols -->
      <div class="webpart">…</div>
      <div class="webpart">…</div>
    </div>
    <div class="right-col">
      <div class="webpart">…</div>
    </div>
  </div>
</div>
<div class="footer">…</div>
```

```html
<!-- Two-col content page (sidebar + body) -->
<div class="wrap">
  <div class="layout two-col">
    <div class="left-col"><div class="webpart">nav</div></div>
    <div class="main-col single-col">
      <div class="webpart">content</div>
    </div>
  </div>
</div>
```

## Webpart anatomy

```html
<div class="webpart wp-orange">
  <div class="webpart-header">
    <span>📢 Title with optional emoji prefix</span>
    <span class="actions">[<a>Edit</a>] [<a>−</a>]</span>
  </div>
  <div class="webpart-body">
    Content here. Use `.webpart-body.flush` to remove padding when nesting a list, table, or feed
    that has its own padding.
  </div>
</div>
```

For collapsible:

```html
<details class="webpart" open>
  <summary class="webpart-header"><span>📁 Title</span></summary>
  <div class="webpart-body flush">…</div>
</details>
```

⚠ Don't put action links inside `<summary>` — any click toggles the panel.

## Tokens

All custom properties are namespaced `--bp-*`. Override on `:root` to
retheme without touching component rules. Most useful:

| Group    | Tokens                                                                                                                                 |
| -------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| Neutrals | `--bp-desktop`, `--bp-panel-tan`, `--bp-panel-cream`, `--bp-paper`, `--bp-paper-alt`, `--bp-paper-sunk`                                |
| Borders  | `--bp-border`, `--bp-border-soft`, `--bp-border-hard`, `--bp-border-dot`                                                               |
| Text     | `--bp-ink`, `--bp-ink-muted`, `--bp-ink-dim`, `--bp-ink-faint`                                                                         |
| Navy     | `--bp-navy`, `--bp-navy-hi`, `--bp-navy-lo`, `--bp-navy-deep`, `--bp-navy-ink`, `--bp-navy-soft`, `--bp-navy-softer`, `--bp-navy-wash` |
| Gold     | `--bp-gold-hi`, `--bp-gold-lo`, `--bp-gold-pale`, `--bp-gold-warm`, `--bp-gold-edge`, `--bp-gold-ink`                                  |
| Green    | `--bp-green-pale`, `--bp-green-hi`, `--bp-green-lo`, `--bp-green-ink`, `--bp-green-wash`                                               |
| Red      | `--bp-red-pale`, `--bp-red-hi`, `--bp-red-lo`, `--bp-red-ink`, `--bp-red-wash`, `--bp-red-dot`                                         |
| Yellow   | `--bp-yell-pale`, `--bp-yell-edge`, `--bp-yell-hot`                                                                                    |
| Fonts    | `--bp-font-ui` (Tahoma), `--bp-font-head` (Trebuchet), `--bp-font-serif` (Georgia), `--bp-font-mono` (Courier)                         |
| Sizes    | `--bp-fs-xs` 9px, `-sm` 10, `-base` 11, `-md` 12, `-lg` 14, `-xl` 16, `-2xl` 18, `-3xl` 22, `-giant` 36                                |

## Utilities (lo-fi Tailwind)

- Text: `.txt-navy`, `.txt-gold`, `.txt-green`, `.txt-red`, `.txt-muted`, `.txt-dim`, `.txt-faint`
- Background: `.bg-paper`, `.bg-tan`, `.bg-cream`, `.bg-sunk`, `.bg-yell`, `.bg-green`, `.bg-red`, `.bg-navy`
- Size: `.fs-xs/sm/md/lg/xl`
- Family: `.ff-mono`, `.ff-serif`, `.ff-head`
- Weight: `.bold`, `.italic`, `.upper`
- Align: `.text-left/right/center`
- Spacing: `.m-0`, `.p-0`, `.mt-1/2/3` (4/8/12px), `.mb-1/2/3`, `.pt-*`, `.pb-*`, `.px-1/2`, `.py-1/2`
- Flex: `.flex`, `.flex-between`, `.flex-center`, `.flex-wrap`, `.flex-1`, `.spacer`
- Grid: `.grid`, `.grid-2/3/4`
- Display: `.hidden`, `.visually-hidden`, `.inline-block`, `.block`
- Misc: `.rule` (dotted hr), `.recent-dot`, `.arrow-sep` (▸), `.mark-row` (yellow hover row), `.num` (serif display number)

## Do

- Use semantic HTML — most elements are already styled.
- Sprinkle emoji into `.webpart-header` and `.section-heading` text — it
  matches the era ("📢 Announcements", "📁 Files", "✓ Tasks").
- Use `.flex-between` for headers that have both a title and right-side actions.
- Use `<details class="webpart">` for collapsible sidebars and FAQs.
- Pair small numeric metadata with `.recent-dot` and `data-tip` tooltips.
- Use `.tag`, `.status-lozenge`, `.prio` for inline status (uppercase, terse).
- Include a `.footer` line ending with "✓ Best viewed in Internet Explorer 6.0+".
- For wide tables, wrap in a webpart-body — mobile media query already
  scrolls them horizontally below 640px.

## Don't

- Don't add `border-radius` (except on the banner logo, which already has 3px).
  Chunky right angles are the look.
- Don't introduce modern colours (slate, indigo, teal, neon). Use the
  existing navy / gold / cream / green / red palette.
- Don't use sans-serif body fonts other than Tahoma/Verdana. Don't load
  Google Fonts.
- Don't use heading sizes larger than `h1` (22px). The era was small type.
- Don't use bare `<button>` for icons — wrap them in `.wbtn`.
- Don't put action links inside `<summary>` — clicks always toggle.
- Don't use `.stack-sm` inside a CSS Grid container — it adds margin-top
  to siblings, which fights grid `gap` and misaligns the first row.
- Don't use modern shadows (`0 10px 30px rgba(0,0,0,.2)`). The system uses
  flat 1–2px hard shadows; keep that flatness.
- Don't `position: sticky` the sidebar — 2000s sites scrolled as one slab.

## Composition rules of thumb

- **Density beats whitespace.** 11px text, 4–8px padding, 1px borders.
  Pack panels close. Modern breathing room reads wrong.
- **Lots of small panels beats one big one.** A page with 8 webparts is
  more in-character than a page with 2.
- **Every list gets a header.** Use `.webpart-header` or `.section-heading`
  even for short lists.
- **Numbers go big and serif.** Wrap headline numbers in `<span class="num">`
  or use `.stat-cell .n`.
- **Status goes UPPERCASE and tiny.** Use `.tag`, `.prio`, `.status-lozenge`.
- **Time goes monospace.** Use `<code>` or the mono utility for dates,
  versions, file sizes.
- **Action affordances are explicit.** `[<a>Edit</a>] [<a>Manage</a>]` in
  `.webpart-header .actions`. Show them; don't hide behind hover-only.

## Mobile

The stylesheet has three breakpoints:

- **≤900px:** 3-col layout collapses to single col; 4-up grids drop to 2-up.
- **≤640px:** banner stacks (title → search → user); subnav scrolls
  horizontally; welcome banner stacks; form rows go label-on-top; wide
  tables scroll horizontally; webpart headers wrap actions.
- **≤420px:** stat-grid and shelf-grid drop to 1 column.

You generally don't need to do anything mobile-specific in your markup —
the breakpoints handle it. Just include the viewport meta tag.

## Files

- `style.css` — the design system itself (~1,800 lines, ~28 KB raw)
- `index.html` — comprehensive showcase of every component

## Quick gut-check

If your output has any of: rounded buttons, sans-serif headlines other
than Trebuchet, headings larger than 22px, modal overlays with backdrop
blur, gradient text, drop shadows softer than 2px, or an avatar circle —
it's not tahoma.css anymore.
