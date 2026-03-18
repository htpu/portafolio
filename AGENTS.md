# AGENTS.md - Developer Guidelines

## Project Overview

This is a personal portfolio website - a "Realtime Orrery" (solar system visualization). It's a static HTML file with:
- Tailwind CSS (Production CLI build)
- Vanilla JavaScript for canvas animations
- Custom CSS embedded in `<style>` tags
- Simple build system for Tailwind CSS

---

## Commands

### Running the Project
Since this uses Tailwind CLI, you need to build the CSS or use watch mode:

```bash
# Install dependencies
npm install

# Build CSS once
npm run build:css

# Watch mode for development
npm run watch:css

# Serving the site
npx serve .
```

### Build Process
The project uses Tailwind CLI version 3. It scans `index.html` and outputs to `dist/output.css`.

### Deployment
- **Platform**: GitHub Pages
- **Automation**: GitHub Actions (`.github/workflows/deploy.yml`)
- **Process**: On push to `main`, the workflow installs dependencies, runs `npm run build:css`, and deploys the entire directory (including the generated `dist/`).
- **Note**: The `dist/` directory is ignored in git and only exists in the CI environment or local development after building.

---

## Code Style Guidelines

### General Principles
- Keep code clean and readable
- Use semantic HTML5 elements
- Maintain consistent indentation
- Add comments for complex logic (Chinese comments are acceptable)

### HTML Conventions
- Use lowercase for tags and attributes
- Use double quotes for attribute values
- Organize attributes in a logical order: `id`, `class`, `src`/`href`, `data-*`, then others
- Include `lang` attribute on `<html>`
- Use `viewport` meta for responsive design
- Prefer Tailwind utility classes over custom CSS when possible

### CSS Guidelines
- Use Tailwind utility classes for layout and spacing
- Custom CSS goes in `<style>` block in `<head>` - not inline
- CSS variables (custom properties) for theme colors: `--accent`, `--bg-dark`
- Use `rem` for font sizes, `px` for borders and small dimensions
- Use `cubic-bezier()` for smooth animations - avoid linear transitions
- Group related styles with comments in Chinese (e.g., `/* 背景 Canvas */`)

### JavaScript Conventions
- Use `const` by default, `let` when mutation is needed
- Avoid `var`
- Use arrow functions for callbacks
- Use template literals for string interpolation
- Prefer `forEach`/`map` over traditional for loops
- Declare variables at the top of their scope
- Add Chinese comments explaining complex logic

### Naming Conventions
- **Variables/functions**: camelCase (`canvas`, `init()`, `activePlanet`)
- **Constants**: UPPER_SNAKE_CASE for magic numbers extracted as constants
- **CSS Classes**: kebab-case (Tailwind uses this)
- **IDs**: camelCase (e.g., `planet-hud`, `main-time`)

### Error Handling
- Wrap DOM queries in `document.getElementById()` directly (no error handling needed for simple file)
- Use optional chaining where appropriate: `?.`
- Handle `resize` and `mousemove` events with debouncing if performance issues arise

### Performance Considerations
- Use `requestAnimationFrame` for animations (not `setInterval`)
- Cache DOM elements at initialization
- Use `const` for values that don't change
- Minimize DOM reflows - batch reads and writes

### Canvas Guidelines
- Always clear canvas with `ctx.clearRect()` at start of frame
- Save/restore context when modifying state (`ctx.save()`, `ctx.restore()`)
- Use `requestAnimationFrame` timestamp for smooth animations
- Center calculations use `width/2`, `height/2`

### Responsive Design
- Use Tailwind's responsive prefixes (`md:`, `lg:`)
- Test on mobile and desktop viewports
- Use `flex` and `grid` for layouts

---

## File Structure

```
portafolio/
└── index.html    # Single-file application (HTML + CSS + JS)
```

All code (HTML, CSS, JavaScript) lives in `index.html`. No splitting across files.

---

## Adding New Features

### To add a new planet:
1. Add entry to `planets` array with: `name`, `dist`, `radius`, `period`, `color`, `desc`
2. Optionally add `moons` array or `rings: true`

### To modify styling:
- Quick changes: Edit Tailwind classes in HTML
- Complex styles: Add to `<style>` block

### To modify animation:
- Main loop: `animate()` function
- Planet drawing: `drawPlanet()` function
- Clock: `updateClock()` function

---

## External Resources

### CDN Dependencies
- Tailwind CSS: Production build (no longer using Play CDN)
- Google Fonts: Inter, Orbitron

### External Images
- Unsplash images used for photo gallery

When adding external resources, ensure they load over HTTPS.

---

## Browser Support

Target modern browsers (Chrome, Firefox, Safari, Edge). No IE11 support needed.

---

## Notes for AI Agents

- This is a creative/portfolio site - prioritize aesthetics and smooth animations
- The "sci-fi/space" theme should be maintained
- Keep the file as a single HTML - don't split into multiple files
- Test any changes locally by serving the file
