# Implementation Plan: School Website

## Overview

Build the static school website as three files (`index.html`, `style.css`, `script.js`).
Tasks are ordered so each step is immediately usable in a browser and builds on the previous one.
All interactivity is vanilla JS; no build step is needed.

---

## Tasks

- [x] 1. Set up file scaffolding and CDN dependencies
  - Create `index.html` with `<!DOCTYPE html>`, `<html lang="en">`, `<head>`, and empty `<body>`.
  - Add `<link>` for Google Fonts (Montserrat + Inter, single tag), Font Awesome CDN `<link>`, and `style.css` `<link>` in `<head>`.
  - Add Tailwind CSS CDN `<script>` tag in `<head>`.
  - Add `<script defer src="script.js">` before `</body>`.
  - Create `style.css` with `:root` block defining `--color-primary: #0A1F44`, `--color-secondary: #FFFFFF`, `--color-accent: #D4AF37` and their `.dark`-mode overrides.
  - Create empty `script.js` with a `DOMContentLoaded` listener as the entry point and section comments for each feature module.
  - Add HTML section comments for each major section.
  - _Requirements: 1.1, 1.2, 1.3, 1.5, 1.6_

  - [ ]* 1.1 Write unit tests for file scaffolding
    - Verify Tailwind CDN `<script>`, Google Fonts `<link>`, Font Awesome `<link>`, `style.css` `<link>`, and `script.js` `<script defer>` are all present in `index.html`.
    - Verify `:root` defines `--color-primary`, `--color-secondary`, `--color-accent`.
    - _Requirements: 1.2, 1.3_

- [x] 2. Implement Navbar markup and sticky behaviour
  - Add `<header id="navbar">` containing `<nav>` with the school logo `<a>` on the left and a `<ul>` of six navigation links (Home, About, Programs, Gallery, News, Contact) on the right.
  - Add hamburger `<button id="hamburger-btn">` (Font Awesome bars icon) visible only on mobile.
  - Apply Tailwind classes for navy background (`bg-[#0A1F44]`), white text, `sticky top-0 z-50`.
  - In `script.js` "Navbar" module: implement hamburger click handler that toggles `nav-open` class on the `<nav>` element.
  - Add CSS rule `.nav-open ul { display: flex; }` and default `ul { display: none; }` on mobile; on `md:` breakpoint `ul { display: flex; }`.
  - Add `scroll-behavior: smooth` to `html` in `style.css`.
  - _Requirements: 2.1, 2.2, 2.3, 2.5, 2.6_

  - [ ]* 2.1 Write unit test for hamburger toggle
    - Simulate a click on `#hamburger-btn` and assert that `nav-open` class is added to `<nav>`.
    - Simulate a second click and assert `nav-open` is removed.
    - _Requirements: 2.6_

- [x] 3. Implement smooth-scroll navigation
  - In the "Navbar" module, add a click listener to each nav `<a>` link.
  - On click: call `document.querySelector(href).scrollIntoView({ behavior: 'smooth' })` and close the mobile menu.
  - _Requirements: 2.4_

- [x] 4. Implement Hero section
  - Add `<section id="hero">` with `min-h-screen` and navy-to-white CSS gradient background.
  - Add a geometric SVG or `::before` CSS pseudo-element pattern over the gradient.
  - Add headline `<h1>` (school name), `<p>` tagline, and `<a href="#contact">` CTA button labelled "Enroll Now".
  - Apply Tailwind `flex flex-col items-center justify-center text-center` on mobile; layout classes as needed.
  - In `script.js` "Parallax" module: add a `scroll` event listener that sets `hero.style.backgroundPositionY = window.scrollY * 0.4 + 'px'`.
  - _Requirements: 3.1, 3.2, 3.3, 3.4, 3.5, 3.6, 14.3_

  - [ ]* 4.1 Write property test for parallax offset (Property 1)
    - **Property 1: Parallax offset is always less than scroll position**
    - Generate random non-negative scroll positions; assert that computed offset (`y * 0.4`) is always less than or equal to `y`.
    - **Validates: Requirements 3.5**

- [x] 5. Implement Scroll Reveal system
  - In `style.css`, define `.scroll-hidden { opacity: 0; transform: translateY(24px); transition: opacity 0.6s ease, transform 0.6s ease; }` and `.scroll-revealed { opacity: 1; transform: translateY(0); }`.
  - In `script.js` "Scroll Reveal" module: create one `IntersectionObserver` with `threshold: 0.15` that, on intersection, adds `.scroll-revealed` to the element then calls `observer.unobserve(entry.target)`.
  - Add `class="scroll-hidden"` to the About section, each program card, each gallery thumbnail, each news card, and the Testimonials section container.
  - _Requirements: 13.1, 13.2, 13.3, 13.4_

  - [ ]* 5.1 Write property test for scroll reveal exactly once (Property 10)
    - **Property 10: Scroll reveal triggers exactly once per element**
    - Create a mock element with `scroll-hidden`; simulate the observer callback firing multiple times; assert `.scroll-revealed` is present and `.scroll-hidden` is absent after any number of callbacks.
    - **Validates: Requirements 13.2, 13.3**

- [x] 6. Implement About section
  - Add `<section id="about" class="scroll-hidden">` with a two-column grid (`md:grid-cols-2 grid-cols-1`).
  - Left column: `<p>` vision text and `<p>` mission text inside a `<div>`.
  - Right column: decorative `<div>` containing a Font Awesome icon or image placeholder.
  - _Requirements: 4.1, 4.2, 4.3, 4.4_

- [x] 7. Implement Programs section
  - Add `<section id="programs">` with a responsive grid `grid-cols-1 sm:grid-cols-2 lg:grid-cols-4`.
  - Add 4 `<div class="program-card scroll-hidden">` elements, each with a Font Awesome `<i>`, `<h3>` name, and `<p>` description.
  - In `style.css`, add `.program-card:hover { transform: translateY(-6px); border-color: var(--color-accent); }` and `transition` on the card.
  - In `script.js`, after the observer reveals a card, read its `data-delay` attribute and set `el.style.transitionDelay = el.dataset.delay + 'ms'` before adding `.scroll-revealed`.
  - Set `data-delay="0"`, `"100"`, `"200"`, `"300"` on the four cards respectively.
  - _Requirements: 5.1, 5.2, 5.3, 5.4_

  - [ ]* 7.1 Write property test for program card required elements (Property 2)
    - **Property 2: All program cards contain required elements**
    - For each rendered `.program-card`, assert it contains an `<i>` element, a non-empty `<h3>`, and a non-empty `<p>`.
    - **Validates: Requirements 5.2**

  - [ ]* 7.2 Write property test for staggered reveal delays (Property 2 related)
    - For any set of n program cards, assert each card has a `data-delay` value equal to its index multiplied by 100.
    - **Validates: Requirements 5.4**

- [x] 8. Implement Statistics / Counters section
  - Add `<section id="stats">` with four `<div class="counter-item">` blocks.
  - Each block: `<span class="counter" data-target="N">0</span>` and `<p>` label (e.g., Students, Teachers, Awards, Alumni).
  - In `script.js` "Counter" module: implement `animateCounter(el, target, duration = 2000)` using `setInterval` at 16 ms ticks, incrementing by `Math.ceil(target / (duration / 16))` per tick, stopping at target.
  - Create one `IntersectionObserver` for `.counter` elements; on intersection call `animateCounter` then `observer.unobserve(entry.target)`.
  - _Requirements: 6.1, 6.2, 6.3, 6.4_

  - [ ]* 8.1 Write property test for counter reaches target (Property 3)
    - **Property 3: Counter animation reaches its target**
    - Generate random non-negative integer targets; run `animateCounter` to completion with a mock element (using fake timers); assert final text equals target.
    - **Validates: Requirements 6.2**

  - [ ]* 8.2 Write property test for counter exactly once (Property 4)
    - **Property 4: Counter animation triggers exactly once**
    - Simulate multiple IntersectionObserver callbacks on a single counter element; assert `animateCounter` was called at most once.
    - **Validates: Requirements 6.3, 13.3**

- [x] 9. Implement Gallery section and Lightbox
  - Add `<section id="gallery">` with `grid-cols-2 md:grid-cols-3`.
  - Add 6 `<figure class="scroll-hidden">` elements each containing `<img src="placeholder.jpg" data-full="placeholder.jpg" alt="...">`.
  - Add `<div id="lightbox" class="hidden fixed inset-0 ...">` overlay with `<img id="lightbox-img">` and `<button id="lightbox-close">×</button>`.
  - In `script.js` "Lightbox" module:
    - Each thumbnail click: set `lightbox-img` src from `data-full`, remove `hidden` from overlay, add `overflow-hidden` to `document.body`.
    - Close button click and `Escape` keydown: add `hidden` back, remove `overflow-hidden`.
  - _Requirements: 7.1, 7.2, 7.3, 7.4, 7.5, 7.6_

  - [ ]* 9.1 Write unit tests for Lightbox
    - Simulate thumbnail click: assert lightbox overlay is visible and `document.body` has `overflow-hidden`.
    - Simulate close button click: assert lightbox is hidden and `overflow-hidden` is removed.
    - Simulate `Escape` keydown: assert lightbox closes.
    - _Requirements: 7.2, 7.3, 7.4, 7.5_

- [x] 10. Implement News section
  - Add `<section id="news">` with `grid-cols-1 sm:grid-cols-2 lg:grid-cols-3`.
  - Add 3 `<article class="news-card scroll-hidden">` elements each containing:
    `<img>` placeholder, `<h3>` title, `<time datetime="YYYY-MM-DD">` date, `<p>` excerpt.
  - _Requirements: 8.1, 8.2, 8.3, 8.4_

  - [ ]* 10.1 Write property test for news card required elements (Property 11)
    - **Property 11: All news cards contain required elements**
    - For each `.news-card`, assert it contains a non-empty `<h3>`, a `<time>` element, and a non-empty `<p>`.
    - **Validates: Requirements 8.2**

- [x] 11. Implement Testimonials Carousel
  - Add `<section id="testimonials">` containing a `<div class="carousel relative overflow-hidden">`.
  - Add at least 3 `<div class="slide">` elements, each with `<blockquote>` quote, `<cite>` name, and `<span>` role.
  - Add `<button id="prev">‹</button>` and `<button id="next">›</button>` navigation controls.
  - In `script.js` "Carousel" module: initialise `currentIndex = 0`; implement `navigate(dir)` using `(currentIndex + dir + slides.length) % slides.length`; implement `updateCarousel()` which adds/removes an `active` class; call `updateCarousel()` on init.
  - In `style.css`: `.slide { opacity: 0; position: absolute; transition: opacity 0.4s; }` and `.slide.active { opacity: 1; position: relative; }`.
  - _Requirements: 9.1, 9.2, 9.3, 9.4, 9.5_

  - [ ]* 11.1 Write property test for carousel wrap-around (Property 5)
    - **Property 5: Carousel navigation wraps correctly**
    - Generate random slide counts (2–10) and current index; assert `navigate(+1)` from last slide returns 0, and `navigate(-1)` from 0 returns last.
    - **Validates: Requirements 9.4, 9.5**

- [~] 12. Checkpoint — verify all sections render correctly
  - Ensure all tests pass, ask the user if questions arise.

- [x] 13. Implement Contact Form with validation
  - Add `<section id="contact">` with `<form id="contact-form">`.
  - Add three fields with sibling `<span class="field-error hidden">`:
    `<input name="fullname">`, `<input name="email" type="email">`, `<textarea name="message">`.
  - Add `<div id="success-message" class="hidden">` for the confirmation message.
  - Add static address and phone number text.
  - Add Google Maps `<iframe>` with `loading="lazy"` and a placeholder `src`.
  - In `script.js` "Form" module:
    - Implement `validateEmail(email)` using regex `/^[^\s@]+@[^\s@]+\.[^\s@]+$/`.
    - Implement `validateForm(data)` returning `{}` on valid, or an object with field error messages.
    - On `submit`: call `validateForm`, show inline errors if any, otherwise show success message and reset form.
  - _Requirements: 10.1, 10.2, 10.3, 10.4, 10.5, 10.6_

  - [ ]* 13.1 Write property test for email validation (Property 6)
    - **Property 6: Email validation correctly classifies inputs**
    - Generate valid emails (e.g., `user@domain.com` templates) and invalid strings (missing `@`, missing domain, whitespace); assert `validateEmail` returns correct boolean for each.
    - **Validates: Requirements 10.3**

  - [ ]* 13.2 Write property test for form validation rejects empty fields (Property 7)
    - **Property 7: Form validation rejects any submission with empty fields**
    - Generate `FormData` objects where at least one field is empty or whitespace-only; assert `validateForm` returns a non-empty errors object.
    - **Validates: Requirements 10.2**

  - [ ]* 13.3 Write unit test for successful form submission
    - Fill all fields with valid data; simulate submit; assert `#success-message` is visible and form fields are reset.
    - _Requirements: 10.4_

- [x] 14. Implement Footer
  - Add `<footer>` with navy background, white text.
  - Include school name, address, phone number, social media icon links (Facebook, Instagram, Twitter/X) using Font Awesome icons, each with `target="_blank" rel="noopener noreferrer"`.
  - Include copyright notice `© [year] School Name. All rights reserved.`.
  - _Requirements: 11.1, 11.2, 11.3_

  - [ ]* 14.1 Write unit test for footer links
    - Assert all social media `<a>` elements have `target="_blank"`.
    - _Requirements: 11.3_

- [x] 15. Implement Dark / Light Mode Toggle
  - In the Navbar, add `<button id="theme-toggle">` with a Font Awesome sun/moon icon.
  - In `<head>`, add an inline `<script>` (before any other scripts) that reads `localStorage.getItem('theme')` and adds class `dark` to `<html>` if the stored value is `'dark'`.
  - In `:root.dark` in `style.css`, define overrides for `--color-primary`, `--color-secondary`.
  - In `script.js` "Dark Mode" module: on toggle click, check if `<html>` has class `dark`:
    - If yes: remove `dark`, store `'light'` in `localStorage`.
    - If no: add `dark`, store `'dark'` in `localStorage`.
  - _Requirements: 12.1, 12.2, 12.3, 12.4_

  - [ ]* 15.1 Write property test for dark mode round trip (Property 8)
    - **Property 8: Dark mode toggle is its own inverse**
    - Simulate toggling dark mode twice from any initial state; assert `<html>` class and `localStorage` value return to their original state.
    - **Validates: Requirements 12.2, 12.3**

  - [ ]* 15.2 Write property test for theme persistence (Property 9)
    - **Property 9: Theme persists across reload simulation**
    - Write `'dark'` and `'light'` to mock `localStorage`; call the init function; assert `<html>` class matches stored value in both cases.
    - **Validates: Requirements 12.4**

- [x] 16. Apply responsive design polish and verify grid layouts
  - Review all grid containers (Programs, Gallery, News) and confirm each has `grid-cols-1` at the base breakpoint.
  - Review Hero section for `flex-col` on mobile and stacked headline/CTA layout.
  - Add `max-w-full` and `overflow-x-hidden` to `<body>` in `style.css` to prevent horizontal overflow.
  - Verify About two-column layout uses `md:grid-cols-2 grid-cols-1`.
  - _Requirements: 14.1, 14.2, 14.3, 14.4_

  - [ ]* 16.1 Write property test for mobile grid single-column (Property 12)
    - **Property 12: All grid layouts have a single-column mobile class**
    - For each of the three grid section containers (Programs, Gallery, News), assert the element's class list contains `grid-cols-1`.
    - **Validates: Requirements 14.4**

- [x] 17. Final checkpoint — full integration pass
  - Ensure all tests pass, ask the user if questions arise.
  - Verify the page opens in a browser from the file system without errors.
  - Confirm all sections are present in the page, all interactive features function, and no console errors appear.

---

## Notes

- Tasks marked with `*` are optional and can be skipped for a faster MVP.
- Each task references specific requirements for traceability.
- Checkpoints (tasks 12 and 17) ensure incremental validation at meaningful milestones.
- Property tests validate universal correctness properties (use [fast-check](https://github.com/dubzzz/fast-check) for JS, minimum 100 iterations per property).
- Unit tests validate specific examples, edge cases, and DOM structure.
- All CDN links are loaded from `index.html` — no npm or build tooling needed.

---

## Task Dependency Graph

```json
{
  "waves": [
    { "id": 0, "tasks": ["1.1"] },
    { "id": 1, "tasks": ["2.1"] },
    { "id": 2, "tasks": ["4.1", "5.1"] },
    { "id": 3, "tasks": ["7.1", "7.2", "8.1", "8.2", "9.1", "10.1", "11.1"] },
    { "id": 4, "tasks": ["13.1", "13.2", "13.3", "14.1", "15.1", "15.2", "16.1"] }
  ]
}
```
