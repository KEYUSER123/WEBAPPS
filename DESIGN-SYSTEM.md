# ATELIER — Workspace design system

ATELIER is the shared visual design direction for the Workspace apps. The implementation keeps the existing static GitHub Pages structure and app behavior, while centralizing shared visual rules in `workspace-design.css`.

## Design principles

- Minimal, quiet surfaces rather than gradients and excessive card chrome.
- Light and dark themes are treated as equally intentional palettes.
- One consistent type, spacing, border, focus, navigation, input, and interaction language.
- Small app-specific accent colors help orientation without making the apps feel unrelated.
- Existing app data, Supabase logic, routes, and page functionality stay in each app's original HTML file.

## Theme palettes

### Porcelain — Light

| Token | Value |
|---|---|
| Background | `#F5F3EE` |
| Surface | `#FFFFFF` |
| Raised surface | `#EEEBE4` |
| Text | `#292A27` |
| Muted text | `#6F706A` |
| Border | `#E2DED5` |
| Shared accent | `#927747` |

### Obsidian — Dark

| Token | Value |
|---|---|
| Background | `#101216` |
| Surface | `#191C21` |
| Raised surface | `#22262C` |
| Text | `#F3F0E9` |
| Muted text | `#A8AAA8` |
| Border | `#2C3036` |
| Shared accent | `#D0B98A` |

The dashboard uses the shared champagne accent. Tasks use sage, Finance uses forest green, and Fitness uses restrained terracotta. These accents adapt for dark mode.

## Implementation

- `workspace-design.css` is the shared stylesheet. Keep reusable components and tokens here instead of adding repeated inline overrides to each app.
- Each page declares its `data-app` value on the `<html>` element (`dashboard`, `tasks`, `finance`, `fitness`) to select the appropriate accent.
- Both themes use the same local-storage key: `workspace-theme`, with values `light` or `dark`.
- The theme is bootstrapped in the page head to reduce flashes of the wrong palette, and the controller keeps the choice in sync across tabs on the same origin.
- Because browser local storage is origin-specific, theme preferences are shared across app routes under the same published site, not across unrelated domains.

## Editing guidance

1. Prefer shared tokens (`--at-bg`, `--at-surface`, `--at-text`, `--at-muted`, `--at-line`, `--at-accent`) over hard-coded colors.
2. Use the primary accent for important states and active navigation sparingly.
3. Keep semantic success, warning, and danger states distinct from decorative accents.
4. Validate both themes, narrow mobile layouts, forms, dialogs, data tables, and app navigation after UI changes.
5. Do not rename application data keys, database tables, Supabase settings, or functional element IDs as part of visual work.
