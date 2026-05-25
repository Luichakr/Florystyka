# Vittoria Fiore Gallery

Luxury floral studio website by Viktoriya — premium B2B floral design for hotels, restaurants, car dealerships, and corporate spaces.

**Live preview:** [luichakr.github.io/Florystyka](https://luichakr.github.io/Florystyka/)

Or open `index.html` locally in any modern browser.

## Highlights

- Single-file HTML/CSS/JS prototype — no build step
- Dark / light theme toggle with `localStorage` persistence
- Responsive: desktop / tablet / mobile (≤720) / small phone (≤380) / large screen (≥1600)
- Modal form system with 5 source-labeled lead types: B2B quote, Bouquet order, Wedding, Portfolio inquiry, Workshop
- Editorial typography: Cormorant Garamond + Inter
- Scroll-reveal animations (IntersectionObserver)
- SEO-ready FAQ accordion

## Form sources

Each form submits with a hidden `source` field so the backend (and Viktoriya) knows where each lead originated:

| source | trigger |
|---|---|
| `b2b-quote` | Hero CTA, "−10% B2B" strip, nav "Dla firm", footer B2B links |
| `bouquet-order` | Each product card (with prefilled product), footer "Bukiety bespoke" |
| `wedding-inquiry` | Nav "Ślub", footer "Florystyka ślubna" |
| `portfolio-inquiry` | Each portfolio case (with prefilled project name) |
| `workshop-inquiry` | Nav "Warsztaty", footer "Warsztaty" |
| `main-contact` | Main contact form at bottom of page |
| `newsletter` | Footer newsletter signup |

Currently submissions log to `console.log('[VFG lead]', ...)`. Backend integration point ready for Formspree / Resend / custom endpoint.

## Tech

Plain HTML/CSS/JS. No frameworks, no dependencies. Designed to be ported to Next.js for the production site at [vittoriagallery.com](https://www.vittoriagallery.com).
