# Content Management System

This document explains how NeverFullTime manages content across all countries and markets using our headless CMS platform.

## Content Management Overview

NeverFullTime uses **[Sanity CMS](https://neverft.sanity.studio/){:target="_blank"}** as our headless content management system to deliver consistent, scalable content across all global markets.

This allows our content team to manage everything from a single dashboard while serving localized experiences worldwide.

## Available Content Types

### 1. Country
Manages country-specific data for internationalization.

**Purpose:** Powers country-based routing and localization

**Fields:**

- `name` (string, required) - Country Name (max 100 chars)

- `slug` (slug, required) - URL-friendly identifier from name (max 96 chars)

- `code` (string, required) - ISO 3166-1 alpha-2 country code (2 chars, uppercase)

**Usage Examples:**
- `/ca` for Canada
- `/au` for Australia  
- `/us` for United States

---

### 2. City
Manages cities within countries for location-based features.

**Purpose:** Local presence and venue organization

**Fields:**

- `name` (string, required) - City Name (max 100 chars)

- `slug` (slug, required) - URL-friendly identifier from name (max 96 chars)

- `description` (text) - City description (max 500 chars)

- `images` (image array) - City photos with alt text

- `coordinates` (geopoint) - Latitude/longitude for maps

- `country` (reference, required) - Reference to Country document

**Usage Examples:**
- City pages and venue filtering
- Map displays and location services
- Regional sports community building

---

### 3. Venue
Manages sports venues and facilities within cities.

**Purpose:** Sports facility listings and bookings

**Fields:**

- `name` (string, required) - Venue Name (max 100 chars)

- `slug` (slug, required) - URL-friendly identifier from name (max 96 chars)

- `locationId` (string) - External location identifier

- `description` (text) - Venue description (max 1000 chars)

- `images` (image array) - Venue photos with alt text

- `location` (geopoint) - Exact venue coordinates

- `generalInformation` (text) - Additional venue details

- `status` (string) - Options: active, inactive, maintenance (default: active)

- `city` (reference, required) - Reference to City document

**Usage Examples:**
- Venue directory and search
- Booking system integration
- Location-based recommendations

---

### 4. Author
Manages blog post authors and their information.

**Purpose:** Content credibility and author profiles

**Fields:**

- `name` (string, required) - Author Name (max 100 chars)

- `slug` (slug, required) - URL-friendly identifier from name (max 96 chars)

- `image` (image) - Author profile photo with alt text

- `location` (string) - Author's location (max 100 chars)

- `bio` (text) - Author biography (max 500 chars)

- `socialLinks` (object) - Social media links:
  - `twitter` (url) - Twitter profile
  - `linkedin` (url) - LinkedIn profile
  - `website` (url) - Personal website

**Usage Examples:**
- Author attribution on blog posts
- Author profile pages
- Content credibility and expertise

---

### 5. Blog
Manages blog posts with internationalization support.

**Purpose:** Content marketing and SEO across all countries

**Core Fields:**

- `title` (string, required) - Blog title (max 100 chars)

- `slug` (slug, required) - URL-friendly identifier from title (max 96 chars)

- `excerpt` (text) - Blog summary (max 200 chars)

- `featuredImage` (image) - Main blog image with alt text

- `author` (reference, required) - Reference to Author document

- `publishedAt` (datetime, required) - Publication date and time

**Content & Structure:**

- `content` (array) - Rich content with sections:
  - Section objects with title, slug, and rich text body
  - Supports headings, lists, links, images
  - Table of contents generation

- `categories` (string array) - Content categories (min 1, max 3):
  - Sports, Gaming, Tournament, Community, News, Tips

- `tags` (string array) - Free-form tags for filtering

**Internationalization:**

- `language` (string, required) - Content language:
  - Options: en, es, fr, de, it, pt, nl, ja, ko, zh-CN, zh-TW, ar, hi
  - Default: en (English)

- `countries` (reference array) - Target countries (max 20)
  - Empty = global content for all countries

**Publishing & Features:**

- `status` (string) - Publication status:
  - Options: draft, published, archived
  - Default: draft

- `readTime` (number) - Estimated reading time (1-60 minutes)

- `relatedArticles` (reference array) - Related blog posts (max 5)

- `banner` (object) - Optional promotional banner:
  - `title` (string, required) - Banner title (max 100 chars)
  - `image` (image) - Banner image with alt text
  - `actionText` (string, required) - Call-to-action text (max 50 chars)
  - `actionLink` (url) - Optional link for banner action

**Usage Examples:**
- Country-specific sports content
- Global blog posts with multiple language versions
- SEO-optimized articles with proper hreflang targeting

---

### 6. Testimonial
Manages user testimonials with type classification.

**Purpose:** Social proof and user reviews

**Fields:**

- `userName` (string, required) - User's name (max 100 chars)

- `userRole` (string, required) - User's role/team (max 100 chars)

- `tag` (string, required) - User type:
  - Options: host, player
  - Radio button selection

- `description` (text, required) - Testimonial content (10-500 chars)

- `userProfile` (image) - User profile photo with alt text

- `status` (string) - Visibility status:
  - Options: published, draft
  - Default: draft

- `order` (number) - Display order (integer, min 0, default 0)

**Usage Examples:**
- Homepage social proof
- Host and player testimonials
- Community building and trust

---

### 7. FAQ
Manages frequently asked questions with categorization.

**Purpose:** Customer support and user guidance

**Fields:**

- `question` (string, required) - FAQ question (max 200 chars)

- `answer` (text, required) - FAQ answer (max 1000 chars)

- `category` (string) - Question category:
  - Options: general, hosting, playing, venues, payments, technical
  - Default: general

- `status` (string) - Visibility status:
  - Options: published, draft
  - Default: draft

- `order` (number) - Display order (integer, min 0, default 0)

- `featured` (boolean) - Mark as featured FAQ

**Usage Examples:**
- Help documentation
- Support pages and user onboarding
- Reducing customer service inquiries

---

## Data Relationships

### Hierarchical Structure
```
Country (1) → Cities (many) → Venues (many)
```

### Content Relationships
```
Author (1) → Blog Posts (many)
Country (many) ← Blog Posts (many) [targeting]
Blog Post (1) → Related Articles (many)
```

### Reference Fields
- **City.country** → Country document
- **Venue.city** → City document  
- **Blog.author** → Author document
- **Blog.countries** → Country documents (array)
- **Blog.relatedArticles** → Blog documents (array)

## Content Workflow

1. **Create** content in Sanity Studio
2. **Publish** content (status: published)
3. **Revalidate Pages** triggers static regeneration
4. **Display** on website with proper SEO and internationalization

This integration enables a headless CMS approach with full content management capabilities while maintaining fast, static site performance.