# Online Gaming Website: Project Instruction Document

**Reference Website:** https://www.rockstargames.com
**Category:** Web Development

---

## Purpose of This Document

This document defines the complete requirements, behaviour, and expected deliverables for building an Online Gaming Website modelled after Rockstar Games (rockstargames.com). It is written for the development team and serves as the single source of truth for everything that must be built. Every page, component, system, and output described here must be implemented exactly as specified. Nothing in this document is optional unless explicitly stated.

---

## Table of Contents

1. [Overview](#1-overview)
2. [Tech Stack Required](#2-tech-stack-required)
3. [Folder Structure](#3-folder-structure)
4. [Page Specifications](#4-page-specifications)
5. [Component Specifications](#5-component-specifications)
6. [User Account System](#6-user-account-system)
7. [Store and E-Commerce System](#7-store-and-e-commerce-system)
8. [Support Portal System](#8-support-portal-system)
9. [Search System](#9-search-system)
10. [Design System and Theming](#10-design-system-and-theming)
11. [Responsive Design Requirements](#11-responsive-design-requirements)
12. [Performance Requirements](#12-performance-requirements)
13. [SEO Requirements](#13-seo-requirements)
14. [Accessibility Requirements](#14-accessibility-requirements)
15. [Deliverables](#15-deliverables)
16. [File Formats](#16-file-formats)
17. [Explicit Ask](#17-explicit-ask)

---

## 1. Overview

### Project Purpose

Build a premium, production-quality online gaming website that replicates the design language, structure, and core functionality of rockstargames.com. The website serves as the central digital presence of a fictional AAA gaming studio, providing users with game discovery, news, media content, an online store, user accounts, and player support.

### Product Summary

The website is a multi-page, server-rendered web application featuring a cinematic dark-themed design. It presents a curated game library with individual detail pages, a Newswire blog for studio announcements, a video hub for trailers and gameplay content, an e-commerce store for games and merchandise, a user authentication system with profile management, and a player support portal. All pages share a consistent global navigation bar with centred logo, a global search system, and a comprehensive footer.

### Target Audience

- Gamers aged 16–40 who play AAA open-world, action-adventure, and multiplayer games
- Gaming journalists and content creators seeking official assets and press materials
- Potential customers browsing games and merchandise for purchase
- Existing players managing their accounts, viewing stats, and seeking support

### Core Functionality

- Browse and filter a complete game catalog by franchise, platform, and year
- Read news articles, patch notes, and event announcements via the Newswire
- Watch official trailers and gameplay videos in a dedicated video hub
- Purchase games and merchandise through an integrated store
- Create and manage user accounts with profile dashboards and game stats
- Submit support tickets and browse a help knowledge base
- Search across all content types from a global search bar

---

## 2. Tech Stack Required

### Frontend Framework

| Technology | Purpose |
|---|---|
| Next.js 14+ (App Router) | React-based framework with server-side rendering, static generation, and file-system routing |
| React 18+ | Component library for building the user interface |
| TypeScript | Type-safe development across all frontend code |

### Styling

| Technology | Purpose |
|---|---|
| CSS Modules or Vanilla CSS | Component-scoped styling with no CSS-in-JS runtime overhead |
| CSS Custom Properties | Design tokens for colours, spacing, typography, and animations |
| Google Fonts (Inter, Roboto Condensed) | Typography matching the modern gaming aesthetic |

### Backend and Database

| Technology | Purpose |
|---|---|
| Next.js API Routes | Server-side API endpoints for authentication, data fetching, and form submissions |
| Node.js 20+ | Runtime environment for the backend |
| MongoDB with Mongoose | Database for storing user accounts, game data, articles, products, and support tickets |
| Cloudinary or local /public folder | Image and video asset hosting and optimization |

### Authentication

| Technology | Purpose |
|---|---|
| NextAuth.js (Auth.js) | Authentication library handling registration, login, session management, and JWT tokens |
| bcrypt | Password hashing for secure credential storage |

### Third-Party Integrations

| Technology | Purpose |
|---|---|
| Stripe (test/sandbox mode) | Payment processing for the store checkout flow |
| Nodemailer or Resend | Transactional emails for verification, password reset, and order confirmation |
| YouTube IFrame API | Embedding and controlling video playback in the video hub and game detail pages |

### Development Tools

| Tool | Purpose |
|---|---|
| ESLint | JavaScript and TypeScript linting |
| Prettier | Code formatting |
| Husky + lint-staged | Pre-commit hooks for code quality enforcement |
| Jest + React Testing Library | Unit and integration testing |
| Playwright | End-to-end testing for critical user flows |

---

## 3. Folder Structure

```
project-root/
├── app/
│   ├── layout.tsx                    # Root layout with global nav and footer
│   ├── page.tsx                      # Homepage
│   ├── globals.css                   # Global styles and CSS custom properties
│   ├── games/
│   │   ├── page.tsx                  # Games library page
│   │   └── [slug]/
│   │       └── page.tsx              # Individual game detail page
│   ├── newswire/
│   │   ├── page.tsx                  # Newswire article list page
│   │   └── [slug]/
│   │       └── page.tsx              # Individual article page
│   ├── videos/
│   │   └── page.tsx                  # Video hub page
│   ├── store/
│   │   ├── page.tsx                  # Store product catalog page
│   │   ├── [productId]/
│   │   │   └── page.tsx              # Individual product detail page
│   │   ├── cart/
│   │   │   └── page.tsx              # Shopping cart page
│   │   └── checkout/
│   │       └── page.tsx              # Checkout page
│   ├── account/
│   │   ├── login/
│   │   │   └── page.tsx              # Login page
│   │   ├── register/
│   │   │   └── page.tsx              # Registration page
│   │   ├── profile/
│   │   │   └── page.tsx              # User profile dashboard
│   │   ├── settings/
│   │   │   └── page.tsx              # Account settings page
│   │   ├── verify-email/
│   │   │   └── page.tsx              # Email verification page
│   │   └── reset-password/
│   │       └── page.tsx              # Password reset page
│   ├── support/
│   │   ├── page.tsx                  # Support portal landing page
│   │   ├── articles/
│   │   │   └── [slug]/
│   │   │       └── page.tsx          # Individual help article page
│   │   ├── submit-ticket/
│   │   │   └── page.tsx              # Submit a ticket page
│   │   ├── status/
│   │   │   └── page.tsx              # Service status page
│   │   └── faq/
│   │       └── page.tsx              # FAQ page
│   ├── about/
│   │   └── page.tsx                  # About the studio page
│   ├── downloads/
│   │   └── page.tsx                  # Downloads page (launchers, wallpapers)
│   ├── search/
│   │   └── page.tsx                  # Search results page
│   └── api/
│       ├── auth/
│       │   └── [...nextauth]/
│       │       └── route.ts          # NextAuth API route
│       ├── games/
│       │   └── route.ts              # Games CRUD API
│       ├── articles/
│       │   └── route.ts              # Newswire articles API
│       ├── products/
│       │   └── route.ts              # Store products API
│       ├── tickets/
│       │   └── route.ts              # Support tickets API
│       ├── search/
│       │   └── route.ts              # Global search API
│       └── newsletter/
│           └── route.ts              # Newsletter subscription API
├── components/
│   ├── layout/
│   │   ├── Navbar.tsx                # Global navigation bar
│   │   ├── Footer.tsx                # Global footer
│   │   ├── MobileMenu.tsx            # Mobile slide-out menu
│   │   └── SearchBar.tsx             # Expandable global search bar
│   ├── home/
│   │   ├── HeroCarousel.tsx          # Homepage hero carousel
│   │   ├── FeaturedGames.tsx         # Featured games grid section
│   │   ├── LatestNews.tsx            # Latest Newswire articles section
│   │   └── FlagshipSection.tsx       # Flagship game promotional section
│   ├── games/
│   │   ├── GameCard.tsx              # Game tile card for library grid
│   │   ├── GameFilters.tsx           # Filter and sort controls
│   │   ├── ScreenshotGallery.tsx     # Lightbox screenshot gallery
│   │   └── SystemRequirements.tsx    # System requirements table
│   ├── newswire/
│   │   ├── ArticleCard.tsx           # Article preview card
│   │   ├── ArticleContent.tsx        # Full article body renderer
│   │   └── CategoryFilter.tsx        # Category filter tabs
│   ├── videos/
│   │   ├── VideoCard.tsx             # Video thumbnail card
│   │   ├── VideoPlayer.tsx           # Modal or inline video player
│   │   └── VideoFilters.tsx          # Video filter controls
│   ├── store/
│   │   ├── ProductCard.tsx           # Product listing card
│   │   ├── ProductGallery.tsx        # Product image gallery with zoom
│   │   ├── CartItem.tsx              # Individual cart item row
│   │   └── CheckoutForm.tsx          # Checkout form with payment
│   ├── account/
│   │   ├── LoginForm.tsx             # Login form component
│   │   ├── RegisterForm.tsx          # Registration form component
│   │   ├── ProfileDashboard.tsx      # User profile overview
│   │   └── SettingsForm.tsx          # Account settings form
│   ├── support/
│   │   ├── TicketForm.tsx            # Support ticket submission form
│   │   ├── StatusIndicator.tsx       # Service status badge
│   │   └── FaqAccordion.tsx          # Collapsible FAQ section
│   └── ui/
│       ├── Button.tsx                # Reusable button component
│       ├── Card.tsx                  # Reusable card wrapper
│       ├── Modal.tsx                 # Modal/overlay component
│       ├── Badge.tsx                 # Badge/tag component
│       ├── Loader.tsx                # Loading spinner/skeleton
│       ├── Toast.tsx                 # Toast notification component
│       └── Pagination.tsx            # Pagination controls
├── lib/
│   ├── db.ts                         # MongoDB connection utility
│   ├── auth.ts                       # NextAuth configuration
│   ├── stripe.ts                     # Stripe client configuration
│   ├── email.ts                      # Email sending utility
│   └── utils.ts                      # General utility functions
├── models/
│   ├── User.ts                       # User Mongoose model
│   ├── Game.ts                       # Game Mongoose model
│   ├── Article.ts                    # Article Mongoose model
│   ├── Product.ts                    # Product Mongoose model
│   ├── Order.ts                      # Order Mongoose model
│   ├── Ticket.ts                     # Support ticket Mongoose model
│   └── Newsletter.ts                 # Newsletter subscriber model
├── hooks/
│   ├── useSearch.ts                  # Search functionality hook
│   ├── useCart.ts                    # Shopping cart state hook
│   └── useAuth.ts                   # Authentication state hook
├── context/
│   ├── CartContext.tsx               # Shopping cart context provider
│   └── ThemeContext.tsx              # Theme context provider
├── public/
│   ├── images/                       # Static images (logos, icons, placeholders)
│   ├── videos/                       # Self-hosted video files (if any)
│   ├── fonts/                        # Local font files (if not using Google Fonts CDN)
│   ├── favicon.ico                   # Site favicon
│   └── robots.txt                    # Robots configuration
├── data/
│   ├── games.json                    # Seed data for games library
│   ├── articles.json                 # Seed data for Newswire articles
│   ├── products.json                 # Seed data for store products
│   └── faq.json                      # FAQ content data
├── types/
│   └── index.ts                      # TypeScript type definitions
├── __tests__/
│   ├── components/                   # Component unit tests
│   ├── pages/                        # Page integration tests
│   └── e2e/                          # End-to-end Playwright tests
├── .env.local                        # Environment variables (not committed)
├── .env.example                      # Environment variable template
├── next.config.js                    # Next.js configuration
├── tsconfig.json                     # TypeScript configuration
├── package.json                      # Dependencies and scripts
├── README.md                         # Project documentation
└── seed.ts                           # Database seeding script
```

### Directory Explanations

| Directory | Purpose |
|---|---|
| `app/` | Next.js App Router pages and API routes. Each subdirectory maps to a URL route. |
| `components/` | Reusable React components organized by feature area. Each component has its own file. |
| `lib/` | Shared utility libraries for database, authentication, payment, and email. |
| `models/` | Mongoose schema definitions for all database collections. |
| `hooks/` | Custom React hooks for shared stateful logic. |
| `context/` | React context providers for global state (cart, theme). |
| `public/` | Static assets served directly by the web server. |
| `data/` | JSON seed data files used to populate the database during development. |
| `types/` | Shared TypeScript interfaces and type definitions. |
| `__tests__/` | All test files organized by test type. |

---

## 4. Page Specifications

### 4.1 Homepage (`/`)

The homepage is the first page users see when visiting the website. It must create a cinematic, immersive first impression that immediately communicates the premium nature of the gaming studio.

**Hero Carousel Section**

The top of the page features a full-viewport-width hero carousel. The carousel must support a minimum of 5 slides. Each slide consists of a full-bleed background image or autoplaying muted video, a game title logo overlaid in the centre or left-aligned, a short tagline or call-to-action text, and a primary action button (e.g., "Learn More", "Pre-Order Now", "Watch Trailer"). The carousel auto-rotates every 6 seconds. Navigation indicators (dots or thin bars) appear at the bottom centre. On mobile, swipe gestures navigate between slides. On desktop, arrow buttons appear on hover at the left and right edges. Transition between slides uses a smooth crossfade animation lasting 800 milliseconds.

**Clickable Navigation Chips**

Directly below the carousel, a horizontally scrollable row of pill-shaped chips provides quick links to featured game landing pages. Each chip displays a game icon and short label. On hover, the chip elevates slightly with a subtle shadow. On mobile, the row is swipeable.

**Latest Newswire Section**

Below the chips, a section titled "Latest News" displays the 4 most recent Newswire articles in a 2×2 grid on desktop and a single-column stack on mobile. Each article card shows a thumbnail image, category tag badge, title, publish date, and a 2-line excerpt. Clicking a card navigates to the full article page.

**Flagship Game Sections**

Two full-width promotional sections follow, one for each major online game title. Each section contains an autoplaying muted background video (or fallback image), the game logo, a brief description paragraph, and two action buttons (e.g., "Play Now" and "Learn More"). These sections use parallax scrolling effects where the background video scrolls at a slower rate than the foreground content.

**Newsletter Signup**

A dark-gradient banner section with a heading "Stay Connected", a subheading "Get the latest news delivered to your inbox", an email input field, and a "Subscribe" button. On submission, the email is saved to the newsletter subscriber database and a success toast notification appears.

---

### 4.2 Games Library Page (`/games`)

This page displays the complete catalog of game titles in a visually rich grid layout.

**Filter Bar**

A horizontal filter bar at the top of the page contains:
- Franchise dropdown: All, Grand Theft Auto, Red Dead Redemption, Max Payne, L.A. Noire, Bully, Midnight Club, Other
- Platform dropdown: All, PC, PlayStation 5, PlayStation 4, Xbox Series X|S, Xbox One, Nintendo Switch, Mobile
- Release Year dropdown: All, then each year from current year down to 1998
- Sort dropdown: Newest First (default), Oldest First, A–Z, Z–A

Filters apply immediately without a page reload. The URL query string updates to reflect active filters so filtered views are shareable.

**Game Grid**

Games display in a responsive grid: 4 columns on desktop, 3 on tablet, 2 on mobile. Each game card shows:
- Cover art image filling the card
- Game title overlaid at the bottom with a dark gradient backdrop
- On hover: the image scales up by 5%, a coloured border-glow effect appears matching the game's brand colour, and a "View Game" button fades in at the centre

If no games match the active filters, a "No games found" message displays with a "Clear Filters" button.

---

### 4.3 Game Detail Page (`/games/[slug]`)

Each game has a dedicated detail page accessible via its URL slug.

**Hero Section**

A full-width hero banner spanning the viewport width and 60% of viewport height. The background is a high-resolution key art image with a dark overlay gradient (transparent at top, 90% black at bottom). Overlaid content includes the game logo image (not text), the game's tagline, platform availability badges displayed as small icons, and a primary "Buy Now" or "Pre-Order" button.

**Overview Section**

A two-column layout on desktop (single column on mobile). The left column contains the game description as rich text with 2–4 paragraphs covering storyline, setting, and gameplay. The right column contains a vertical list of key features, each with an icon and a short label (e.g., "Open World", "Multiplayer", "Online Mode").

**Media Section**

**Trailer**: An embedded YouTube video player showing the latest official trailer. The player must be responsive and maintain a 16:9 aspect ratio.

**Screenshot Gallery**: A grid of 6–12 screenshot thumbnails. Clicking a thumbnail opens a full-screen lightbox modal. The lightbox displays the image at full resolution with previous/next navigation arrows, a close button (X) in the top right corner, and keyboard navigation (arrow keys for navigation, Escape to close). Thumbnail grid: 3 columns desktop, 2 tablet, 1 mobile.

**System Requirements Section** (PC titles only)

A two-column table displaying minimum and recommended specifications side by side. Required fields: OS, Processor, Memory, Graphics, DirectX, Storage, Sound Card. If the game is not available on PC, this section is hidden entirely.

**Related News Section**

A row of 3 article cards from the Newswire filtered to articles tagged with this game's title. Layout and card design match the Newswire article cards used elsewhere.

---

### 4.4 Newswire Page (`/newswire`)

The studio's official blog for news, updates, and community content.

**Category Tabs**

A horizontal tab bar at the top with options: All, Updates, Events, Patch Notes, Community. The active tab is visually highlighted with an underline accent in the studio's brand colour. Switching tabs filters articles without a full page reload.

**Article List**

Articles display in a single-column feed. Each article entry shows:
- A large thumbnail image (16:9 aspect ratio) spanning the full content width
- A category badge in the top left corner of the image
- The article title as a heading below the image
- Publish date and estimated reading time
- A 3-line text excerpt
- A "Read More" link

Pagination controls appear at the bottom showing 10 articles per page. The URL updates with the page number.

---

### 4.5 Article Detail Page (`/newswire/[slug]`)

**Hero Image**: Full-width banner image at the top of the article.

**Article Metadata**: Category badge, publish date, author name, and estimated reading time displayed below the hero image.

**Article Body**: Rich text content rendered from stored HTML or Markdown. Must support headings (h2, h3), paragraphs, bold and italic text, bulleted and numbered lists, inline images with captions, embedded YouTube videos, block quotes, and code blocks.

**Social Sharing Bar**: Fixed or sticky bar with share buttons for Twitter/X, Facebook, Reddit, and a "Copy Link" button that copies the article URL to the clipboard and shows a "Copied!" tooltip.

**Related Articles**: A row of 3 related article cards at the bottom of the page.

---

### 4.6 Video Hub Page (`/videos`)

**Filter Bar**: Dropdown filters for Game Title and Video Type (All, Trailers, Gameplay, Behind the Scenes).

**Video Grid**: Responsive grid (3 columns desktop, 2 tablet, 1 mobile) of video cards. Each card shows:
- Thumbnail image with a centred play button overlay icon
- Video title below the thumbnail
- Game title and duration

Clicking a card opens a modal with an embedded YouTube player. The modal has a dark backdrop overlay, a close button (X), and the video title displayed above the player. Pressing Escape closes the modal.

---

### 4.7 Store Pages (`/store`, `/store/[productId]`, `/store/cart`, `/store/checkout`)

See Section 7 (Store and E-Commerce System) for full specifications.

---

### 4.8 Account Pages

See Section 6 (User Account System) for full specifications.

---

### 4.9 Support Pages

See Section 8 (Support Portal System) for full specifications.

---

### 4.10 About Page (`/about`)

A single scrolling page with the following sections:

**Studio History**: A narrative section with a heading "Our Story" and 3–4 paragraphs describing the fictional studio's founding, mission, and achievements. Accompanied by a timeline of major game releases displayed as a horizontal scrollable element on desktop and a vertical timeline on mobile.

**Leadership Team**: A grid of team member cards (4 columns desktop, 2 mobile). Each card shows a circular photo, name, title, and a 1-sentence bio.

**Locations**: An embedded interactive map (Google Maps embed or static image) showing studio office locations with pins and labels.

**Careers**: A section with a heading "Join Our Team", a brief description, and a "View Open Positions" button linking to an external careers page or a simple job listing.

---

### 4.11 Downloads Page (`/downloads`)

**Launcher Section**: A card for each platform's launcher with the platform icon, a description, download file size, and a "Download" button.

**Wallpapers Section**: A masonry grid of wallpaper images organized by game title. Each image has a hover overlay showing available resolutions. Clicking opens the full image in a new tab for saving.

**Press Kit**: A section with a "Download Press Kit" button that downloads a ZIP file containing logos, screenshots, and factsheets.

---

### 4.12 Search Results Page (`/search`)

Triggered when the user submits a query from the global search bar. Results are displayed in tabbed sections: All, Games, News, Videos, Support. Each result shows a thumbnail (where applicable), title, type badge, and a brief excerpt. Results are paginated at 10 per page per tab.

---

## 5. Component Specifications

### 5.1 Global Navigation Bar (Navbar)

The navigation bar is sticky and remains at the top of the viewport on all pages.

**Desktop Layout**:
- Height: 72px
- Background: solid black (#000000) with 85% opacity and a backdrop blur of 12px
- Left section: Navigation links (Games, Newswire, Videos, Store, Support) in uppercase, 13px, Inter font, letter-spacing 2px
- Centre: Studio logo image, height 40px, linked to homepage
- Right section: Search icon (magnifying glass), User account icon (person silhouette)
- On scroll down beyond 100px: the background transitions to fully opaque black

**Mobile Layout**:
- Height: 56px
- Left: Hamburger menu icon (three horizontal lines)
- Centre: Studio logo, height 32px
- Right: Search icon
- Hamburger opens a full-screen slide-out menu from the left with all navigation links stacked vertically, plus Login/Register links at the bottom

**Search Bar Behaviour**:
Clicking the search icon expands an input field across the navigation bar width (desktop) or drops down a full-width search input (mobile). The input has a placeholder text "Search games, news, videos...". As the user types, an autocomplete dropdown appears with up to 5 suggestions grouped by type (Games, Articles, Videos). Pressing Enter or clicking "See all results" navigates to the search results page.

### 5.2 Footer

**Layout**: Four-column grid on desktop, single column on mobile.

- Column 1: Studio logo and 2-line tagline
- Column 2: Quick Links — Games, Newswire, Videos, Store, Support, About
- Column 3: Legal — Privacy Policy, Terms of Service, Cookie Policy, DMCA
- Column 4: Newsletter signup form (email input + Subscribe button)

**Bottom Bar**: A thin separator line, then a single row containing copyright text on the left, social media icons (Twitter/X, Instagram, YouTube, Facebook, TikTok) in the centre, and age rating badges (ESRB, PEGI) on the right.

Background colour: #0A0A0A. Text colour: #999999 for body, #FFFFFF for headings and links on hover.

---

## 6. User Account System

### 6.1 Registration (`/account/register`)

**Form Fields**:
- Username (required, 3–20 characters, alphanumeric and underscores only)
- Email (required, valid email format)
- Password (required, minimum 8 characters, at least 1 uppercase, 1 lowercase, 1 number, 1 special character)
- Confirm Password (must match Password)
- Terms of Service checkbox (required)

**Validation**: Real-time field validation with inline error messages below each field. The Submit button remains disabled until all validations pass.

**On Submit**: Create user record in MongoDB with hashed password (bcrypt, 12 salt rounds). Send verification email with a tokenized link valid for 24 hours. Redirect to a "Check Your Email" confirmation page.

### 6.2 Login (`/account/login`)

**Form Fields**:
- Email (required)
- Password (required)
- "Remember Me" checkbox

**On Submit**: Validate credentials against the database. On success, create a JWT session and redirect to the homepage. On failure, display "Invalid email or password" error without specifying which field is wrong.

**Additional Links**: "Forgot Password?" link below the form. "Don't have an account? Register" link below that.

### 6.3 Profile Dashboard (`/account/profile`)

**Requires Authentication**: Redirect to login page if not authenticated.

**Profile Header**: Avatar image (circle, 120px diameter) with an edit overlay icon, username, email, and "Member since [date]" label.

**Game Stats Section**: A grid of cards for each game the user has "played" (simulated data). Each card shows the game cover art, game title, hours played, achievements unlocked (e.g., "24/50"), and a progress bar.

**Recent Activity Feed**: A chronological list of recent actions (e.g., "Purchased GTA V", "Submitted support ticket", "Earned achievement"). Maximum 10 entries.

### 6.4 Account Settings (`/account/settings`)

Tabbed interface with sections:
- **Profile**: Edit username, email, and avatar upload
- **Security**: Change password (current password, new password, confirm new password)
- **Notifications**: Toggle switches for email notifications (newsletter, order updates, support replies)
- **Danger Zone**: "Delete Account" button with a confirmation modal requiring the user to type their username to confirm

### 6.5 Password Reset Flow

**Forgot Password Page** (`/account/reset-password`): Email input field and "Send Reset Link" button. On submit, generate a reset token valid for 1 hour and send email with tokenized link.

**Reset Password Page** (`/account/reset-password?token=...`): New password and confirm password fields. On submit, validate token, update password hash, invalidate all existing sessions, and redirect to login with "Password reset successful" toast.

---

## 7. Store and E-Commerce System

### 7.1 Product Catalog (`/store`)

**Category Navigation**: Horizontal tabs or sidebar: All, Games, Apparel, Collectibles, Accessories.

**Product Grid**: 4 columns desktop, 3 tablet, 2 mobile. Each product card shows:
- Product image (1:1 aspect ratio for merchandise, 3:4 for games)
- Product name
- Price (formatted as $XX.XX)
- Sale badge with original price struck through (if on sale)
- "Add to Cart" button that appears on hover (desktop) or is always visible (mobile)
- Quick-add animation: a brief flyout animation toward the cart icon in the navbar

**Sorting**: Price Low to High, Price High to Low, Newest, Best Selling.

### 7.2 Product Detail Page (`/store/[productId]`)

**Image Gallery**: Large primary image on the left with 4–6 thumbnail previews below. Clicking a thumbnail swaps the primary image. The primary image supports zoom on hover (2x magnification following cursor position).

**Product Info** (right column):
- Product name as h1
- Price with sale indicator if applicable
- Short description (2–3 sentences)
- Size selector (for apparel) with available sizes as clickable chips
- Colour selector (if applicable) as swatchable circles
- Quantity input (number spinner, min 1, max 10)
- "Add to Cart" primary button (full width)
- "Add to Wishlist" secondary button (outline style)

**Product Description Tab Section**: Tabs for Description, Specifications, and Reviews. Description contains the full product details. Specifications shows a key-value table. Reviews shows user ratings (placeholder/simulated data).

### 7.3 Shopping Cart (`/store/cart`)

**Cart Items**: Each row displays product thumbnail, name, selected options (size, colour), unit price, quantity spinner, row total, and a remove (trash icon) button. Quantity changes update the row total and cart total in real time.

**Cart Summary**: Subtotal, estimated shipping (flat rate $5.99 or free over $50), estimated tax (calculated as 8.5% of subtotal), and order total. "Proceed to Checkout" primary button. "Continue Shopping" text link.

**Empty Cart State**: An illustration or icon, "Your cart is empty" message, and a "Browse Store" button.

Cart data must persist across browser sessions using localStorage or a database-backed cart for authenticated users.

### 7.4 Checkout (`/store/checkout`)

**Step 1 — Shipping Information**: Form fields for first name, last name, email, phone, address line 1, address line 2, city, state/province, zip/postal code, country. All required except address line 2 and phone.

**Step 2 — Order Review**: Read-only summary of cart items, shipping address, and cost breakdown.

**Step 3 — Payment**: Stripe Elements embedded form for card number, expiration, CVC. Use Stripe test mode. "Place Order" button that creates a Stripe PaymentIntent, processes the charge, saves the order to the database, clears the cart, and redirects to an order confirmation page.

**Order Confirmation Page**: Displays order number, order summary, estimated delivery date, and a "Continue Shopping" button.

---

## 8. Support Portal System

### 8.1 Support Landing Page (`/support`)

**Search Bar**: Large centred search input with "How can we help?" placeholder. Results display inline below as the user types.

**Category Cards**: A grid of 6 category cards (Account Issues, Payment & Billing, Technical Support, Game Issues, Report a Player, General Inquiry). Each card has an icon, category name, and a brief description. Clicking navigates to filtered help articles for that category.

**Quick Links**: "Submit a Ticket" button and "Check Service Status" button prominently displayed.

### 8.2 Help Article Page (`/support/articles/[slug]`)

**Breadcrumb**: Support > Category > Article Title.

**Article Content**: Rendered rich text with step-by-step instructions, screenshots, and callout boxes for warnings or tips.

**Feedback**: "Was this article helpful?" with Yes/No buttons. On click, record the feedback and show "Thanks for your feedback" message.

**Related Articles**: 3 related article cards at the bottom.

### 8.3 Submit a Ticket (`/support/submit-ticket`)

**Requires Authentication**: Redirect to login if not authenticated.

**Form Fields**:
- Category dropdown (required): Account, Payment, Technical, Game Issue, Report Player, Other
- Game dropdown (required): list of all games plus "Not game-specific"
- Platform dropdown: PC, PlayStation, Xbox, Mobile
- Subject line (required, max 100 characters)
- Description textarea (required, max 2000 characters)
- File attachments (optional, max 3 files, max 5MB each, accepted formats: .png, .jpg, .gif, .pdf, .txt, .log)

**On Submit**: Save ticket to database with status "Open" and a generated ticket ID (format: TKT-XXXXXXX). Display confirmation with ticket ID and estimated response time. Send confirmation email to user.

### 8.4 Service Status Page (`/support/status`)

A table or card list showing each online game service with:
- Game name and icon
- Status indicator (green circle = Operational, yellow = Degraded Performance, red = Outage)
- Status text
- Last updated timestamp

**Incident History**: Below the status grid, a chronological log of recent incidents with date, affected service, description, and resolution status.

### 8.5 FAQ Page (`/support/faq`)

Collapsible accordion sections grouped by topic. Each section has a question as the header and an answer as the expandable body. Only one section can be expanded at a time. Smooth expand/collapse animation of 300ms.

---

## 9. Search System

### 9.1 Global Search API (`/api/search`)

**Input**: Query string parameter `q` with the search term. Optional filter parameter `type` (games, articles, videos, support).

**Behaviour**: Search across games (title, description), articles (title, body, tags), videos (title, game), and support articles (title, body). Return results ranked by relevance with a maximum of 50 results per type.

### 9.2 Autocomplete

The search bar input triggers autocomplete after the user has typed at least 3 characters. A dropdown shows up to 5 results grouped by type with small thumbnails. A debounce of 300ms prevents excessive API calls. Keyboard navigation (arrow keys + Enter) must work in the dropdown.

---

## 10. Design System and Theming

### 10.1 Colour Palette

| Token | Hex Value | Usage |
|---|---|---|
| `--color-bg-primary` | #000000 | Page backgrounds |
| `--color-bg-secondary` | #0A0A0A | Card and section backgrounds |
| `--color-bg-tertiary` | #141414 | Input fields, elevated surfaces |
| `--color-bg-hover` | #1A1A1A | Hover states for interactive surfaces |
| `--color-text-primary` | #FFFFFF | Headings, primary text |
| `--color-text-secondary` | #B3B3B3 | Body text, descriptions |
| `--color-text-muted` | #666666 | Metadata, timestamps, placeholders |
| `--color-accent-primary` | #FCAF17 | Primary buttons, active states, brand accent (Rockstar yellow) |
| `--color-accent-hover` | #E09A00 | Primary button hover state |
| `--color-accent-secondary` | #D85A30 | Secondary accent, alerts, sale badges |
| `--color-success` | #2ECC71 | Success states, operational status |
| `--color-warning` | #F39C12 | Warning states, degraded status |
| `--color-error` | #E74C3C | Error states, outage status, form errors |
| `--color-border` | #222222 | Default border colour |
| `--color-border-hover` | #333333 | Border hover state |

### 10.2 Typography

| Element | Font Family | Weight | Size | Line Height |
|---|---|---|---|---|
| h1 | Roboto Condensed | 700 | 48px (desktop), 32px (mobile) | 1.1 |
| h2 | Roboto Condensed | 700 | 36px (desktop), 28px (mobile) | 1.2 |
| h3 | Roboto Condensed | 600 | 24px (desktop), 20px (mobile) | 1.3 |
| Body | Inter | 400 | 16px | 1.6 |
| Body Small | Inter | 400 | 14px | 1.5 |
| Caption | Inter | 500 | 12px | 1.4 |
| Button | Inter | 600 | 14px, uppercase | 1.0 |
| Navigation | Inter | 500 | 13px, uppercase, letter-spacing 2px | 1.0 |

### 10.3 Spacing Scale

Base unit: 4px. Scale: 4, 8, 12, 16, 20, 24, 32, 40, 48, 64, 80, 96, 128.

All margins, paddings, and gaps must use values from this scale. No arbitrary spacing values are permitted.

### 10.4 Border Radius

| Element | Radius |
|---|---|
| Buttons | 4px |
| Cards | 8px |
| Input Fields | 4px |
| Modals | 12px |
| Avatars | 50% (circle) |
| Badges / Tags | 2px |

### 10.5 Shadows

| Level | Value |
|---|---|
| Subtle | 0 2px 4px rgba(0, 0, 0, 0.3) |
| Medium | 0 4px 12px rgba(0, 0, 0, 0.5) |
| Elevated | 0 8px 24px rgba(0, 0, 0, 0.7) |
| Glow (accent) | 0 0 20px rgba(252, 175, 23, 0.3) |

### 10.6 Animation Standards

| Property | Duration | Easing |
|---|---|---|
| Hover transitions | 200ms | ease-out |
| Page transitions | 400ms | ease-in-out |
| Modal open/close | 300ms | ease-out |
| Carousel slide | 800ms | ease-in-out |
| Accordion expand | 300ms | ease-out |
| Toast notification | 500ms | ease-out (enter), ease-in (exit) |
| Skeleton loading pulse | 1500ms | ease-in-out (infinite) |

All hover states must have smooth transitions. No instant property changes on interactive elements.

---

## 11. Responsive Design Requirements

### 11.1 Breakpoints

| Name | Width | Target |
|---|---|---|
| Mobile | 0–767px | Phones in portrait and landscape |
| Tablet | 768–1199px | Tablets and small laptops |
| Desktop | 1200–1919px | Standard desktop monitors |
| Wide | 1920px+ | Large and ultrawide monitors |

### 11.2 Layout Rules

- Maximum content width: 1400px, centred with auto margins
- Mobile: single-column layouts throughout, full-width cards and images
- Tablet: 2–3 column grids, collapsible sidebars
- Desktop: up to 4-column grids, persistent sidebars where applicable
- All interactive elements must have a minimum touch target of 44×44px
- No horizontal scrolling on any page at any breakpoint (except intentional carousels)

### 11.3 Image Handling

All images must use the Next.js `<Image>` component for automatic optimization. Provide srcset for responsive sizing. Use WebP format with JPEG fallback. Implement lazy loading for all below-the-fold images. Hero images and carousel backgrounds must maintain visual impact at all breakpoints using object-fit: cover.

---

## 12. Performance Requirements

| Metric | Target |
|---|---|
| Lighthouse Performance Score | ≥ 90 |
| First Contentful Paint (FCP) | ≤ 1.5 seconds |
| Largest Contentful Paint (LCP) | ≤ 2.5 seconds |
| First Input Delay (FID) | ≤ 100 milliseconds |
| Cumulative Layout Shift (CLS) | ≤ 0.1 |
| Time to Interactive (TTI) | ≤ 3.0 seconds |
| Total Page Weight (initial load) | ≤ 2 MB |
| Image Optimization | WebP format, lazy loading, srcset responsive sizes |
| JavaScript Bundle Size (per route) | ≤ 200 KB gzipped |
| API Response Time | ≤ 300ms for all endpoints |

### Mandatory Optimisations

- Server-side rendering (SSR) for SEO-critical pages (games, articles)
- Static site generation (SSG) for stable content pages (about, downloads, FAQ)
- Code splitting per route via Next.js dynamic imports
- Image lazy loading via Next.js Image component
- Font subsetting to include only Latin character set
- Database query indexing on all searchable and filterable fields
- Client-side caching of API responses with SWR or React Query

---

## 13. SEO Requirements

Every page must include:

| Tag | Requirement |
|---|---|
| `<title>` | Unique descriptive title, max 60 characters, format: "Page Name | Studio Name" |
| `<meta name="description">` | Unique description, max 155 characters |
| `<meta property="og:title">` | Match page title |
| `<meta property="og:description">` | Match meta description |
| `<meta property="og:image">` | Page-specific image (game art for game pages, article image for articles, studio logo for utility pages) |
| `<meta property="og:url">` | Canonical URL of the page |
| `<meta name="twitter:card">` | "summary_large_image" |
| `<link rel="canonical">` | Self-referencing canonical URL |

**Additional SEO Requirements**:
- Semantic HTML5 elements: `<header>`, `<main>`, `<nav>`, `<article>`, `<section>`, `<footer>`, `<aside>`
- Single `<h1>` per page
- Logical heading hierarchy (h1 → h2 → h3, no skipping levels)
- All images have descriptive `alt` attributes
- Sitemap.xml generated at build time listing all public pages
- robots.txt allowing all public pages and blocking /api/ routes
- Structured data (JSON-LD) for: Organization (homepage), VideoObject (videos), Product (store), Article (newswire)

---

## 14. Accessibility Requirements

The website must comply with WCAG 2.1 Level AA. The following specific requirements apply:

| Requirement | Standard |
|---|---|
| Colour Contrast (text) | Minimum 4.5:1 ratio for normal text, 3:1 for large text |
| Keyboard Navigation | All interactive elements reachable and operable via keyboard |
| Focus Indicators | Visible focus ring (2px solid var(--color-accent-primary)) on all focusable elements |
| ARIA Labels | All icons, buttons without text, and dynamic content regions must have aria-label or aria-labelledby |
| Skip Navigation | "Skip to main content" link as the first focusable element on every page |
| Form Labels | All form inputs have associated `<label>` elements |
| Error Announcements | Form validation errors announced to screen readers via aria-live regions |
| Alt Text | All meaningful images have descriptive alt text. Decorative images use alt="" |
| Reduced Motion | Respect `prefers-reduced-motion` media query by disabling animations |
| Language | `<html lang="en">` attribute on every page |

---

## 15. Deliverables

| ID | Deliverable | Type | Notes |
|---|---|---|---|
| D-01 | Homepage with hero carousel, latest news, flagship sections, newsletter signup | Frontend Page | Auto-rotating carousel with 5+ slides, parallax flagship sections |
| D-02 | Games Library page with filter and sort controls | Frontend Page | Filters update URL query string, responsive grid layout |
| D-03 | Game Detail pages with hero, overview, media, system requirements, related news | Frontend Page | Dynamic routes via [slug], lightbox gallery, embedded video player |
| D-04 | Newswire article list with category tabs and pagination | Frontend Page | 10 articles per page, category filtering without page reload |
| D-05 | Newswire article detail pages with rich content and social sharing | Frontend Page | Full rich-text rendering, sticky share bar, related articles |
| D-06 | Video Hub with filter controls and modal video player | Frontend Page | YouTube embed, keyboard-accessible modal, filter by game and type |
| D-07 | Store product catalog with category navigation | Frontend Page | Add-to-cart flyout animation, sale badge support |
| D-08 | Product detail pages with image zoom, size/colour selectors, add to cart | Frontend Page | Cursor-following zoom, variant selection, tab-based description |
| D-09 | Shopping cart with real-time quantity updates and cost breakdown | Frontend Page | Persists via localStorage/database, empty cart state |
| D-10 | Checkout flow with Stripe test-mode payment integration | Frontend Page | 3-step flow, order confirmation, email notification |
| D-11 | User registration with email verification | Full Stack | bcrypt hashing, tokenized verification link, 24-hour expiry |
| D-12 | User login with JWT session management | Full Stack | Secure HTTP-only cookies, remember me, rate limiting |
| D-13 | User profile dashboard with game stats and activity feed | Frontend Page | Authenticated route, avatar upload, simulated game data |
| D-14 | Account settings with password change and account deletion | Frontend Page | Confirmation modal for deletion, re-authentication for password change |
| D-15 | Support portal landing with search and category navigation | Frontend Page | Inline search results, 6 category cards |
| D-16 | Help article pages with feedback mechanism | Frontend Page | Yes/No feedback buttons, breadcrumb navigation |
| D-17 | Support ticket submission with file attachment | Full Stack | Authenticated, max 3 files, ticket ID generation |
| D-18 | Service status page with incident history | Frontend Page | Status indicators, auto-refresh every 60 seconds |
| D-19 | FAQ page with collapsible accordion | Frontend Page | Single-expand behaviour, smooth animation |
| D-20 | Global navigation bar with search autocomplete | Component | Sticky, backdrop blur, mobile hamburger menu, 3+ character autocomplete |
| D-21 | Footer with newsletter signup and social links | Component | 4-column grid desktop, single column mobile |
| D-22 | About page with studio history, team, locations, and careers | Frontend Page | Timeline component, team card grid, embedded map |
| D-23 | Downloads page with launcher links and wallpaper gallery | Frontend Page | Platform detection, masonry grid |
| D-24 | Search results page with tabbed content type filtering | Frontend Page | Tabs: All, Games, News, Videos, Support. Pagination per tab |
| D-25 | MongoDB database with all Mongoose models and seed data | Backend | User, Game, Article, Product, Order, Ticket, Newsletter models |
| D-26 | REST API endpoints for all data operations | Backend | Games, Articles, Products, Tickets, Search, Newsletter routes |
| D-27 | Responsive design passing all breakpoint requirements | Cross-cutting | Desktop, tablet, mobile, wide layouts all tested |
| D-28 | Dark theme with complete design token system | Cross-cutting | CSS custom properties, consistent colour, spacing, typography |
| D-29 | SEO implementation with structured data | Cross-cutting | Meta tags, JSON-LD, sitemap, robots.txt |
| D-30 | Accessibility compliance (WCAG 2.1 AA) | Cross-cutting | Keyboard nav, ARIA, contrast, skip nav, reduced motion |
| D-31 | Production build and deployment configuration | DevOps | next build passes, environment variable documentation, README |

---

## 16. File Formats

| Deliverable | Format |
|---|---|
| Source Code | GitHub repository or .zip archive |
| Documentation | .md (Markdown) |
| Design Assets | .png, .svg, .webp |
| Seed Data | .json |
| Environment Configuration | .env.example |
| Build Output | Next.js production build (`next build`) |

---

## 17. Explicit Ask

### What Must Be Built

A complete, multi-page online gaming website modelled after rockstargames.com. The website must include all 31 deliverables listed in Section 15 with no omissions. Every page, component, API endpoint, and system described in this document must be fully implemented and functional.

### Expected Behaviour

- All pages render correctly at all breakpoints (mobile, tablet, desktop, wide)
- Navigation between pages is seamless with no broken links
- The hero carousel auto-rotates and responds to manual navigation
- Game filtering and sorting updates results in real time without full page reloads
- Video modals open and close cleanly with keyboard support
- User registration sends a verification email and login establishes a persistent session
- The shopping cart persists across sessions and the checkout flow processes a test payment
- Support ticket submission saves to the database and returns a confirmation with ticket ID
- Global search returns relevant results across all content types with autocomplete
- All animations are smooth and respect the prefers-reduced-motion preference

### Acceptance Criteria

1. All 31 deliverables are present and functional
2. The website renders correctly at mobile (375px), tablet (768px), desktop (1200px), and wide (1920px) breakpoints
3. Lighthouse Performance score is 90 or above on all pages
4. WCAG 2.1 Level AA compliance passes on all pages
5. All forms validate inputs and display clear error messages
6. Authentication flow (register, verify, login, reset password) works end to end
7. Store checkout flow processes a Stripe test payment successfully
8. The database seeds correctly with all sample data
9. The production build (`next build`) completes without errors or warnings
10. All API endpoints return correct responses with appropriate status codes

### Performance Expectations

- Pages load within 2 seconds on a standard broadband connection
- No layout shift visible during page load
- Animations run at 60 frames per second
- API endpoints respond within 300 milliseconds

### Platform Requirements

- Browsers: Chrome 100+, Firefox 100+, Safari 16+, Edge 100+
- Devices: iPhone 12+ (iOS Safari), Samsung Galaxy S21+ (Chrome Android), iPad (Safari), Desktop (Chrome/Firefox/Edge)
- Screen Readers: VoiceOver (macOS/iOS), NVDA (Windows)

---

## Notes for the Development Team

All colour values, spacing values, typography settings, and animation durations defined in the Design System (Section 10) must be implemented as CSS Custom Properties in the globals.css file. No hard-coded colour or spacing values are permitted directly inside component styles. All database queries must use indexed fields for filterable and searchable content. All API responses must include proper HTTP status codes (200, 201, 400, 401, 404, 500) and JSON error messages. Environment variables must be documented in .env.example with placeholder values for all secrets. The README.md must include setup instructions, environment variable descriptions, database seeding commands, and available npm scripts.
