# AI Agent Instructions for e-Portfolio Project

## Project Overview
This is a **bilingual French/English data science portfolio** for Nathan Chan Sing Man. Two parallel HTML versions exist:
- **index.html** → Bootstrap 5 + custom CSS ([CSS/style.css](CSS/style.css))
- **index2.html** → Tailwind CSS with inlined config (modern approach, currently active)

**Language**: Content is in French; HTML comments and structure should match this convention.

## Architecture: Design System

### Color Theme (CSS Variables & Tailwind Config)
Both versions use the same **earthy, nature-inspired palette** defined in [CSS/style.css](CSS/style.css#L1-L12):
```css
--primary-color: #606c38;      /* Forest green */
--secondary-color: #283618;    /* Dark forest */
--accent-color: #bc6c25;       /* Earth brown */
--light-accent: #dda15e;       /* Sand/tan */
--background-light: #fefae0;   /* Cream */
```

**In index2.html**, this is mapped to Tailwind colors:
```javascript
colors: {
  cream: '#fefae0',   olive: '#606c38',
  forest: '#283618',  earth: '#bc6c25',   sand: '#dda15e'
}
```

**When updating design**: Always modify both places if touching colors.

## Content Sections (Static Structure)

All pages use this consistent layout:
1. **Fixed Navigation** - Logo, nav links (À propos, Projets, Contact), responsive toggle
2. **Hero Section** - Profile photo, title "Data Scientist & Analyste", CTA buttons
3. **About** - Formation (IUT), experience (Kantar Worldpanel), languages
4. **Skills** - Organized by type: Programmation (Python, R, SQL), Outils d'Analyse, Data Science, Soft Skills
5. **Projects** - 3 showcase projects with modal details (Dashboard Météo, Scraping Parisien, Automatisation R)
6. **Experience** - Professional timeline (currently under Kantar)
7. **Contact** - Email CTA

## Key Technical Patterns

### Dark Mode Implementation (index.html only)
Uses CSS checkbox trick: `<input type="checkbox" id="dark-toggle">` toggles `#dark-toggle:checked ~ *` selector. **Not implemented in index2.html yet** - if adding, follow same pattern.

### Animations & Interactions
- **Reveal classes**: `fade-in`, `reveal` with `transition-delay` for staggered reveals
- **Hover states**: Cards lift on hover (e.g., `transform: translateY(-5px)`)
- **Modals**: index2.html has modal system (`openModal()`, `closeModal()`) with `modal-overlay` backdrop
- **Blob animations** (index2.html only): Animated gradient blobs in background using keyframes

### Responsive Design
- Bootstrap: Built-in grid (`col-md-6`, `col-lg-8`)
- Tailwind: `md:` breakpoint prefix; key layout: `md:grid-cols-2`, `md:flex-row`
- Mobile-first: Navigation collapse, single-column projects on small screens

## Development Decisions

### Bootstrap vs Tailwind: Current Strategy
- **index.html** is feature-complete but verbose
- **index2.html** is the primary active version (cleaner, Tailwind utilities reduce CSS)
- **Recommendation**: Deprecate Bootstrap version OR standardize on Tailwind for maintenance

### Projects Section
Projects render as cards with modal popups. In index2.html:
- Each project has `onclick="openModal('modal-N')"` button
- Modal template: Header with category badge, content, gallery if needed
- Add new projects by duplicating card button + modal div, updating IDs sequentially

### Image Assets
All images in `/Image/` folder:
- `Photo CV.jpg` - Profile photo (reused across both versions)
- Project screenshots (e.g., `collect3.png`, `Base_ppt.png`)
- `logo.png` - Navigation logo (index.html only)

**Pattern**: Use relative paths `Image/filename`, no trailing slash

## Code Style & Conventions

### HTML
- French section IDs: `id="home"`, `id="projets"`, `id="contact"` (lowercase)
- Semantic tags: `<section id="...">`, `<nav>`, proper heading hierarchy
- Accessibility: Include `alt` text on all images, `aria-*` for interactive elements

### CSS (index.html)
- Use CSS variables (`var(--primary-color)`) NOT hardcoded colors
- Custom utilities: `.fade-in`, `.card-modern`, `.skill-item`
- Animations in `@keyframes`: `fadeInUp`, `fadeIn`

### Tailwind (index2.html)
- Prefer Tailwind utilities over custom CSS (e.g., `bg-forest` not `background-color`)
- Keep inline `<style>` minimal; use Tailwind config for extends
- Color opacity: Use `/20`, `/60` syntax (e.g., `text-forest/70`)
- Custom animations in config: `blob`, `fade-in`

## Important Gotchas & Maintenance Notes

1. **External CDN Dependencies**:
   - Font-Awesome 6.4.0 (icons) - both versions
   - Google Fonts (Inter family)
   - Bootstrap CDN (index.html only)
   - Tailwind CDN (index2.html only) - requires runtime JIT compilation

2. **Metadata in Head**:
   - `<meta name="description">` and `<meta name="keywords">` in index.html are SEO-optimized
   - Google verification file: `google183908ac8b8e3024.html` (for Search Console)

3. **Modal IDs Must Match**:
   Button onclick target must exactly match modal ID: `onclick="openModal('modal-1')"` → `id="modal-1"`

4. **Image Paths**:
   - If moving files, update all relative paths
   - `Image/` folder is case-sensitive starting with capital I

## Next Steps for Agents

- **Adding content**: Update section HTML + ensure smooth scroll (via `id` anchors)
- **Adding projects**: Create new card button + new modal div block; increment `modal-N` ID
- **Styling tweaks**: Prefer Tailwind config in index2.html OR CSS variables in style.css to maintain both versions
- **Responsive issues**: Test both mobile and desktop; Bootstrap has `visible-*` classes, Tailwind uses `hidden md:block`
