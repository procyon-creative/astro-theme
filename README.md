# @procyon-creative/astro-theme

Procyon Creative house-style Astro theme. Tailwind v4, dark navy palette, gradient accents. Provides landing-page and docs layouts, plus an optional Starlight color/font overlay.

**Status:** pre-0.1.0, scaffolding in progress.

## What it ships

- A Tailwind v4 `@theme` block with the Procyon Creative palette, font stack, and glow utilities
- Astro components: `TopStrip`, `Hero`, `FeatureCards`, `StructPanel`, `LinkCards`, `Footer`, `Background`
- Two layouts:
  - `LandingLayout` — single-page marketing
  - `DocsLayout` — content-collection-driven, one section per markdown entry
- Optional Starlight overlay for projects that want a multi-page docs site themed to match

## Design system

| Token          | Value     |
| -------------- | --------- |
| `bg`           | `#0a0628` |
| `surface`      | `#150a36` |
| `ink`          | `#f3edff` |
| `ink-soft`     | `#d6cfff` |
| `rule`         | `#4a3a8a` |
| `neon-cyan`    | `#6cf3fb` |
| `neon-magenta` | `#ff6ed3` |
| `neon-yellow`  | `#f6e858` |
| `neon-orange`  | `#ff9b6e` |

Display font: Big Shoulders Display. Body: IBM Plex Sans. Mono: JetBrains Mono.

## Local development

```bash
cd demo
npm install
npm run dev
```

The `demo/` Astro site consumes the theme via `file:..` and proves the tokens compile through `@tailwindcss/vite`. Edit anything under `src/` and the demo hot-reloads.

## Compatibility

- **Astro 5.x.** Astro 6 currently fails to build with `@tailwindcss/vite` because of a Rolldown bundler/oxc-resolver mismatch (`Missing field tsconfigPaths`). Pinned to Astro 5 until that lands upstream.
- **Tailwind v4.** Uses the `@theme inline` block, not a `tailwind.config.js`. Consumers must be on v4.

## Consumers (planned)

- [procyon-creative/wp-dario-provider](https://github.com/procyon-creative/wp-dario-provider) — landing page at `/wp-dario-provider/`
- [procyon-creative/procyon-plugin-boilerplate](https://github.com/procyon-creative/procyon-plugin-boilerplate) — landing page at `/procyon-plugin-boilerplate/`

## License

GPL-2.0-or-later.
