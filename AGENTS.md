# Quarto FH-SWF Theme — Project Overview & Plan

## Goal

Create a Quarto theme that implements the **FH Südwestfalen (FH-SWF) Corporate Design** guidelines as documented in `CD-Handbuch_der_FH_SWF.pdf` (August 2014, 33 pages). The theme supports **RevealJS presentations** and **HTML documents/websites**.

## Architecture Decision

Use **`_brand.yml`** (Quarto 1.6+) as the primary mechanism. This provides cross-format branding from a single configuration file.

### Key `_brand.yml` Features to Utilize:
- **Semantic Color Mapping**: Map primary blue to `primary` and secondary colors to `secondary`, `success`, `info`, `warning`, `danger` as appropriate.
- **Typography Sourcing**: Use `source: google` for Lato and Source Serif 4 to ensure easy installation and consistent rendering.
- **Logo Variants**: Use the `logo` section with `small`, `medium`, and `large` keys, and provide `light`/`dark` variants to support negative versions.
- **Theme Layering**: In `_quarto.yml`, use the `brand` keyword in the `theme` list (e.g., `theme: [brand, fhswf-revealjs.scss]`) to ensure brand defaults are correctly layered.
- **Shortcodes**: Leverage `{{< brand color primary >}}` and `{{< brand logo medium >}}` within example documents.

---

## Reference: CD Handbook Summary

### Colors (Chapter 3, pages 11–12)

**Primary Color:**

| Name | CMYK | RGB | Hex | HKS | RAL |
|------|------|-----|-----|-----|-----|
| **Blau** (Blue) | 100/70/0/0 | 57/86/159 | `#39569F` | 39 | 5005 Signalblau |

> The PDF states Hex `#39659F` and RGB `57/86/159`. RGB 57/86/159 converts to `#39569F`. Verify visually during implementation.

Tint scale: 20%–100% in 10% steps.

**Secondary Colors:**

| Name | English | CMYK | Approx. Hex | Role |
|------|---------|------|-------------|------|
| Grau | Grey | 10/0/0/30 | `#A1B3B3` | General |
| Rot | Red | 0/100/100/20 | `#CC0000` | Präsenz-Bachelor |
| Orange | Orange | 0/50/100/0 | `#FF8000` | Präsenz-Master |
| Türkis | Turquoise | 100/10/30/0 | `#009FB3` | Verbund-Bachelor |
| Grün | Green | 40/0/100/0 | `#99CC00` | Verbund-Master |
| Pink | Magenta | 25/100/15/0 | `#BF0088` | General |
| Wasserblau | Water Blue | 100/30/0/0 | `#0077BF` | General |

> Only the primary blue has officially specified RGB/Hex. Secondary hex values are CMYK-to-RGB approximations — verify visually.

Each secondary color has a **tint scale** (6 steps down to 40%) and a **shade scale** (6 steps with added black: Grey +60%K, Red +40%K, all others +25%K).

### Typography (Chapter 2, pages 9–10)

**Original fonts:** Fedra Serif B / Fedra Sans (commercial). **Fallback in CD:** Arial.

**Free alternatives for this project:**

| Role | Original | Replacement | Rationale |
|------|----------|-------------|-----------|
| Sans-serif (body, UI) | Arial | **Lato** | User preference; humanist, Google Font, OFL |
| Headings/display | Fedra Sans | **Lato** (semibold/bold) | Good weight range for display use |
| Serif (long-form) | Fedra Serif B | **Source Serif 4** | Adobe open-source, variable, old-style figures |
| Monospace (code) | — | **Source Code Pro** or **JetBrains Mono** | Complements Source Serif 4 |

CD typography rules: Guillemets `»...«` for quotation marks. Old-style figures in body, lining figures in tables.

### Logo (Chapter 1, pages 3–8)

- **Wort-Bildmarke**: Full logo with stylized face icon
- **Bildmarke**: Icon only (can be used separately)
- Min width: 3 cm; at A4 = 5.0 cm (~25% of media width)
- Safety zone: 3x the small square width
- Negative variant (white on dark), B/W variant (70%/100% black)

### Design Elements (Chapters 4–7)

- **Rahmen** (Frames): Corner radius 9mm at A4, ratio 1:3
- **Linie** (Line): Connecting/dividing element
- **Claim**: "Wir geben Impulse" (German only)

---

## Project Structure

```
Quarto-FH-SWF-Theme/
├── AGENTS.md                        # This file
├── CD-Handbuch_der_FH_SWF.pdf      # Reference (not distributed)
├── _brand.yml                       # Core brand definition
├── _quarto.yml                      # Project configuration
├── assets/
│   ├── logos/
│   │   ├── logo-fh-swf.png        # Official PNG logo (183x57 px, provided by user)
│   │   ├── logo-fh-swf-rgb.png    # RGB conversion for PDF compatibility
│   │   ├── fhswf-logo.svg          # Full logo (SVG placeholder)
│   │   ├── fhswf-logo-white.svg    # Negative variant
│   │   ├── fhswf-logo-bw.svg       # B/W variant
│   │   ├── fhswf-icon.svg          # Bildmarke (color)
│   │   └── fhswf-icon-white.svg    # Bildmarke negative
│   └── fonts/                       # Local font files (optional)
├── styles/
│   ├── fhswf-revealjs.scss          # RevealJS SCSS customizations
│   ├── fhswf-html.scss             # HTML document SCSS customizations
│   └── _variables.scss              # Shared SCSS variables
├── templates/
│   └── title-slide.html             # Custom RevealJS title slide
├── examples/
│   ├── slides.qmd                   # Example presentation
│   └── document.qmd                # Example HTML document
└── README.md                        # User documentation
```

---

## Implementation Plan

### Phase 1: Foundation

1. **Set up `_brand.yml`** — color palette, semantic mappings, typography (Lato + Source Serif 4), logo references
2. **Prepare logo assets** — extract/recreate SVGs in color, white, and B/W variants
3. **Create `_quarto.yml`** — project config, format defaults for revealjs and html

### Phase 2: RevealJS Theme

4. **Create `fhswf-revealjs.scss`** — CD colors mapped to Reveal Sass variables, headings, body text, code blocks, blue header bar
5. **Create custom title slide** — `title-slide.html` partial with logo, blue frame, typography
6. **Configure RevealJS defaults** — logo, footer, slide numbers, transitions

### Phase 3: HTML Document Theme

7. **Create `fhswf-html.scss`** — Bootstrap Sass variables, navbar, headings, links, callouts, tables
8. **Configure HTML defaults** — TOC, navbar logo, footer

### Phase 4: Polish & Documentation

9. **Create example documents** — slides.qmd and document.qmd showcasing all elements
10. **Write README.md** — installation, usage, configuration, screenshots
11. **Color verification** — visual comparison against PDF swatches, adjust hex values
12. **Accessibility check** — WCAG AA contrast ratios for all text/background combos

---

## Key Decisions

| Decision | Choice | Rationale |
|----------|--------|-----------|
| Distribution | `_brand.yml` | Modern, cross-format, minimal maintenance |
| Sans-serif | Lato | User preference; replaces Arial fallback |
| Serif | Source Serif 4 | Best open-source serif, variable, old-style figures |
| Formats | RevealJS + HTML | Most common Quarto use cases |
| Logo | PNG (official) | User provided `logo-fh-swf.png` (183x57 px); SVG placeholders for backwards compatibility |

## Open Questions

- [ ] Dark mode support for HTML?
- [ ] Multiple RevealJS slide layouts (section dividers with full-color backgrounds)?
- [ ] Future Typst/PDF format?
- [ ] Pre-compute tint/shade scales as SCSS variables or generate programmatically?
- [x] Official PNG logo provided by user (logo-fh-swf.png)

## Dependencies

- **Quarto** >= 1.6
- **Fonts**: Lato (OFL), Source Serif 4 (OFL), monospace TBD
- No runtime dependencies — pure SCSS/YAML/HTML

## Global Instructions Reference

Universal workflow rules (beads protocol, session completion, skill loading, prohibited items) are defined in the global `opencode.json` `instructions` array and apply to all projects automatically.

<!-- BEGIN BEADS INTEGRATION v:1 profile:minimal hash:970c3bf2 -->
## Beads Issue Tracker

This project uses **bd (beads)** for issue tracking. Run `bd prime` to see full workflow context and commands.

### Quick Reference

```bash
bd ready              # Find available work
bd show <id>          # View issue details
bd update <id> --claim  # Claim work
bd close <id>         # Complete work
```

### Rules

- Use `bd` for ALL task tracking — do NOT use TodoWrite, TaskCreate, or markdown TODO lists
- Run `bd prime` for detailed command reference and session close protocol
- Use `bd remember` for persistent knowledge — do NOT use MEMORY.md files

**Architecture in one line:** issues live in a local Dolt DB; sync uses `refs/dolt/data` on your git remote; `.beads/issues.jsonl` is a passive export. See https://github.com/gastownhall/beads/blob/main/docs/SYNC_CONCEPTS.md for details and anti-patterns.

## Agent Context Profiles

The managed Beads block is task-tracking guidance, not permission to override repository, user, or orchestrator instructions.

- **Conservative (default)**: Use `bd` for task tracking. Do not run git commits, git pushes, or Dolt remote sync unless explicitly asked. At handoff, report changed files, validation, and suggested next commands.
- **Minimal**: Keep tool instruction files as pointers to `bd prime`; use the same conservative git policy unless active instructions say otherwise.
- **Team-maintainer**: Only when the repository explicitly opts in, agents may close beads, run quality gates, commit, and push as part of session close. A current "do not commit" or "do not push" instruction still wins.

## Session Completion

This protocol applies when ending a Beads implementation workflow. It is subordinate to explicit user, repository, and orchestrator instructions.

1. **File issues for remaining work** - Create beads for anything that needs follow-up
2. **Run quality gates** (if code changed) - Tests, linters, builds
3. **Update issue status** - Close finished work, update in-progress items
4. **Handle git/sync by active profile**:
   ```bash
   # Conservative/minimal/default: report status and proposed commands; wait for approval.
   git status

   # Team-maintainer opt-in only, unless current instructions forbid it:
   git pull --rebase
   bd dolt push
   git push
   git status
   ```
5. **Hand off** - Summarize changes, validation, issue status, and any blocked sync/commit/push step

**Critical rules:**
- Explicit user or orchestrator instructions override this Beads block.
- Do not commit or push without clear authority from the active profile or the current user request.
- If a required sync or push is blocked, stop and report the exact command and error.
<!-- END BEADS INTEGRATION -->

<!-- BEGIN BEADS CODEX SETUP: generated by bd setup codex -->
## Beads Issue Tracker

Use Beads (`bd`) for durable task tracking in repositories that include it. Use the `beads` skill at `.agents/skills/beads/SKILL.md` (project install) or `~/.agents/skills/beads/SKILL.md` (global install) for Beads workflow guidance, then use the `bd` CLI for issue operations.

### Quick Reference

```bash
bd ready                # Find available work
bd show <id>            # View issue details
bd update <id> --claim  # Claim work
bd close <id>           # Complete work
bd prime                # Refresh Beads context
```

### Rules

- Use `bd` for all task tracking; do not create markdown TODO lists.
- Run `bd prime` when Beads context is missing or stale. Codex 0.129.0+ can load Beads context automatically through native hooks; use `/hooks` to inspect or toggle them.
- Keep persistent project memory in Beads via `bd remember`; do not create ad hoc memory files.

**Architecture in one line:** issues live in a local Dolt DB; sync uses `refs/dolt/data` on your git remote; `.beads/issues.jsonl` is a passive export. See https://github.com/gastownhall/beads/blob/main/docs/SYNC_CONCEPTS.md for details and anti-patterns.
<!-- END BEADS CODEX SETUP -->
