# Website Architecture & Page Structure

This document explains how NeverFullTime's website is organized across different countries and what content powers each page.

## Website Structure Overview

NeverFullTime uses **country-based website architecture** to serve localized experiences globally:

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

**Live Examples:**

**Global Pages** - [View Global Site](https://staging1.neverft.com/){:target="_blank"}

- [Homepage](https://staging1.neverft.com/){:target="_blank"}
- [Blog](https://staging1.neverft.com/blog){:target="_blank"}  
- [Feature Pages](https://staging1.neverft.com/feature-pricing){:target="_blank"}
- [Soccer Venues](https://staging1.neverft.com/soccer-venues){:target="_blank"}

**Country-Specific Pages** - [View Canada Site](https://staging1.neverft.com/ca){:target="_blank"}

- [Canada Homepage](https://staging1.neverft.com/ca){:target="_blank"}
- [Canada Blog](https://staging1.neverft.com/ca/blog){:target="_blank"}
- [Canada Features](https://staging1.neverft.com/ca/feature-pricing){:target="_blank"}
- [Canada Venues](https://staging1.neverft.com/ca/soccer-venues){:target="_blank"}

**City & Venue Pages** - [View City Example](https://staging1.neverft.com/ca/toronto/venues){:target="_blank"}

- [City Venues Listing](https://staging1.neverft.com/ca/toronto/venues){:target="_blank"}
- [Individual Venue](https://staging1.neverft.com/ba/rio-de-janeiro/venues/ballsports-polson-pier){:target="_blank"}

---

## Page Details

### Global Pages (`/`)

#### Homepage (`/`)
**Purpose:** Main landing page showcasing the platform

**Live Example:** [https://staging1.neverft.com/](https://staging1.neverft.com/){:target="_blank"}

**Content Sources:**
- Recent blog posts for stories section
- User testimonials for social proof  
- Featured FAQs for help section
- Countries and cities for navigation

---

#### Blog Listing (`/blog`)
**Purpose:** Global blog content and resources

**Live Example:** [https://staging1.neverft.com/blog](https://staging1.neverft.com/blog){:target="_blank"}

**Content Sources:**
- All published blog posts
- Related FAQs
- Countries/cities for navigation

---

#### Individual Blog Posts (`/blog/{slug}`)
**Purpose:** Detailed sports content and guides

**Live Example:** [https://staging1.neverft.com/blog/how-to-host-a-pickup-soccer-game](https://staging1.neverft.com/blog/how-to-host-a-pickup-soccer-game){:target="_blank"}

**Content Sources:**
- Complete blog post content with rich media
- Related articles for engagement
- Author information and credibility
- SEO optimization for global reach

---

#### Feature Pages
**Purpose:** Platform features and pricing information

**Live Examples:**
- [Feature Pricing](https://staging1.neverft.com/feature-pricing){:target="_blank"}
- [Play Soccer Games](https://staging1.neverft.com/feature-play-soccer-games){:target="_blank"}
- [How It Works](https://staging1.neverft.com/feature-how-it-works){:target="_blank"}
- [Host Soccer Games](https://staging1.neverft.com/feature-host-soccer-games){:target="_blank"}

**Content Sources:**
- Static content managed in code
- Optimized for conversion and user education

---

#### Soccer Venues (`/soccer-venues`)
**Purpose:** Platform venue information and features

**Live Example:** [https://staging1.neverft.com/soccer-venues](https://staging1.neverft.com/soccer-venues){:target="_blank"}

**Content Sources:**
- Static venue feature information
- Platform capabilities showcase

---

## Country-Specific Pages (`/[country]`)

### Country Homepage (`/{country}`)

#### Country Homepage (`/{country}`)
**Purpose:** Localized landing page for each country

**Live Example:** [https://staging1.neverft.com/ca](https://staging1.neverft.com/ca){:target="_blank"} (Canada)

**Content Sources:**
- Same content as global homepage
- Country-specific customization
- Localized testimonials and FAQs
- Regional sports focus

---

#### Country Blog Listing (`/{country}/blog`)
**Purpose:** Country-specific blog content and resources

**Live Example:** [https://staging1.neverft.com/ca/blog](https://staging1.neverft.com/ca/blog){:target="_blank"} (Canada Blog)

**Content Sources:**
- Blog posts targeted to specific countries
- Global blog posts available everywhere
- Country-specific sports content

---

#### Country Blog Posts (`/{country}/blog/{slug}`)
**Purpose:** Localized blog content and guides

**Live Example:** [https://staging1.neverft.com/ca/blog/how-to-host-a-pickup-soccer-game](https://staging1.neverft.com/ca/blog/how-to-host-a-pickup-soccer-game){:target="_blank"} (Canada Blog Post)

**Content Sources:**
- Complete blog post with country targeting
- Related articles from same country/language
- SEO optimization with country-specific hreflang

---

#### Country Feature Pages
**Purpose:** Localized feature information and pricing

**Live Examples:**
- [Canada Pricing](https://staging1.neverft.com/ca/feature-pricing){:target="_blank"}
- [Canada Play Games](https://staging1.neverft.com/ca/feature-play-soccer-games){:target="_blank"}
- [Canada How It Works](https://staging1.neverft.com/ca/feature-how-it-works){:target="_blank"}
- [Canada Host Games](https://staging1.neverft.com/ca/feature-host-soccer-games){:target="_blank"}
- [Canada Soccer Venues](https://staging1.neverft.com/ca/soccer-venues){:target="_blank"}

**Content Sources:**
- Same static content as global pages
- Country-specific customization possible
- Localized pricing and features

---

## Location-Based Pages (`/{country}/{city}`)

#### City Venues Listing (`/{country}/{city}/venues`)
**Purpose:** List all sports venues in a specific city

**Live Example:** [https://staging1.neverft.com/ca/toronto/venues](https://staging1.neverft.com/ca/toronto/venues){:target="_blank"} (Toronto Venues)

**Content Sources:**
- All active venues in the city
- City information and details
- Venue photos and descriptions

---

#### Individual Venue Pages (`/{country}/{city}/venues/{venue-slug}`)
**Purpose:** Detailed information about specific sports facilities

**Live Example:** [https://staging1.neverft.com/ba/rio-de-janeiro/venues/ballsports-polson-pier](https://staging1.neverft.com/ba/rio-de-janeiro/venues/ballsports-polson-pier){:target="_blank"} (Specific Venue)

**Content Sources:**
- Complete venue information and photos
- Location coordinates and maps
- Facility details and amenities
- Related venues in the same city

## Platform Scale & Implementation

### Technical Architecture

**Static Site Generation**
- All pages are pre-built at deployment time for maximum performance
- Content is fetched from Sanity CMS during the build process
- Fast global delivery via CDN

**SEO Optimization**
- Proper hreflang implementation for international targeting
- Country-specific canonical URLs
- Automatic sitemap generation with all page variations

**Content Management**
- Centralized content control via [Sanity CMS](https://neverft.sanity.studio/){:target="_blank"}
- Real-time content updates and publishing
- Multi-language and multi-country targeting

### Platform Scale

**Total Page Count**
- **Global pages:** 7 core pages
- **Country pages:** 7 pages × 10+ countries = 70+ pages  
- **City venue pages:** Dynamic based on cities in database
- **Individual venues:** Dynamic based on venue listings
- **Blog posts:** Dynamic based on published content

**Content Types**
- **Static content:** Feature pages, homepage sections
- **Dynamic content:** Blogs, testimonials, FAQs, venues
- **Location data:** Countries, cities, venue information
- **User content:** Testimonials, author profiles

This architecture enables NeverFullTime to scale globally while maintaining consistent user experiences across all markets.

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