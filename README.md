# FreeLivingDesigns Portfolio
**Tom Black — FEWD — February 2026 — Assignment 4**

---

## About This Project

This project is a responsive portfolio website built with semantic HTML and external CSS code style sheet. It was created for Assignment 4 and builds on the foundation of Assignment 3, expanding it with advanced CSS layout techniques, responsive design, and interactive features.

Core files:
- `index.html` — all page content and structure
- `styles.css` — all styling, layout, animation, and responsive rules

The site presents:
- A branded header with custom navigation
- An About Me section with a profile image
- A portfolio section with two featured WordPress project videos and thumbnails
- A floating two-step scroll-to-top control for ease of use and accidental "top" presssing.
- A footer with an emoji-based feedback rating and contact form overlay leading to a mailto: feature for feedback.

---

## Assessment Objectives Covered

This submission demonstrates:

| Requirement | Implementation |
|---|---|
| Mobile-first CSS structure | Base styles written for mobile, enhanced upward with `min-width` queries towards wide screens |
| Media queries at multiple breakpoints | 640px (tablet) and 900px (desktop) breakpoints |
| Flexbox for layout | Navigation and About section |
| CSS Grid for layout | Portfolio project card grid |
| Custom navigation with styled list items (menu) | Pill-shaped gradient nav buttons with hover/press states |
| CSS transitions and animation | fadeIn, card hover, nav hover, scroll-to-top, feedback overlay |
| CSS validation | Validated with W3C CSS Validation Service — no CSS errors |
| HTML validation | Validated with W3C Markup Validation Service — no HTML errors |
| README documentation | Final documentation and reflection included |

---

## How I Approached Responsiveness

I used a mobile-first strategy throughout. All base styles in `styles.css` are written for small screens without any media query wrapping. I then progressively layered enhancements at two breakpoints using `min-width` queries rather than `max-width`, for the best mobile-first approach.

**Breakpoints and what they change:**

- **Base (all screens):** 14px body padding, single-column layout, stacked About section, fluid typography using `clamp()`, compact nav buttons that stay on one line without stacking on mobile (result buttons nexto each other on mobile)
- **`min-width: 640px` (tablet):** body padding increases to 20px, logo size increases, section padding increases, nav buttons scale up to full size
- **`min-width: 900px` (desktop):** About section switches from column to row layout, portfolio grid expands from one to two columns, About section goes to text and image layout and cards side buy side, with body padding increases further.

The reason I chose mobile-first is that most portfolio visitors are on mobile. Designing for the smallest screen first and layering up is more intentional than trying to shrink things down from a wide desktop view.

---

## Where and Why I Used Flexbox and Grid

**Flexbox** was the right tool anywhere the layout needed to align items along a single axis:

- `nav ul` — Flex row with `justify-content: center` and `flex-wrap: nowrap` keeps navigation on one line on mobile without stacking. This was a deliberate decision to avoid a hamburger menu.
- `#about` — Flex column on mobile (profile image below text) that switches to flex row at desktop, placing the text and image side by side. I used `flex: 1` on the text block so it fills available space while the photo stays at a fixed max width.

**CSS Grid** was the right choice for the portfolio section because it manages a two-dimensional card layout cleanly:

- `.portfolio-grid` — `grid-template-columns: 1fr` stacks cards on mobile, switching to `1fr 1fr` at desktop for an equal two-column layout. Using Grid here meant I did not need to manually calculate widths, margins, or use float clearing, allowing for a seamless duel coloumn layout of PC vs. Mobile (stacxked).

---

## Design Decisions for Navigation, Structure, and Interactivity

### Navigation
I styled the nav links as custom pill-shaped buttons using a gradient fill, border, and layered shadow rather than a plain underlined list. The Oswald heading font with uppercase lettering and letter-spacing gives the nav a distinct brand identity separate from the body text. On hover the buttons lift with `translateY` and brighten slightly, and on active press they lower. This creates a tactile, professional feel. In the final version, I added a dedicated dropdown Menu button that contains About Me and Portfolio, with matching button size and styling for consistency. The final solution opens on click, stays visible while the user chooses an option, and closes automatically after a section link is selected.

### Structure
The page uses semantic HTML throughout. Portfolio projects are wrapped in `<article>` elements inside a grid container, the About section uses `<section>`, and each video is inside a `<figure>` with a `<figcaption>`. This makes the page accessible to assistive technologies and reflects professional front-end standards.

### Interactivity
- `@keyframes fadeIn` — sections animate up into view on page load for a polished entrance
- Project cards lift and gain a drop shadow on hover, making them feel like distinct interactive content blocks
- The scroll-to-top button uses a CSS `:target` pattern to create a two-step interaction: first click reveals a green confirmation state, second click scrolls to the top. Its shape and motion styling match the navigation button system for visual consistency. This helps to avoid miss-touch to top button and actions a two step go to top function.
- The footer feedback flow uses emoji triggers to open full-screen overlay modals, showing a gratitude animation followed by a feedback textarea form — allowing users to email me at freelivingdesigns@gmail.com using a mailto: function opening the native mail app encouraging feedback on website. I wanted to make it a counter button but could not do this successfully using only CSS. `:target`

---

## Typography

I chose Oswald and Open Sans as a pairing from Google Fonts because they complement each other well:

- **Headings:** Oswald — strong, condensed, and works well with uppercase letter-spacing for impact
- **Body text:** Open Sans — clean, highly readable, and performs well at small sizes on mobile
- **Fallback stack:** `'Arial Narrow', Arial` for headings and `'Segoe UI', Helvetica, Arial` for body text, covering Windows, Mac, and Linux systems
- **Fluid sizing:** All font sizes use `clamp()` so they scale naturally between mobile and desktop without extra media query rules

---

## Accessibility and UX Considerations

Accessibility was considered throughout and not added as an afterthought:

- Skip link at the top of the page for keyboard and screen reader users
- Visible `focus-visible` outlines with a high-contrast yellow accent (`#FFE082`) on all interactive elements
- Semantic HTML structure: `<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<figure>`, `<figcaption>`, `<footer>`
- `aria-label` attributes on navigation and interactive controls
- Video poster thumbnails so content is meaningful before playback begins
- `loading="lazy"` and `decoding="async"` on images for performance

---

## Video and Feedback Features

**Video posters:**
- `images/reskin-cover.png` — Reskin Aesthetics project thumbnail
- `images/sunglide-cover.png` — Sunglide Online project thumbnail (using a fun youtube type thumbnail with me displaying the content with headings and screenshots of the video on the cover image)

**Footer feedback rating:**
- Three emoji buttons (👍 😍 🎉) allow visitors to rate the website
- Each triggers a full-screen CSS overlay with a one-second gratitude animation
- After the animation, a feedback textarea form appears for the visitor to write a message
- On submission, the form opens the visitor's email client pre-addressed to `freelivingdesigns@gmail.com`
- Implemented entirely in CSS using `:target` = no JavaScript needed.
- Because this solution uses `mailto:`, submission depends on the visitor having a desktop mail client configured as their system default. During testing, this worked reliably with Outlook, but browser-only email setups such as Gmail may not handle the form in the same way. This is a known limitation of `mailto:` when no JavaScript or backend form handler is used.

---

## Challenges Faced and Ideas Tested

**Video fullscreen on embedded previews:**
Early testing showed the native fullscreen button was unresponsive when viewing the file in code editors built-in browser. This was not a CSS or HTML problem — it was a restriction of the embedded webview environment. Opening the file in Chrome resolved it. I learned to always test media in a real browser from the start.

**Keeping navigation on one line on mobile:**
My first attempt used `flex-wrap: wrap` which caused the nav links to stack on small screens. I switched to `flex-wrap: nowrap` on mobile and reduced font size and padding at the base level, restoring them at the 640px breakpoint. This keeps the nav horizontal on all screen sizes.

**Menu jump issue and final dropdown behavior:**
I initially tested a hash-based menu opener that caused the page to jump when Menu was clicked because the browser tried to scroll to the target position. I also tested a hover-style version, but that made the submenu harder to use because it could disappear while moving the mouse downward. The final solution uses a CSS-only target pattern linked to a hidden fixed-position state element, so clicking Menu opens the dropdown in place without scrolling the page, and selecting About Me or Portfolio changes the target to that section and closes the menu automatically.

**CSS-only overlay forms:**
Implementing the feedback modals without JavaScript required the `:target` pattern to show and hide overlays via anchor link clicks. I also used CSS animation delays to show the gratitude message first, then reveal the feedback textarea one second later. This required careful layering of `opacity`, `visibility`, and `pointer-events` to work reliably across browsers.

---

## Validation

**CSS Validation**

The stylesheet was validated using the W3C CSS Validation Service:
https://jigsaw.w3.org/css-validator/

Result: **No CSS syntax errors found in styles.css**
Added visual images of W3C CSS Validation badges in footer.

**HTML Validation**

The page markup was validated using the W3C Markup Validation Service:
https://validator.w3.org/

Result: **No HTML errors found in index.html**

---

## Final Reflection

This assignment helped me improve how I approach front-end development from a mobile-first perspective. I became more confident using Flexbox and CSS Grid together, structuring semantic HTML, and creating interactive features using only CSS. I am most proud of turning the site into a cleaner, more professional portfolio with stronger accessibility and responsive behavior across screen sizes. Going forward, I want to keep refining visual polish, test even earlier across browsers, and continue building more advanced interactions while keeping performance and usability at the center of my work. I am excited to submit this work as it reflects a true passion and understanding of html and CSS in action for the marker to experience thru my project.

## Final Submission Checklist

- Responsive mobile-first CSS completed with tablet and desktop breakpoints
- Flexbox and CSS Grid both used appropriately
- Navigation, hover states, and animation effects completed
- Two-step scroll-to-top control completed
- Emoji feedback overlay flow completed (CSS-only)
- W3C CSS validation completed and evidence captured
- W3C HTML validation completed
- README updated to final submission version

With that said, I hope you enjoy the project I present you and am very eager to jump into Javascript in the next module.
---

Kind Regards,
Tom Black

---


