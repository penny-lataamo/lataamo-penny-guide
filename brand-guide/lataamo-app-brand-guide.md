---
version: alpha
name: Lataamo App Brand Guide
description: Minimal Lataamo brand and UI system for AI-assisted app development.
colors:
  primary: "#D70376"
  secondary: "#FF6B35"
  ink: "#111111"
  body: "#3F3A3D"
  white: "#FFFFFF"
  surface: "#FFFFFF"
  line: "#E6E0E3"
typography:
  h1:
    fontFamily: Montserrat, Inter, system-ui, sans-serif
    fontSize: 2rem
    fontWeight: 800
    lineHeight: 1.15
    letterSpacing: "-0.02em"
  body-md:
    fontFamily: Montserrat, Inter, system-ui, sans-serif
    fontSize: 1rem
    fontWeight: 400
    lineHeight: 1.55
rounded:
  sm: 8px
  md: 12px
  lg: 16px
spacing:
  xs: 4px
  sm: 8px
  md: 16px
  lg: 24px
  xl: 32px
components:
  button-primary:
    backgroundColor: "{colors.primary}"
    textColor: "{colors.white}"
    rounded: "{rounded.md}"
    padding: 10px 14px
  card:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.ink}"
    rounded: "{rounded.lg}"
    padding: 20px
---

# Lataamo app brand guide for AI developers

Updated: 2026-05-25  
Audience: AI developers building internal tools, dashboards, client portals, prototypes and event-production apps for Lataamo.  
Status: Minimal implementation guide and token system, not a full official visual identity manual.

## 1. What changed in v2

This version corrects the first example page: the previous display headline was too large for a normal app. Lataamo can still use bold brand expression, but **web apps need functional hierarchy, predictable spacing, density control and accessible defaults**.

Key updates:

- App-first typography scale: page headings around `28–36px`, section headings `20–24px`, body `14–16px`.
- Both **light and dark mode** are defined with the same semantic tokens.
- The system is organized for developers: primitives → semantic tokens → components → templates.
- The gradient remains a brand accent, not the default surface for every element.
- The example page is now a component/template lab rather than a campaign-style landing page.
- Published example pages now include a template switcher dropdown for approved template families only; light/dark mode lives inside each template as its own toggle.

## 2. Research basis for app UI decisions

The implementation rules below follow common web-app design-system patterns:

- **Typography should be optimized for software UI density, not poster scale.** Shopify Polaris notes that its type scale is tailored for UI usage and high-density layouts with complex features; line heights align with a 4px grid. Source: https://polaris.shopify.com/design/typography/font-and-typescale
- **Layout and spacing need a consistent grid system.** Material Design documents grids and spacing as foundation-level layout primitives. Source: https://m3.material.io/foundations/layout/grids-spacing/overview
- **Accessible contrast is non-negotiable.** WCAG 2.2 AA requires at least `4.5:1` contrast for normal text and `3:1` for large-scale text. Source: https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum.html
- **App design should use semantic color roles.** Polaris color tokens separate background, surface, text, border, hover and inverse roles rather than hard-coding brand colors everywhere. Source: https://polaris.shopify.com/tokens/color

Practical interpretation for Lataamo apps: keep the brand energetic, but make operational screens readable, modular and maintainable.

## 3. Brand in one sentence

Lataamo Creative is a bold, emotional and action-oriented event agency: **"tekojen toimisto"** — creating moments where creativity and emotion meet, experiences that stay in memory and move business forward.

For apps this means: **clear, energetic, human, polished and action-oriented — not generic blue SaaS, not campaign-poster UI, not low-contrast decoration.**

## 4. Logo assets

Recommended public assets:

- **Preferred transparent gradient brandmark for apps/loaders:** https://penny-lataamo.github.io/lataamo-penny-guide/assets/lataamo-brandmark-transparent.png
- **Public gradient brandmark / icon fallback:** https://www.lataamo.fi/hubfs/Lataamo_Creative_RGB-merkki-liuku_400x400px.png
- **SVG brandmark fallback:** https://www.lataamo.fi/hubfs/lataamo-brandmark.svg
- **Transparent gradient brandmark for app loaders:** https://penny-lataamo.github.io/lataamo-penny-guide/assets/lataamo-brandmark-transparent.svg
- **Footer / wordmark asset visible on current site:** https://50465574.fs1.hubspotusercontent-na1.net/hub/50465574/hubfs/Logo_footer.webp?width=265&height=67&name=Logo_footer.webp

Usage rules:

- Keep clear space around the logo: at least `24px` in normal headers, `12px` in compact app chrome.
- Do not stretch, recolor, outline or add effects to the logo.
- Use the transparent gradient brandmark for app icons, favicons, compact nav, avatars and loaders.
- Use the wordmark/full logo in login screens, public-facing headers and documents when space allows.
- In dark mode, place the logo on a calm dark surface; do not put it directly over noisy photos or full-strength gradients unless contrast is controlled.

## 5. Design-system architecture

Build the Lataamo app UI as a small token system, not one-off CSS.

```text
brand primitives
  raw colors, gradient, logo URLs, font families
      ↓
semantic tokens
  background, surface, text, muted text, border, action, focus, danger, success
      ↓
component tokens
  button, input, card, badge, table, nav, alert
      ↓
templates
  dashboard, form page, data table page, detail page, empty state, modal
```

Rules for devs:

1. **Never hard-code brand colors inside components.** Components use semantic variables like `--color-action-bg` and `--color-surface`.
2. **Theme changes happen in one place.** Light/dark mode overrides semantic tokens with `[data-theme="dark"]`.
3. **Templates compose components.** A new dashboard or form should not invent button/table/card styles again.
4. **The gradient is a primitive.** Use it through component or utility classes like `.accent-strip`, `.button-accent`, `.active-indicator`.
5. **Accessibility lives in tokens.** Default text/background and default button pairs must pass WCAG AA for normal text.

Suggested file structure:

```text
src/styles/
  lataamo.tokens.css        # raw + semantic CSS variables, light/dark
  lataamo.components.css    # buttons, cards, forms, badges, tables, nav
  lataamo.templates.css     # dashboard/form/detail/page templates
src/components/
  Button.tsx
  Card.tsx
  Field.tsx
  Badge.tsx
  DataTable.tsx
  AppShell.tsx
src/templates/
  DashboardTemplate.tsx
  FormTemplate.tsx
  DetailTemplate.tsx
```

## 6. Core primitives

```css
:root {
  /* Brand primitives */
  --brand-orange: #FF6B35;
  --brand-orange-deep: #FF5500;
  --brand-magenta: #EC0382;
  --brand-magenta-deep: #D70376;
  --brand-gradient: linear-gradient(135deg, #FF6B35 0%, #FF5500 30%, #EC0382 70%, #D70376 100%);

  /* Typography */
  --font-heading: Montserrat, Inter, system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
  --font-body: Montserrat, Inter, system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;

  /* Layout */
  --space-1: 4px;
  --space-2: 8px;
  --space-3: 12px;
  --space-4: 16px;
  --space-5: 20px;
  --space-6: 24px;
  --space-8: 32px;
  --space-10: 40px;

  --radius-sm: 8px;
  --radius-md: 12px;
  --radius-lg: 16px;
  --radius-xl: 22px;
  --radius-pill: 999px;
}
```

## 7. Semantic theme tokens

Use these tokens in actual components.

```css
:root,
[data-theme="light"] {
  color-scheme: light;
  --color-bg: #F7F4F2;
  --color-surface: #FFFFFF;
  --color-surface-raised: #FFFFFF;
  --color-surface-subtle: #FFF1EA;
  --color-text: #111111;
  --color-text-muted: #5F565B;
  --color-text-soft: #82777D;
  --color-border: #E6E0E3;
  --color-border-strong: #CFC5CB;
  --color-action-bg: #D70376;
  --color-action-bg-hover: #B90263;
  --color-action-text: #FFFFFF;
  --color-secondary-bg: #FFFFFF;
  --color-secondary-bg-hover: #FFF1EA;
  --color-secondary-text: #111111;
  --color-secondary-border: #B9AAB2;
  --color-link: #B90263;
  --color-focus: rgba(215, 3, 118, 0.28);
  --shadow-card: 0 14px 34px rgba(17, 17, 17, 0.08);
}

[data-theme="dark"] {
  color-scheme: dark;
  --color-bg: #111012;
  --color-surface: #1A171B;
  --color-surface-raised: #231F24;
  --color-surface-subtle: #2B1724;
  --color-text: #F7F3F5;
  --color-text-muted: #C9BDC4;
  --color-text-soft: #9D9098;
  --color-border: rgba(255, 255, 255, 0.12);
  --color-border-strong: rgba(255, 255, 255, 0.20);
  --color-action-bg: #EC0382;
  --color-action-bg-hover: #FF2A9B;
  --color-action-text: #FFFFFF;
  --color-secondary-bg: #332B34;
  --color-secondary-bg-hover: #433846;
  --color-secondary-text: #FFFFFF;
  --color-secondary-border: rgba(255, 255, 255, 0.32);
  --color-link: #FF7ABF;
  --color-focus: rgba(236, 3, 130, 0.38);
  --shadow-card: 0 18px 46px rgba(0, 0, 0, 0.35);
}
```

## 8. Typography for apps

Do not use enormous campaign headings inside product UI. Use this scale by default:

| Role | Size | Weight | Line height | Use |
|---|---:|---:|---:|---|
| Page title | `32px` desktop / `28px` mobile | `800` | `1.15` | Main app page title |
| Section title | `22px` | `800` | `1.2` | Card groups, form sections |
| Card title | `18px` | `800` | `1.25` | Cards, panels |
| Body | `15–16px` | `400–600` | `1.5–1.6` | Reading text |
| UI label | `13–14px` | `700–800` | `1.3` | Forms, table headers, nav |
| Caption/meta | `12–13px` | `600–700` | `1.35` | Supporting metadata |

Brand expression rule:

- Use larger visual type only on login/landing/marketing surfaces.
- In operational apps, the user needs orientation and action, not a poster.
- Uppercase can work for small labels, not long headings or paragraphs.

Recommended CSS:

```css
.page-title {
  font: 800 clamp(1.75rem, 2vw, 2rem) / 1.15 var(--font-heading);
  letter-spacing: -0.02em;
}
.section-title {
  font: 800 1.375rem / 1.2 var(--font-heading);
  letter-spacing: -0.01em;
}
.body { font: 400 1rem / 1.55 var(--font-body); }
.label { font: 800 .8125rem / 1.3 var(--font-body); }
```

## 9. Layout rules

- Use a `12-column` responsive grid for complex dashboards; simple pages can use `1–2 columns`.
- Use `4px` as the micro-grid and `8px` as the primary spacing base.
- Default app content width: `1120–1280px`.
- Default page padding: `24px` desktop, `16px` mobile.
- Card padding: `16–24px`, depending on density.
- Keep data tables calm and readable; reserve the gradient for selection/active/accent, not every row.
- Use one primary action per view.

### Mobile-first rules for AI developers

The example page is deliberately mobile-optimized because AI developers copy patterns from examples. Every Lataamo app template must work on phones as well as desktop.

- Design mobile from the start, not as an afterthought.
- Header/navigation must wrap or collapse cleanly; never allow horizontal scrolling from nav/actions.
- Cards, metric grids, forms, charts, dialogs and tables must become single-column or horizontally contained on narrow screens.
- Touch targets should be at least `40–44px` high.
- Toolbars and action rows should wrap, with primary action first or full-width where useful.
- Tables need an overflow container or stacked mobile pattern; do not let columns break the page width.
- Charts should scale to the container and avoid fixed pixel widths.
- Test at `375px`, `430px`, tablet and desktop widths before shipping.

## 10. Component guidance

### Buttons

Primary action uses a solid accessible magenta by default. The gradient is available for high-emphasis brand moments.

```css
.button {
  min-height: 40px;
  border-radius: var(--radius-md);
  padding: 0 14px;
  font: 800 14px / 1 var(--font-body);
  border: 1px solid transparent;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
}
.button-primary {
  background: var(--color-action-bg);
  color: var(--color-action-text);
}
.button-primary:hover { background: var(--color-action-bg-hover); }
.button-accent { background: var(--brand-gradient); color: #fff; }
.button-secondary {
  background: var(--color-secondary-bg);
  color: var(--color-secondary-text);
  border-color: var(--color-secondary-border);
  box-shadow: 0 1px 0 color-mix(in srgb, var(--color-text) 8%, transparent);
}
.button-secondary:hover {
  background: var(--color-secondary-bg-hover);
  border-color: var(--color-action-bg);
}
.button:focus-visible {
  outline: 3px solid var(--color-focus);
  outline-offset: 2px;
}
```

Use:

- `button-primary` for default save/generate/continue actions.
- `button-accent` for one highlighted brand action per screen, such as `Create concept`.
- `button-secondary` for cancel/back/filter/export.
- Secondary buttons must still look like controls. Do not make them visually identical to the surrounding card or app chrome. Give them a visible boundary, distinct background/hover state and high-contrast text in both light and dark mode.

### Cards

```css
.card {
  background: var(--color-surface);
  color: var(--color-text);
  border: 1px solid var(--color-border);
  border-radius: var(--radius-lg);
  box-shadow: var(--shadow-card);
  padding: var(--space-5);
}
.card-accent { position: relative; overflow: hidden; }
.card-accent::before {
  content: "";
  position: absolute;
  inset: 0 0 auto 0;
  height: 4px;
  background: var(--brand-gradient);
}
```

### Forms

```css
.field label {
  display: block;
  margin-bottom: 6px;
  color: var(--color-text);
  font: 800 13px / 1.3 var(--font-body);
}
.input, .select, .textarea {
  width: 100%;
  min-height: 40px;
  border: 1px solid var(--color-border);
  border-radius: var(--radius-md);
  background: var(--color-surface-raised);
  color: var(--color-text);
  padding: 10px 12px;
  font: 500 14px / 1.4 var(--font-body);
}
.input:focus, .select:focus, .textarea:focus {
  outline: 3px solid var(--color-focus);
  border-color: var(--color-action-bg);
}
```

### Tables

- Header text: `12–13px`, uppercase optional, high contrast.
- Row text: `14px` for dense operational data.
- Use subtle borders and hover states.
- Do not use gradient table headers in data-heavy views; it reduces readability.

### Badges and status

Use semantic colors for operational status. Use brand colors only for brand/category tags.

```css
.badge {
  border-radius: var(--radius-pill);
  padding: 4px 8px;
  font: 800 12px / 1 var(--font-body);
  border: 1px solid var(--color-border);
}
.badge-brand {
  color: var(--color-link);
  background: color-mix(in srgb, var(--color-action-bg) 14%, var(--color-surface));
  border-color: color-mix(in srgb, var(--color-action-bg) 45%, var(--color-border));
}
.badge-success { background: #E7F6EE; color: #0A5B41; }
.badge-warning { background: #FFF1D6; color: #7A4300; }
```

### Navigation

- App shell: logo left, primary sections center/left, user/actions right.
- Active state can use a gradient underline or small gradient pill.
- Keep nav labels short: `Dashboard`, `Concepts`, `Vendors`, `Reports`, `Settings`.

## 11. Templates developers should create

Create templates as composable layouts. Each template should use the same `AppShell`, `PageHeader`, `Card`, `Button`, `Field`, `Badge` and `DataTable` primitives.

### Dashboard template

Use for overviews and operational command centers.

Required slots:

- `PageHeader` with title, description, primary action
- `MetricGrid`
- `MainColumn` cards
- `SidePanel` for next actions or alerts
- Optional `DataTable`

### Form / generator template

Use for brief intake, concept generation and AI-assisted workflows.

Required slots:

- `StepTabs` or progress indicator
- Form sections with grouped fields
- Sticky or clearly placed action bar
- Preview/result panel

### Detail template

Use for event, vendor, concept or report detail pages.

Required slots:

- Title + metadata badges
- Summary card
- Tabbed detail sections
- Activity/notes panel
- Related actions

### Data table template

Use for vendor lists, tasks, budgets and comparisons.

Required slots:

- Filter/search row
- Table with readable columns
- Status badges
- Row actions
- Empty state

## 12. Light and dark mode implementation

Preferred implementation:

```html
<html data-theme="light">
```

Toggle by changing the attribute:

```js
const root = document.documentElement;
const next = root.dataset.theme === 'dark' ? 'light' : 'dark';
root.dataset.theme = next;
localStorage.setItem('theme', next);
```

Rules:

- Components must not know whether they are in light or dark mode.
- Components only use semantic tokens.
- Test every screen in both modes.
- Avoid pure white text on pure black for long reading; use softened theme tokens.

## 13. Voice in apps

Tone: direct, energetic, useful, human.

Good UI copy:

- `Turn brief into action`
- `Build the participant journey`
- `What should people remember?`
- `Next production step`
- `Ready for client review`

Avoid:

- `Submit data`
- `Click here`
- `AI-powered seamless solution`
- Generic chatbot filler such as `Certainly!`

## 14. Example page

A standalone implementation example is published on GitHub Pages:

https://penny-lataamo.github.io/lataamo-penny-guide/brand-guide/

The page demonstrates:

- App-scale heading hierarchy
- Light/dark theme switch
- App shell navigation
- Page header
- Primary, secondary and gradient buttons with visible secondary states
- Cards and metric tiles
- Form fields
- Tabs
- Table
- Badges, tags and filter chips with stronger visibility
- Alerts and high-notice toasts
- Empty state
- Skeleton loading plus a branded Lataamo logo loader
- Charts, modals, sidebar/filter patterns, files, avatars and activity feed
- Template notes for dashboard/form/detail/table patterns

## 15. Quick checklist for AI developers

Before shipping a Lataamo app screen:

- [ ] Uses semantic tokens, not hard-coded colors.
- [ ] Works in both light and dark mode.
- [ ] Works at mobile widths (`375px`/`430px`) with no horizontal overflow.
- [ ] Page title is app-sized, not poster-sized.
- [ ] Body text and buttons pass WCAG AA contrast.
- [ ] One clear primary action per view.
- [ ] Gradient is used as accent/emphasis, not everywhere.
- [ ] Components are reusable and template-friendly.
- [ ] Tables and forms remain calm and readable.
- [ ] Copy is action-oriented and human, not generic AI/SaaS filler.

## 16. Source notes

User-provided source of truth:

- Required gradient: `linear-gradient(135deg, #FF6B35 0%, #FF5500 30%, #EC0382 70%, #D70376 100%)`
- Requirement: minimal easy-to-understand MD file for AI app developers.
- Requirement: example page with regular app elements.
- Requirement update: app-scale UI, light/dark mode and a system that makes future changes/templates easy for devs.
- Requirement update: toasts must be more noticeable than surrounding UI, tags/chips must not be invisible, loaders should use the logo creatively alongside skeletons, secondary buttons must follow proper contrast/control-visibility rules, and example screens must be mobile-optimized.
- User-provided transparent logo asset should be preferred in app examples and loader patterns.

Observed public Lataamo source:

- Public website: https://www.lataamo.fi/
- Logo asset URLs listed in this guide.
- Public site typography observed from CSS: Big Shoulders / Big Shoulders Text for expressive headings and Montserrat for body. For apps, this guide simplifies to Montserrat/Inter-first because app UI needs readability and density more than campaign-display expression.

## 17. Additional app elements and data visualization

Lataamo apps will often need more than forms and cards. Use the same token system for operational elements so developers can create new screens without reinventing styling.

### Charts and graphs

Charts should be **clear first, branded second**. Use brand colors for emphasis, not for every series.

Recommended chart palette:

```css
:root {
  --chart-primary: #D70376;
  --chart-secondary: #FF6B35;
  --chart-tertiary: #7A3EF0;
  --chart-success: #12805C;
  --chart-warning: #B35C00;
  --chart-grid: var(--color-border);
  --chart-axis: var(--color-text-soft);
  --chart-label: var(--color-text-muted);
}
[data-theme="dark"] {
  --chart-primary: #FF5BAE;
  --chart-secondary: #FF8A5C;
  --chart-tertiary: #B79CFF;
  --chart-success: #7DDCB4;
  --chart-warning: #FFD28C;
}
```

Graph rules:

- Use `--chart-primary` for the most important series only.
- Use muted grid lines; never use heavy black grid lines.
- Put labels close to the data where possible.
- Avoid rainbow palettes. If more than 4 series are needed, use grouping/filtering instead.
- For positive/negative operational status, use semantic success/warning/danger colors, not brand magenta.
- For gradients in charts, use transparent fades under area charts only; do not make every bar a gradient.
- Tooltips should use the normal card/surface tokens.

Common chart types:

| Chart | Recommended Lataamo treatment |
|---|---|
| Line chart | Thin `2px` line, primary magenta for main series, muted comparison lines. |
| Bar chart | Rounded `6px` bars, single brand color for selected/highlight bar, neutral bars for the rest. |
| Area chart | Subtle magenta-to-transparent fill under one main line. |
| Donut chart | Use only for simple distribution, max 5 slices, center label for total. |
| KPI sparkline | Tiny line with no axis, used inside metric cards. |
| Progress | Use solid action color or gradient for one-off brand emphasis. |

### Modals and dialogs

Use modals for confirmation, focused editing and destructive actions. Do not use a modal for every form.

- Overlay: `rgba(17, 16, 18, .58)` in light mode, `rgba(0, 0, 0, .72)` in dark mode.
- Dialog max width: `480–640px` for normal tasks.
- Header: app-scale `20–22px`, not campaign display type.
- Primary action right, secondary action left/next to it.
- Destructive action should use danger styling, not brand gradient.

### Toasts and notifications

Use toasts for non-blocking feedback, but make them unmistakably separate from the surrounding UI. A toast is an interruptive transient message, so it needs elevation, position and a visible semantic accent.

- Place toasts in a dedicated stack, normally top-right or bottom-right of the viewport on desktop and full-width/inset on mobile.
- Use a raised surface, stronger border, clear shadow and a `4–5px` semantic left border or top stripe.
- Success: semantic green.
- Warning: semantic amber.
- Error: semantic red.
- Brand/info: magenta accent for Lataamo-specific system notes.
- Keep text short: one sentence plus optional action.
- Do not style toasts exactly like cards, table rows or normal list items; users will miss them.

### Sidebars and filters

Many Lataamo tools will need vendor filters, event filters and workspace navigation.

- Sidebar width: `240–280px` desktop.
- Use subtle active state with gradient left border or underline.
- Keep filter groups collapsible when there are more than 5–6 controls.
- Filter chips should be removable and readable in both themes.
- Chips/tags need a visible border and enough fill contrast to read as selected metadata, not faint decoration. Use brand-tinted chips for active filters and neutral bordered chips for passive metadata.

### Avatars, file cards and timeline/activity

- Avatars can use initials on a brand-gradient background when no photo exists.
- File cards should show file type, title, modified date and primary action.
- Timeline/activity items should use small status dots and calm borders; avoid turning every item into a large card.

### Skeleton/loading states

Loading states should use neutral shimmer/skeleton surfaces. Avoid animated full-gradient skeletons; they feel noisy and make the app look unstable.

Use two loading patterns:

1. **Skeletons** for preserving layout while content loads.
2. **Lataamo logo loader** for short full-panel waits, AI generation, upload/processing and branded empty-to-result transitions. Use the transparent-gradient brandmark asset and keep it small and calm: rotate or gently pulse the logo itself; do not spin a heavy decorative element around the logo.

```css
.skeleton {
  border-radius: var(--radius-sm);
  background: linear-gradient(90deg,
    color-mix(in srgb, var(--color-border) 45%, transparent),
    color-mix(in srgb, var(--color-border) 20%, transparent),
    color-mix(in srgb, var(--color-border) 45%, transparent)
  );
  background-size: 220% 100%;
  animation: skeleton 1.4s ease-in-out infinite;
}
@keyframes skeleton { to { background-position-x: -220%; } }

.logo-loader {
  width: 56px;
  height: 56px;
  position: relative;
  display: grid;
  place-items: center;
}
.logo-loader::before {
  content: "";
  position: absolute;
  inset: -4px;
  border-radius: 18px;
  background: var(--brand-gradient);
  opacity: .12;
  filter: blur(1px);
}
.logo-loader img {
  position: relative;
  width: 44px;
  height: 44px;
  padding: 0;
  background: transparent;
  box-shadow: none;
  animation: logo-spin 1.25s cubic-bezier(.55,.08,.35,1) infinite;
  transform-origin: center;
}
@keyframes logo-spin {
  0% { transform: rotate(0deg) scale(1); }
  72% { transform: rotate(360deg) scale(1.04); }
  100% { transform: rotate(360deg) scale(1); }
}
```

## 16. Learnings from the 2026-05 template stress test

A second example page was created from a soft grey / frosted-glass dashboard reference: https://penny-lataamo.github.io/lataamo-penny-guide/brand-guide-sense/

Key learnings:

1. **The brand system should support multiple moods, not one fixed look.** The same Lataamo primitives — logo, orange/magenta gradient, action-first copy and semantic components — can produce both a sharper SaaS-like UI and a softer glass/neumorphic UI.
2. **Tokens matter more than screenshots.** The successful variant kept the gradient as a primitive and reused component roles: surface, border, shadow, action, focus, badge, table, chart and loader. This makes the style transferable to new apps.
3. **Mood can change through surfaces, radii and shadows.** The soft variant used pale warm-grey background, translucent panels, large radii, white borders, inset fields and gentle shadows. It did not need new brand colors.
4. **The Lataamo gradient works best as emphasis.** In the soft style it is strongest in CTAs, progress, chart lines, small badges, abstract panels and logo moments — not as a full-page wash.
5. **Reference-inspired pages must still remain app systems.** The page should not clone the reference subject matter. It should translate the visual posture into Lataamo-relevant dashboard, form, table, modal, toast, file, loading and activity examples.
6. **Every template should include ordinary app states.** AI developers need examples of boring-but-critical UI: empty states, loading, error/warning/success badges, table density, filter controls, forms and modals.
7. **Accessibility is the main caveat for soft UI.** Frosted/neumorphic designs easily drift into low contrast. Any production use needs a contrast pass on muted text, pastel badges, chart labels and secondary metadata.
8. **Publishing and verification should be part of the system test.** A variant is only useful when it is public, loads without console errors, loads logo assets correctly and includes the exact gradient token.

Practical guidance for future variants: start from the existing component inventory, change only the surface treatment and visual posture, keep semantic tokens intact, then verify in-browser before presenting the page as an AI-dev reference.

