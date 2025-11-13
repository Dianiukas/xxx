# Dynasty Gallery - Design Guidelines

## Design Approach

**Reference-Based Approach**: Drawing inspiration from premium art marketplaces (Artsy, Saatchi Art) and creative e-commerce platforms (Society6, SSENSE) to create a bold, professional gallery experience that celebrates both art and artist individuality.

### Core Design Principles
1. **Art-First Presentation**: Generous whitespace and minimal distraction to let artwork command attention
2. **Bold Professionalism**: Confident typography and layout that signals credibility and quality
3. **Inclusive Warmth**: Accessible design that welcomes collectors and artists of all backgrounds
4. **Movement & Energy**: Dynamic layouts that reflect the "Art that moves" brand promise

---

## Typography

**Font Families** (via Google Fonts):
- **Display/Headers**: 'Playfair Display' (serif) - elegant, gallery-appropriate, commands presence
- **Body/UI**: 'Inter' (sans-serif) - clean, highly readable, professional
- **Accents**: 'Space Grotesk' (sans-serif) - for artist names, prices, bold statements

**Type Scale**:
- Hero Headlines: text-6xl to text-7xl (Playfair Display, font-bold)
- Page Titles: text-4xl to text-5xl (Playfair Display, font-semibold)
- Section Headers: text-3xl (Space Grotesk, font-bold)
- Subsections: text-xl to text-2xl (Space Grotesk, font-medium)
- Body Text: text-base to text-lg (Inter, font-normal)
- Captions/Meta: text-sm (Inter, font-medium)
- Artist Names: text-lg (Space Grotesk, tracking-wide, uppercase)

---

## Layout System

**Spacing Primitives**: Tailwind units of 2, 4, 6, 8, 12, 16, 20, 24
- Micro spacing: p-2, gap-2 (tight elements)
- Component spacing: p-4, p-6, gap-4 (cards, buttons)
- Section padding: py-12, py-16, py-20 (content areas)
- Page margins: px-4 (mobile), px-8 (tablet), px-12 to px-16 (desktop)

**Grid Structure**:
- Homepage Gallery: Masonry-style grid with varying card sizes (1-4 columns responsive)
- Artist Collections: 3-column grid (desktop), 2-column (tablet), 1-column (mobile)
- Featured Artwork: Asymmetric hero layouts with 60/40 or 70/30 splits
- Max Container Width: max-w-7xl for content, max-w-prose for long-form text

**Vertical Rhythm**:
- Mobile sections: py-12 to py-16
- Desktop sections: py-20 to py-24
- Hero sections: min-h-screen or 80vh with proper content flow

---

## Component Library

### Navigation
- **Primary Nav**: Fixed header with Dynasty Gallery wordmark (Space Grotesk, bold), transparent initially, solid on scroll
- **Menu Items**: Shop, Artists, About, Contact (Inter, text-sm, tracking-wide, uppercase)
- **Cart Icon**: Top right with item count badge
- **Mobile**: Slide-out menu with full-height overlay, large touch targets

### Homepage Components

**Hero Section** (min-h-screen):
- Large featured artwork image (70% width) with asymmetric text placement
- Headline: "Where individuality meets opportunity" (Playfair Display, text-6xl)
- Subhead with mission statement (Inter, text-xl)
- Primary CTA: "Explore Gallery" button with backdrop blur when over image
- Scrolling brand values ticker at bottom

**Featured Gallery Grid**:
- Masonry layout with mixed card sizes (Pinterest-inspired)
- Cards show: Artwork image, artist name, title, price, "View Details" on hover
- No rigid spacing - dynamic, organic arrangement
- Infinite scroll or "Load More" pattern

**Artist Spotlight Section**:
- Rotating carousel or 3-column grid of featured artists
- Large circular artist photos with names and signature style
- "Meet the Artist" CTAs leading to profile pages

**Curated Collections**:
- Horizontal scrolling sections for themes (Seasonal, Abstract, Portraits)
- Bold section headers (Space Grotesk, text-3xl)
- 4-6 artworks per row with smooth scroll behavior

### Artwork Detail Pages

**Layout**: Two-column split (image left 60%, details right 40%)

**Image Gallery**:
- Primary image with high-resolution zoom capability
- Thumbnail navigation below
- Full-screen lightbox option

**Details Panel**:
- Artist name (large, Space Grotesk, clickable to profile)
- Artwork title (Playfair Display, text-3xl)
- Medium, dimensions, year
- Price (Space Grotesk, text-4xl, bold)
- Print options toggle (Original vs. Print sizes)
- "Add to Cart" primary button (full-width, large)
- Artist statement/description (Inter, text-base)
- Social share buttons

### Artist Profile Pages

**Header**: Full-width banner with artist photo, name, bio, location
**Artist Statement**: max-w-prose centered text block
**Portfolio Grid**: 3-column gallery of their available works
**Contact/Follow Section**: Social links, follow button, inquiry form

### Shopping Cart & Checkout

**Cart Drawer**: Slide-out from right with:
- Line items showing thumbnail, title, artist, price, quantity controls
- Subtotal with commission breakdown visible
- Sticky "Checkout" button at bottom

**Checkout Flow**: Clean, single-page Stripe integration
- Shipping and billing forms (clear labels, generous spacing)
- Order summary sidebar
- Trust signals (secure payment badges, return policy link)

### Admin Dashboard

**Layout**: Sidebar navigation (Artists, Artworks, Orders, Settings)
**Tables**: Clean, sortable data tables for artwork and order management
**Forms**: Artist/artwork upload with image preview, drag-and-drop
**Analytics Cards**: Sales stats, trending pieces, artist performance

---

## Imagery Guidelines

**Hero Section**: Large, professionally photographed artwork in gallery setting - aspirational but authentic
**Artwork Images**: High-resolution, consistent lighting, multiple angles for detail pages
**Artist Photos**: Professional but approachable headshots, circular crops
**About/Mission Pages**: Candid studio shots, artists at work, diverse representation
**Background Textures**: Subtle canvas or paper textures for depth (very low opacity)

**Image Treatment**:
- Maintain aspect ratios (no distortion)
- Lazy loading for performance
- Hover effects: subtle zoom (scale-105) on gallery cards
- Sharp, clean edges - no heavy filters

---

## Interactions & Animation

**Use Sparingly**:
- Smooth scroll behavior for navigation
- Fade-in on scroll for gallery items (stagger delay for masonry grid)
- Card hover: gentle lift (translate-y-1) with subtle shadow increase
- Button states: background opacity changes, no elaborate transitions
- Page transitions: Simple fade between routes

**Avoid**: Auto-playing carousels, parallax effects, heavy animations that distract from artwork

---

## Forms & Inputs

- Floating labels for all text inputs
- Large touch targets (min-height of h-12)
- Clear error states with helpful messaging
- Radio buttons for print size selection (large, visual)
- File upload with drag-and-drop and preview for admin
- Consistent border treatment across all inputs

---

## Responsive Behavior

**Breakpoints**:
- Mobile: Single-column layouts, stacked cards
- Tablet (md:): 2-column grids, reduced hero imagery
- Desktop (lg:): Full multi-column masonry, asymmetric layouts
- Wide (xl:): Max-width containers maintain readability

**Mobile-Specific**:
- Bottom navigation bar for quick access (Shop, Artists, Cart)
- Simplified headers with hamburger menu
- Touch-optimized gallery with swipe gestures
- Larger tap targets for all interactive elements

---

This design system creates a professional, art-forward experience that honors both the creators and collectors while maintaining the bold, inclusive spirit of Dynasty Gallery's brand promise.