# NeverFullTime Web & Sanity CMS Integration

This document explains the connection between the NeverFullTime web application and Sanity CMS, including all available content types and their fields.

## Connection Overview

The NeverFullTime web application (`neverfulltime-web`) connects to Sanity CMS (`neverfulltime-sanity-crm`) to manage all content and data.

## Available Content Types in Sanity

### 1. Country
Manages country-specific data for internationalization.

**Fields:**
- `name` (string, required) - Country Name (max 100 chars)
- `slug` (slug, required) - URL-friendly identifier from name (max 96 chars)
- `code` (string, required) - ISO 3166-1 alpha-2 country code (2 chars, uppercase)

**Usage:** Powers country-based routing (e.g., `/ca`, `/au`, `/us`) and all canonical, lang hrefs, and sitemap data.

---

### 2. City
Manages cities within countries for location-based features.

**Fields:**
- `name` (string, required) - City Name (max 100 chars)
- `slug` (slug, required) - URL-friendly identifier from name (max 96 chars)
- `description` (text) - City description (max 500 chars)
- `images` (image array) - City photos with alt text
- `coordinates` (geopoint) - Latitude/longitude for maps
- `country` (reference, required) - Reference to Country document

**Usage:** City pages, location filtering, map displays

---

### 3. Venue
Manages sports venues and facilities within cities.

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

**Usage:** Venue listings, booking system, location services

---

### 4. Author
Manages blog post authors and their information.

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

**Usage:** Author pages, blog post attribution, author profiles

---

### 5. Blog
Manages blog posts with internationalization support.

**Fields:**
- `title` (string, required) - Blog title (max 100 chars)
- `slug` (slug, required) - URL-friendly identifier from title (max 96 chars)
- `excerpt` (text) - Blog summary (max 200 chars)
- `featuredImage` (image) - Main blog image with alt text
- `content` (array) - Rich content with sections:
  - Section objects with title, slug, and rich text body
  - Supports headings, lists, links, images
  - Table of contents generation
- `author` (reference, required) - Reference to Author document
- `publishedAt` (datetime, required) - Publication date and time
- `categories` (string array) - Content categories:
  - Sports, Gaming, Tournament, Community, News, Tips
  - Min 1, Max 3 categories required
- `tags` (string array) - Free-form tags for filtering
- `language` (string, required) - Content language:
  - Options: en, es, fr, de, it, pt, nl, ja, ko, zh-CN, zh-TW, ar, hi
  - Default: en (English)
- `countries` (reference array) - Target countries (max 20)
  - Empty = global content for all countries
- `status` (string) - Publication status:
  - Options: draft, published, archived
  - Default: draft
- `readTime` (number) - Estimated reading time in minutes (1-60)
- `relatedArticles` (reference array) - Related blog posts (max 5)
- `banner` (object) - Optional promotional banner:
  - `title` (string, required) - Banner title (max 100 chars)
  - `image` (image) - Banner image with alt text
  - `actionText` (string, required) - Call-to-action text (max 50 chars)
  - `actionLink` (url) - Optional link for banner action

**Usage:** Blog system, content marketing, SEO, internationalization

---

### 6. Testimonial
Manages user testimonials with type classification.

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

**Usage:** Social proof, user testimonials, homepage features

---

### 7. FAQ
Manages frequently asked questions with categorization.

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

**Usage:** Help documentation, support pages, user guidance

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