# NeverFullTime Routing & Pages Architecture

This document explains the page structure, routing system, and Sanity data usage across the NeverFullTime web application.

## Routing Structure Overview

The application uses **country-based routing** with two main levels:

```
/ (Global)
├── Home Page (/)
├── Blog Listing (/blog)
├── Blog Posts (/blog/[...slug])
├── Soccer Venues (/soccer-venues)
├── Feature Pricing (/feature-pricing)
├── Feature Play Soccer Games (/feature-play-soccer-games)
├── Feature How It Works (/feature-how-it-works)
└── Feature Host Soccer Games (/feature-host-soccer-games)

/[country] (Country-specific)
├── Country Home Page (/[country])
├── Country Blog Listing (/[country]/blog)
├── Country Blog Posts (/[country]/blog/[...slug])
├── Country Soccer Venues (/[country]/soccer-venues)
├── Country Feature Pricing (/[country]/feature-pricing)
├── Country Feature Play Soccer Games (/[country]/feature-play-soccer-games)
├── Country Feature How It Works (/[country]/feature-how-it-works)
├── Country Feature Host Soccer Games (/[country]/feature-host-soccer-games)
├── City Venues Listing (/[country]/[city]/venues)
└── Individual Venue Pages (/[country]/[city]/venues/[pitch])
```

**Examples of actual routes:**
```
Global:
├── /
├── /blog
├── /blog/how-to-host-a-pickup-soccer-game
├── /soccer-venues
├── /feature-pricing
├── /feature-play-soccer-games
├── /feature-how-it-works
└── /feature-host-soccer-games

Country-specific (Canada example):
├── /ca
├── /ca/blog
├── /ca/blog/how-to-host-a-pickup-soccer-game
├── /ca/soccer-venues
├── /ca/feature-pricing
├── /ca/feature-play-soccer-games
├── /ca/feature-how-it-works
├── /ca/feature-host-soccer-games
├── /ca/toronto/venues (City venues listing)
└── /ca/toronto/venues/cn-tower-sports-complex (Individual venue)

Location-based (Bosnia example from your URLs):
├── /ba/rio-de-janeiro/venues (City venues listing)
└── /ba/rio-de-janeiro/venues/ballsports-polson-pier (Individual venue)
```

## Global Pages (`/`)

### Homepage (`/index.js`)
**Route:** `/`
**Purpose:** Main landing page with global content
**Sanity Data Used:**
- Recent blog posts for stories section
- User testimonials for social proof  
- Featured FAQs for help section
- Countries and cities for navigation

**Components:**
- `GlobalSEO` - Generates hreflang for all countries (language: 'en')
- `RootMetaData` - Global meta tags
- `Landing` - Main content component

---

### Blog Listing (`/blog/index.jsx`)
**Route:** `/blog`
**Purpose:** Global blog listing page
**Sanity Data Used:**
- All published blog posts
- Related FAQs
- Countries/cities for navigation

---

### Individual Blog Posts (`/blog/[...slug].jsx`)
**Route:** `/blog/{slug}`
**Purpose:** Global blog post pages
**Sanity Data Used:**
- Specific blog post content
- Related articles
- Related FAQs
- Countries/cities data

**Components:**
- `SimpleSEO` - Blog-specific SEO with hreflang based on blog.countries and blog.language

---

### Feature Pages
**Routes & Data:**

#### `/feature-pricing.jsx`
**Sanity Data:** None (static content)
**Purpose:** Pricing information and plans

#### `/feature-play-soccer-games.jsx` 
**Sanity Data:** None (static content)
**Purpose:** Feature showcase for playing games

#### `/feature-how-it-works.js`
**Sanity Data:** None (static content) 
**Purpose:** Explanation of platform functionality

#### `/feature-host-soccer-games.js`
**Sanity Data:** None (static content)
**Purpose:** Feature showcase for hosting games

#### `/soccer-venues/index.jsx`
**Sanity Data:** None (static content)
**Purpose:** Information about venue features

---

## Country-Specific Pages (`/[country]`)

### Country Homepage (`/[country]/index.js`)
**Route:** `/{country}`
**Purpose:** Country-specific landing page
**Sanity Data Used:**
- Recent blogs for stories
- User testimonials  
- FAQs for help section
- Country validation and data fetching

**Components:**
- `GlobalSEO` - Country-specific SEO with customized title/description
- `InvalidCountrySelector` - Fallback for invalid countries

---

### Country Blog Listing (`/[country]/blog/index.jsx`)
**Route:** `/{country}/blog`
**Purpose:** Country-specific blog listing
**Sanity Data Used:**
- All published blogs
- Related FAQs
- Country validation

---

### Country Blog Posts (`/[country]/blog/[...slug].jsx`)
**Route:** `/{country}/blog/{slug}`
**Purpose:** Country-specific blog post pages
**Sanity Data Used:**
- Specific blog content
- Related articles
- Related FAQs
- Country validation

**Components:**
- `SimpleSEO` - Generates hreflang based on blog countries/language with proper country URL structure

---

### Country Feature Pages
All feature pages are replicated under `/{country}/`:

#### `/{country}/feature-pricing.jsx`
#### `/{country}/feature-play-soccer-games.jsx` 
#### `/{country}/feature-how-it-works.js`
#### `/{country}/feature-host-soccer-games.js`
#### `/{country}/soccer-venues/index.jsx`

**Sanity Data:** Same as global versions (static content)
**Purpose:** Localized versions of feature pages

---

## Location-Based Pages (`/[country]/[city]`)

### City Venues Listing (`/[country]/[city]/venues/index.jsx`)
**Route:** `/{country}/{city}/venues`
**Purpose:** List all venues in a specific city
**Sanity Data Used:**
- All active venues in the city
- City information and details
- Country validation

**Examples:**
- `/ca/toronto/venues` - All venues in Toronto, Canada
- `/ba/rio-de-janeiro/venues` - All venues in Rio de Janeiro, Bosnia

---

### Individual Venue Pages (`/[country]/[city]/venues/[pitch].jsx`)
**Route:** `/{country}/{city}/venues/{venue-slug}`
**Purpose:** Detailed information about a specific venue
**Sanity Data Used:**
- Specific venue details
- Related venues in the city
- Country validation

**Examples:**
- `/ca/toronto/venues/cn-tower-sports-complex` - Specific venue in Toronto
- `/ba/rio-de-janeiro/venues/ballsports-polson-pier` - Specific venue in Rio de Janeiro

**Venue Data Structure:**
- Venue name, description, images
- Location coordinates (geopoint)
- General information and facilities
- Status (active/inactive/maintenance)
- City and country relationships

---

## Static Generation Strategy

### getStaticPaths
**Country Routes:**
```javascript
// Uses getCountryStaticPaths() to generate paths for all countries
paths: ['/ca', '/au', '/us', '/uk', '/nz', ...]
```

**Blog Routes:**
```javascript
// Combines countries with blog slugs
paths: [
  '/ca/blog/soccer-tips',
  '/au/blog/soccer-tips', 
  '/us/blog/soccer-tips',
  ...
]
```

### getStaticProps
**Data Fetching Pattern:**
```javascript
const [blogs, testimonials, faqs, locationData] = await Promise.all([
  BlogAPI.getRecentBlogs(3),
  TestimonialAPI.getTestimonials(5), 
  FaqAPI.getFaqs(6),
  CityAPI.getAllData()
]);
```

---

## SEO & Internationalization

### Global Pages
- **Canonical:** `https://neverft.com{path}`
- **Hreflang:** Generated for all countries
- **Language:** Always 'en'

### Country Pages  
- **Canonical:** `https://neverft.com/{country}{path}`
- **Hreflang:** Based on blog.countries or fallback to all countries
- **Language:** From blog.language or default 'en'

### Blog Posts
- **Dynamic hreflang:** Uses blog's countries array and language field
- **Country targeting:** Blog can target specific countries or be global
- **URL structure:** Always `/{country}/blog/{slug}` for SEO consistency

---

## Data Flow Summary

### Homepage Flow
```
User visits / or /{country}
↓
getStaticProps fetches: blogs, testimonials, faqs, countries
↓  
GlobalSEO generates hreflang for all countries
↓
Landing component renders with fetched data
```

### Blog Post Flow
```
User visits /{country}/blog/{slug}
↓
validateCountryAndGetData() validates country
↓
BlogAPI.getBlogBySlug() fetches post content
↓
SimpleSEO generates hreflang based on post.countries & post.language
↓
BlogSingle component renders with post data
```

### Static Generation Flow
```
Build time
↓
getCountryStaticPaths() fetches countries from Sanity
↓
BlogAPI.getBlogPaths() fetches blog slugs from Sanity
↓
Generates all possible /{country}/{page} combinations
↓
Each page fetches required Sanity data during build
```

---

## Excluded Pages (Not in Sitemap)

The application has many additional pages for authenticated users that are excluded from public sitemaps:

- `/dashboard` - User dashboard
- `/profile/*` - User profile pages  
- `/community/*` - Community features
- `/match/*` - Game matching system
- `/tournament/*` - Tournament system
- `/teams/*` - Team management
- `/host/*` - Host-specific features
- And many more...

These pages use various Sanity data but are part of the authenticated application experience, not the public marketing site.

## Key Routing Principles

1. **Country-first approach:** Most content is country-specific
2. **SEO optimization:** Proper hreflang and canonical URLs
3. **Static generation:** All public pages are statically generated
4. **Data consistency:** Same data structure across global and country pages
5. **Fallback handling:** Invalid countries redirect to country selector