<!-- Repository-specific Copilot instructions for AI coding agents -->
# Guidance for AI contributors

This is a small, static GitHub Pages portfolio site. Keep recommendations focused, concrete, and aligned with the code in `index.html` and the project description in `README.md`.

- **Big picture**: single-page static site served from the repository root via GitHub Pages. `index.html` is the app entry — HTML, CSS, and minimal dependency-free JavaScript live in that file.

- **When editing / adding features**: prefer small, local edits inside `index.html`. There is no build step or bundler; changes take effect when `index.html` is updated and pushed.

- **Preview locally**: run a simple static server from the repo root. Example commands:

  - `python3 -m http.server 8000` — open `http://localhost:8000`.
  - (Optional) `npx serve .` if Node.js is available.

- **Deployment**: GitHub Pages serves the site from the `main` branch (root). No additional CI or build pipeline present.

- **Key patterns and concrete examples**:
  - Projects and experience are defined as JavaScript arrays inside `index.html` (`projects` and `experience`). To add or modify entries, edit those arrays. Example project object shape:

```js
{
  title: 'My Project',
  blurb: 'Short description',
  tags: ['web','ml'],        // tags used by the filter buttons
  techStack: 'React | FastAPI | ...',
  imageText: 'Thumb',
  links: { demo: 'https://...', code: 'https://github.com/...' }
}
```

  - The project filtering UI uses `data-filter` attributes on `.filter` buttons and the `tags` array on each project. Keep tag strings consistent (lowercase) to avoid mismatches.

  - Theme handling is implemented inline: the theme key is `theme` in `localStorage` and the DOM attribute is `data-theme` on the root element. Respect that mechanism when changing theme behavior.

  - Accessibility cues are present (e.g., `aria-pressed` for filter buttons, `aria-live` on the project grid, `role=menubar` on nav). Preserve or improve these attributes when modifying interactive elements.

- **Static assets and references**:
  - `preview.png` and the résumé links are referenced from `index.html`. If adding images, place them in the repo root (or update paths) and ensure relative URLs work on GitHub Pages.

- **Conventions to follow**:
  - Minimal dependencies: the site intentionally avoids build tools and external frameworks. Prefer vanilla JS/CSS fixes that don't require introducing a bundler.
  - Keep markup, styles, and behavior accessible and responsive — the CSS uses CSS variables and `data-theme` for light/dark.
  - When updating content arrays (`projects`, `experience`), maintain the current object keys to avoid runtime errors.

- **What not to assume / not present**:
  - There is no test suite, package manifest, or CI config in the repo. Do not add complex build tooling without confirming intent with the repo owner.

- **Suggested quick tasks for an AI helper**:
  - Add one new project entry to the `projects` array following the example object shape.
  - Improve the filter UX by normalizing tags before comparison (keep changes limited to `index.html`).
  - Add a small script to lazy-load `preview.png` only if present (place checks in `index.html`).

If any of the above items are unclear or you want more detailed examples (e.g., a patch that adds a new project or normalizes tags), tell me which change you'd like and I'll implement it.
