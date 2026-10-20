# Design Report: Gear & Chain Cycle Works

## 1. What I built
A one-page static site for a small cycle repair shop. It has a header with navigation, a hero, a services section, a content area with a sidebar, and a footer. Files: `index.html`, `style.css`, `report.md`.

> No wireframe file came with the task, so I worked from the standard layout the brief describes (header, navigation, content areas, footer) and chose the shop as the subject. If your wireframe differs, the section order is easy to change because each block is self-contained.

## 2. Semantic HTML
- `header`, `nav`, `main`, `section`, `article`, `aside`, `footer` are used for what they mean, not as styled divs.
- One `h1`, then `h2` for each section and `h3` inside cards and sidebar boxes, so the heading outline is clean.
- The price list is a real `table` with `caption`, `thead` and `th scope`, since it is tabular data.
- Opening hours use a description list (`dl`) and the address uses `address`.
- Decorative SVG has `aria-hidden="true"`.

## 3. Layout strategy
| Area | Technique | Why |
|---|---|---|
| Header | Flexbox | Logo left, links right, one row |
| Hero | CSS Grid, 1.2fr / 1fr | Text slightly wider than the illustration |
| Service cards | Grid, 3 equal columns | Equal heights without hacks |
| Main + sidebar | Grid, `1fr 300px` | Fixed-width sidebar, flexible content |
| Footer | Grid | Name and links on one line, note below |

A single `.wrap` class (max-width 1080px) keeps every section aligned to the same edges.

## 4. Colour and type
- Navy `#1d3557` for header, footer and headings; yellow `#f2c230` for buttons and card tops; soft grey `#eef2f5` for backgrounds.
- Navy and yellow are close to what you see on bike shop signboards, which is why I picked them.
- System font stack (Segoe UI, Roboto, Arial). No external fonts, so the page loads fast and works offline.
- Body line-height 1.6 and paragraph width capped at 38rem for comfortable reading.

## 5. Responsiveness
Desktop-first with two breakpoints:
- **900px**: hero and content stack into one column, cards become a single column.
- **600px**: header stacks, nav links wrap, buttons go full width, headings shrink.

I checked 1280px, 1024px, 768px and 375px widths using browser DevTools device mode.

## 6. Challenges and how I solved them
1. **Table overflowing on phones.** Wide tables push the whole page sideways. I wrapped it in `.table-scroll { overflow-x: auto }` so only the table scrolls.
2. **Sticky header covering section titles.** Clicking a nav link scrolled the heading under the header. Fixed with `scroll-padding-top` on `html`.
3. **Navigation without JavaScript.** A hamburger menu needs JS or checkbox hacks. For four links, letting them wrap under the logo was simpler and more reliable.
4. **Specificity clashes.** An early `.hero p` rule overrode my button styles. I switched to class-based selectors and kept the CSS in one order (base, layout, components, media queries).
5. **Hero illustration blurring or overflowing.** Using an inline SVG with `viewBox` and `width: 100%` keeps it sharp at any size.

## 7. What I would improve next
- Real photos with `srcset` and `loading="lazy"`.
- A working contact form.
- A proper mobile menu once there are more than four pages.
