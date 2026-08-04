# Requirements Document

## Introduction

A simple yet unique single-page school website built with HTML5, CSS (Tailwind via CDN), and vanilla JavaScript. The site presents a school's brand through a cohesive navy/white/gold color palette, rich interactive elements (scroll animations, counters, lightbox, testimonial carousel, dark/light mode toggle), and a fully responsive mobile-first layout. The output is three files — `index.html`, `style.css`, and `script.js` — intended for static hosting with no build step required.

## Glossary

- **Site**: The complete school website delivered as three static files.
- **Navbar**: The sticky top navigation bar containing the school logo placeholder and navigation links.
- **Hero**: The full-viewport opening section with the school name, tagline, and CTA button.
- **Card**: A discrete UI block used in Programs, News, and Testimonials sections.
- **Counter**: An animated numeric display that counts up from zero to a target value when scrolled into view.
- **Lightbox**: A modal overlay that displays a full-size image when a gallery thumbnail is clicked.
- **Scroll_Reveal**: A fade-in/slide-up entrance animation applied to elements as they enter the viewport.
- **Intersection_Observer**: The browser API used to trigger Scroll_Reveal animations and Counter start.
- **Dark_Mode**: An alternate color theme applied to the entire page when the user activates the toggle.
- **CTA**: Call-to-action button ("Enroll Now") in the Hero section.
- **Tailwind**: The Tailwind CSS framework loaded via CDN `<script>` tag.
- **Google_Fonts**: Montserrat (headings) and Inter (body) loaded via a single `<link>` tag.
- **Font_Awesome**: Icon library loaded via CDN `<link>` tag.

---

## Requirements

### Requirement 1: File Structure and Technical Foundation

**User Story:** As a developer, I want the site delivered in exactly three well-commented files, so that I can host it statically without a build step.

#### Acceptance Criteria

1. THE Site SHALL consist of exactly three files: `index.html`, `style.css`, and `script.js`.
2. THE `index.html` file SHALL load Tailwind CSS via CDN `<script>` tag, Google_Fonts via `<link>` tag, Font_Awesome via CDN `<link>` tag, `style.css` via `<link>` tag, and `script.js` via `<script defer>` tag.
3. THE `style.css` file SHALL define CSS custom properties in `:root` for the primary color (`#0A1F44`), secondary color (`#FFFFFF`), accent color (`#D4AF37`), and their dark-mode overrides.
4. THE Site SHALL use semantic HTML5 elements — `<header>`, `<nav>`, `<section>`, `<article>`, `<footer>` — to structure each page section.
5. THE `index.html` file SHALL include well-placed comments identifying each major section.
6. THE `script.js` file SHALL include well-placed comments explaining each major feature implementation.

---

### Requirement 2: Navbar

**User Story:** As a visitor, I want a sticky navigation bar at the top of the page, so that I can jump to any section without scrolling back up.

#### Acceptance Criteria

1. THE Navbar SHALL have a solid navy (`#0A1F44`) background with white text links.
2. THE Navbar SHALL display a text-based school logo placeholder on the left and navigation links — Home, About, Programs, Gallery, News, Contact — on the right.
3. WHILE the page is scrolled past the top, THE Navbar SHALL remain fixed at the top of the viewport (`position: sticky` or `position: fixed`).
4. WHEN a navigation link is clicked, THE Site SHALL smooth-scroll to the corresponding section.
5. WHEN the viewport width is below 768 px, THE Navbar SHALL collapse the navigation links into a hamburger menu icon.
6. WHEN the hamburger menu icon is clicked, THE Navbar SHALL toggle the visibility of the navigation link list.

---

### Requirement 3: Hero Section

**User Story:** As a visitor, I want an impactful opening section, so that I immediately understand the school's identity and can take action to enroll.

#### Acceptance Criteria

1. THE Hero SHALL display a large headline containing the school name and a tagline below it.
2. THE Hero SHALL render a CTA button labeled "Enroll Now" that smooth-scrolls to the Contact section when clicked.
3. THE Hero SHALL apply a navy-to-white CSS gradient as the background.
4. THE Hero SHALL overlay a subtle geometric SVG or CSS pattern on the gradient background.
5. WHEN the page is scrolled, THE Hero background SHALL shift vertically at a reduced speed (parallax effect) relative to the scroll position.
6. THE Hero SHALL be at least 100 vh in height on desktop viewports.

---

### Requirement 4: About School Section

**User Story:** As a prospective student or parent, I want to read the school's vision and mission, so that I can decide if it aligns with my values.

#### Acceptance Criteria

1. THE About section SHALL present the school's vision and mission text in readable paragraphs.
2. THE About section SHALL use a two-column layout on desktop (text on one side, an illustrative icon or image placeholder on the other).
3. WHEN the viewport width is below 768 px, THE About section SHALL stack the columns into a single-column layout.
4. WHEN the About section enters the viewport, THE Scroll_Reveal animation SHALL fade in and slide up the section content.

---

### Requirement 5: Featured Programs Section

**User Story:** As a prospective student, I want to browse offered programs at a glance, so that I can identify which majors interest me.

#### Acceptance Criteria

1. THE Programs section SHALL display 3 to 4 program cards in a responsive grid (3–4 columns on desktop, 2 on tablet, 1 on mobile).
2. EACH program card SHALL contain a Font_Awesome icon, a program name, and a short description.
3. WHEN a program card is hovered, THE Card SHALL apply a lift effect (translate-Y) and a gold (`#D4AF37`) border highlight.
4. WHEN the Programs section enters the viewport, THE Scroll_Reveal animation SHALL apply a staggered fade-in to each card.

---

### Requirement 6: Statistics / Achievements Section

**User Story:** As a visitor, I want to see key school statistics displayed prominently, so that I can quickly gauge the school's scale and success.

#### Acceptance Criteria

1. THE Statistics section SHALL display at least four counters: total students, total teachers, achievements/awards, and alumni.
2. EACH Counter SHALL display the numeric value animated from 0 to the target value over approximately 2 seconds.
3. WHEN the Statistics section enters the viewport, THE Intersection_Observer SHALL start each Counter animation exactly once.
4. THE Statistics section SHALL display a descriptive label beneath each Counter value.

---

### Requirement 7: Gallery Section

**User Story:** As a visitor, I want to browse school photos, so that I can get a feel for the campus and activities.

#### Acceptance Criteria

1. THE Gallery SHALL display at least 6 image thumbnails in a CSS grid layout.
2. WHEN a thumbnail is clicked, THE Lightbox SHALL open and display the full-size version of the clicked image.
3. WHEN the Lightbox is open, THE Lightbox SHALL display a close button ("×") that dismisses the overlay when clicked.
4. WHEN the Lightbox is open and the user presses the Escape key, THE Lightbox SHALL close.
5. WHEN the Lightbox is open, THE Lightbox SHALL prevent the page body from scrolling.
6. WHEN the Gallery section enters the viewport, THE Scroll_Reveal animation SHALL fade in the thumbnails.

---

### Requirement 8: Latest News Section

**User Story:** As a visitor, I want to see recent news articles, so that I can stay informed about school activities.

#### Acceptance Criteria

1. THE News section SHALL display exactly 3 news cards.
2. EACH news card SHALL contain a placeholder image, an article title, a publish date, and a short excerpt.
3. THE News section SHALL use a 3-column grid on desktop, 2 columns on tablet, and 1 column on mobile.
4. WHEN the News section enters the viewport, THE Scroll_Reveal animation SHALL fade in the cards.

---

### Requirement 9: Testimonials Section

**User Story:** As a prospective student or parent, I want to read testimonials from current students or alumni, so that I can build trust in the school.

#### Acceptance Criteria

1. THE Testimonials section SHALL present at least 3 testimonial slides in a carousel/slider.
2. EACH testimonial slide SHALL display a quote, the speaker's name, and the speaker's role (e.g., "Student" or "Alumni").
3. THE Testimonials carousel SHALL include previous and next navigation controls.
4. WHEN a navigation control is activated, THE carousel SHALL transition to the adjacent slide smoothly.
5. THE carousel SHALL loop from the last slide back to the first slide, and vice versa.

---

### Requirement 10: Contact & Map Section

**User Story:** As a prospective student, I want to submit an inquiry and see the school's location on a map, so that I can plan a visit or ask questions.

#### Acceptance Criteria

1. THE Contact section SHALL include a form with fields for full name, email address, and message.
2. WHEN the form is submitted with any field empty, THE Site SHALL display an inline validation error message next to the empty field and prevent form submission.
3. WHEN the form is submitted with an email field that does not match a valid email format, THE Site SHALL display an inline validation error and prevent submission.
4. WHEN the form is submitted successfully (all fields valid), THE Site SHALL display a success confirmation message and reset the form fields.
5. THE Contact section SHALL display the school's address and phone number.
6. THE Contact section SHALL embed a Google Maps `<iframe>` showing the school's location.

---

### Requirement 11: Footer

**User Story:** As a visitor, I want a clear footer with contact info and social links, so that I can find secondary information without returning to the top.

#### Acceptance Criteria

1. THE Footer SHALL have a navy (`#0A1F44`) background with white text.
2. THE Footer SHALL display the school name, contact information, social media icon links (at minimum: Facebook, Instagram, Twitter/X), and a copyright notice.
3. THE Footer social media links SHALL open in a new browser tab.

---

### Requirement 12: Dark/Light Mode Toggle

**User Story:** As a visitor, I want to switch between dark and light themes, so that I can comfortably read the site in different lighting conditions.

#### Acceptance Criteria

1. THE Navbar SHALL include a toggle button (icon-based) for switching between Dark_Mode and the default light mode.
2. WHEN the Dark_Mode toggle is activated, THE Site SHALL apply a dark color scheme across all sections by toggling a CSS class on the `<html>` or `<body>` element.
3. WHEN the Dark_Mode toggle is deactivated, THE Site SHALL restore the default light color scheme.
4. WHEN the page is reloaded, THE Site SHALL restore the previously selected theme using `localStorage`.

---

### Requirement 13: Scroll Reveal Animations

**User Story:** As a visitor, I want page sections to animate into view as I scroll, so that the browsing experience feels dynamic and engaging.

#### Acceptance Criteria

1. THE Scroll_Reveal system SHALL use the Intersection_Observer API to detect when elements enter the viewport.
2. WHEN a scroll-reveal element enters the viewport, THE element SHALL transition from opacity 0 and a downward offset to opacity 1 and its natural position.
3. THE Scroll_Reveal animation SHALL trigger exactly once per element (not re-trigger on scroll-up).
4. THE `style.css` file SHALL define the initial hidden state and the revealed state as CSS classes.

---

### Requirement 14: Responsive Design

**User Story:** As a mobile visitor, I want the site to render correctly on any device, so that I can browse comfortably on a phone or tablet.

#### Acceptance Criteria

1. THE Site SHALL be built mobile-first, with base styles targeting small screens and Tailwind responsive prefixes (`md:`, `lg:`) for larger breakpoints.
2. THE Site SHALL render without horizontal overflow on viewports from 320 px to 1920 px wide.
3. THE Hero section SHALL stack headline and CTA vertically on mobile viewports.
4. ALL grid layouts (Programs, Gallery, News) SHALL reduce to a single column on mobile viewports (below 640 px).
