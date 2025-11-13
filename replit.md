# Dynasty Gallery

## Overview

Dynasty Gallery is a multi-artist marketplace platform enabling artists to sell original artwork and premium prints. It offers a curated gallery experience, professional fulfillment through print-on-demand integration, and operates on a commission-based revenue model (20-30% per sale). The platform is a full-stack web application designed with a bold, professional aesthetic to showcase diverse artistic expression, functioning as both an e-commerce platform for collectors and a sales channel for independent artists.

**Branding:** The platform logo displays "Dynasty Gallery ∞ 28" with a custom infinity symbol and "28" styled in the primary brand color. The infinity symbol represents limitless artistic potential and the union of artists and collectors.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture
- **Framework & Tooling**: React 18+ with TypeScript, Vite, Wouter (routing), TanStack Query (server state).
- **UI Component System**: shadcn/ui (Radix UI), Tailwind CSS with custom design tokens.
- **Design Philosophy**: Art-first presentation, generous whitespace, bold professionalism, responsive grid layouts (masonry-style), custom HSL color system, distinctive typography (Playfair Display, Inter, Space Grotesk).

### Backend Architecture
- **Server Framework**: Express.js on Node.js with TypeScript.
- **API Design**: RESTful API (`/api/*`), Zod for request validation, JSON response format, consistent error handling.
- **Business Logic**: Storage abstraction (`IStorage`), separation of concerns, commission tracking.

### Data Storage
- **Database**: PostgreSQL (Neon serverless) with Drizzle ORM for type-safe queries and migrations.
- **Schema Design**: `users`, `artists`, `artworks`, `cartItems`, `orders` tables.
- **Key Relationships**: Artworks linked to Artists, Cart items to Artworks. Session-based cart isolation.

### Authentication & Authorization
- **Replit Auth Integration**: Full Replit Auth (Google, GitHub, X, Apple, email/password) for user sign-in.
- **Session Management**: Express-session with PostgreSQL session store (`connect-pg-simple`), 7-day session cookies.
- **Security**: Server-side user ID extraction from JWT, protected API endpoints, `isAdmin` flag for admin authorization.

### Feature Specifications

#### Search and Filter System (Saatchi Art-style)
- **Capabilities**: Keyword search (artwork titles, artist names, tags, descriptions), real-time results.
- **Filter Options**:
  - Price range slider (£0-£100,000)
  - Multiple medium selections (Oil, Acrylic, Digital, Watercolor, Mixed Media, Photography, Sculpture)
  - Subject categories (Abstract, Animals, Architecture, Beach, Birds, Botanical, Cities, Fantasy, Figurative, Floral, Food & Drink, Landscape, Nature, People, Portrait, Seascape, Still Life, Street Art, Urban)
  - Style dropdown (Abstract, Contemporary, Modern, Realism, Impressionism, Expressionism, Minimalism, Pop Art)
  - Orientation filters (Portrait, Landscape, Square, Panoramic - calculated from width/height ratio)
  - Size filters (Small, Medium, Large, Extra Large - based on artwork dimensions)
  - Artwork Type filter (Original, Print, Both - distinguishes original paintings from prints)
  - Tag-based filtering (clickable badges) - 50 tags including mood (dreamy, dramatic, serene), color themes (vibrant, pastel, dark), techniques (textured, smooth, layered), and styles (vintage, modern, minimalist)
- **Sorting Options**: Newest, Price (Low/High), Title (A-Z).
- **UI/UX**: Side sheet filter panel, active filter badges with individual remove buttons, clear all filters, filter count indicator.
- **Technical**: Server-side filtering via query parameters, React Query for dynamic updates, orientation/size calculated from artwork dimensions.

#### Artist Onboarding System
- **Registration**: Artists register via Replit Auth, submit profile (name, bio, location, image), application defaults to "pending".
- **Artist Dashboard**: View profile, approval status, helpful messaging for pending artists.
- **Admin Panel**: Admin-only page to review, approve/reject artist applications, filter by status, view statistics.
- **Security**: Requires authentication, server-side `userId` and `approvalStatus` assignment, `isAdmin` check for admin access.

#### Artist Subscription Pricing System
- **Pricing Tiers**: Pay-as-you-go (£4.40/upload), Monthly (£8/month for unlimited), Annual (£35/year for unlimited).
- **Trial Period**: 7-day free trial for new artists, server-side controlled.
- **Subscription Management**: Artists view/switch plans, trial status, upload limits, in dashboard.
- **Promo Code System**: Admin-assigned promo codes for individual artists to waive fees/commission.
- **Revenue Model**: 25% platform commission on sales (waivable by promo code).

#### Donation System
- **Capabilities**: Standalone donation feature allowing visitors to support the gallery without purchasing artwork.
- **Donation Options**: Preset amounts (£1, £3, £5, £10) and custom amount input (minimum £1).
- **Payment Processing**: Stripe checkout integration in payment mode (one-time donations, not recurring).
- **User Experience**: Dedicated /donate page with amount selection, impact messaging, and secure checkout flow.
- **Navigation**: "Support" button in header navigation, donation section on About page.
- **State Management**: Clean preset-to-custom amount switching with automatic state reset.
- **Security**: Server-side amount validation, Stripe hosted checkout, no authentication required.
- **Success Handling**: Redirects to /about?donation=success after successful donation.

#### Currency Filter System
- **Supported Currencies**: British Pounds (£/GBP) and Euros (€/EUR)
- **Conversion Rate**: Static rate of 1 GBP = 1.17 EUR
- **UI Location**: Currency toggle (£/€ buttons) next to sort dropdown in gallery filters
- **Persistence**: Currency preference saved in localStorage and persists across page navigation and sessions
- **Coverage**: All price displays updated including:
  - Gallery artwork cards
  - Artwork detail page (original artwork price, all print size options)
  - Shopping cart (item prices, subtotal, commission, total)
  - Filter panel price range display
- **State Management**: Global CurrencyContext provides currency state to all components
- **Technical**: All prices stored in GBP in database, converted for display using formatPrice utility function

#### theprintspace API Integration
- **Purpose**: Professional print-on-demand fulfillment for artists to create physical prints from their digital artwork
- **API Authentication**: Production API key stored in THEPRINTSPACE_API_KEY environment secret, bearer token authentication
- **Backend Endpoints**:
  - POST /api/printspace/orders - Creates print order, validates image URL, submits to theprintspace API
  - GET /api/printspace/orders - Retrieves artist's print orders
- **Product Types**: Maps to theprintspace product IDs:
  - Giclée A3: "giclee-a3"
  - C-Type A4: "ctype-a4"
  - C-Type A3: "ctype-a3"
  - C-Type A2: "ctype-a2"
- **Order Flow**:
  1. Artist uploads artwork via /artist/upload
  2. Optional checkbox to create print order
  3. Artist selects product type and enters shipping address
  4. Image validation (URL accessibility, resolution, format)
  5. Backend submits order to theprintspace API
  6. Database stores order with printspaceOrderId and status tracking
- **Data Captured**: Product type, shipping address (name, address lines, city, postcode, country), image URL, artist reference
- **Status Tracking**: pending → submitted/failed, displayed in artist dashboard with error messages
- **Security**: Backend-only API access, authenticated artist-only endpoints, server-side validation
- **Image Requirements**: Publicly accessible URL, supported formats (JPEG, PNG), adequate resolution

#### Artwork Visualizer
- **Purpose**: Professional mockup generator enabling artists to create marketing images showing their artwork in realistic room settings with accurate scaling
- **Route**: /artist/visualizer (accessible from artist dashboard)
- **Technology**: HTML5 Canvas with unified pointer events (mouse + touch support)
- **Canvas Features**:
  - Upload artwork image (drag to position on canvas)
  - **12 preset room backgrounds** across 4 categories:
    - Modern (4): Modern White Wall, Industrial Brick Wall, Contemporary Space, Wooden Wall
    - Gallery (3): Dark Gallery, Minimalist Gallery, White Gallery Space
    - Classic (3): Classic Interior, Elegant Sitting Room, Luxury Interior
    - Lifestyle (2): Cozy Living Room, Modern Bedroom
  - Custom background upload option
  - **Realistic Size Calibration**: Input actual artwork dimensions in centimeters (1-500cm range)
  - **Image Cropping Tool**: Drag-to-select crop area with visual overlay, removes unwanted backgrounds
  - 5 frame styles (none, modern black, classic white, ornate gold, natural wood)
  - 4 lighting filters (none, warm, cool, dramatic) using canvas filter API
  - Size slider (20-200% scale control) working with real-world dimensions
  - Pointer capture for smooth cross-device dragging
- **Realistic Scaling System**:
  - Canvas represents 300cm (3 meter) wide wall
  - Artists input width & height in cm (default: 60cm × 80cm)
  - Automatic pixel conversion: 800px canvas = 300cm wall (2.67 pixels per cm)
  - Artwork displays at accurate scale relative to room background
- **Cropping Functionality**:
  - Opens in dialog with interactive canvas
  - Drag to draw crop rectangle on uploaded image
  - Visual overlay darkens excluded areas, white border shows selection
  - Applies crop to preserve original image quality
  - Useful for isolating artwork from photos taken on walls
- **User Flow**:
  1. Artist uploads artwork image (device file upload)
  2. Sets actual dimensions in cm for realistic scale
  3. Optional: Opens crop tool to refine image (remove background/frame)
  4. Selects preset or custom room background
  5. Adjusts artwork position via drag-and-drop (touch + mouse)
  6. Selects frame style and lighting filter
  7. Adjusts size with slider (percentage of actual dimensions)
  8. Downloads final mockup as PNG (800x600px)
- **Cross-Device Support**: Unified pointer events (onPointerDown/Move/Up) with touch-none CSS, ensuring full functionality on desktop, tablet, and mobile for both canvas manipulation and cropping
- **UI/UX**: Responsive grid layout, dimension inputs appear immediately, crop button shows after upload, controls update dynamically, reset button to clear canvas, download button generates PNG file
- **Navigation**: "Artwork Visualizer" button in artist dashboard "Manage Your Artworks" card

## External Dependencies

- **Payment Processing**: Stripe for secure payment handling (Stripe React components), payment intent tracking, webhook signature verification, server-side price calculation.
- **Print-on-Demand Services**: theprintspace API integration for professional print fulfillment. Production API key (production-FVGGHFPKJ2wFhqX6BtpK4FlPRxrth25d) stored in THEPRINTSPACE_API_KEY secret. Orders tracked in printOrders table.
- **Image Hosting**: Currently uses external URLs (e.g., Unsplash for placeholders). Assets stored in `attached_assets` directory.
- **Development Tools**: Replit-specific plugins, Google Fonts API.
- **Database Infrastructure**: Neon serverless PostgreSQL with WebSocket support, Drizzle Kit for migrations.