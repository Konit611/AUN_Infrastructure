# Design System — AUN

## Product Context
- **What this is:** Sake personality quiz that matches young Japanese drinkers to their ideal nihonshu
- **Who it's for:** Young Japanese adults (20s) new to sake, mobile-first, active on LINE/Twitter
- **Space/industry:** Alcoholic beverage discovery, personality testing
- **Project type:** Web app (quiz flow + result sharing + personal journal)

## Aesthetic Direction
- **Direction:** Luxury/Refined meets Organic/Natural
- **Decoration level:** Intentional. Subtle washi paper texture on backgrounds. No gradients, no blobs, no decorative elements that don't reference sake culture.
- **Mood:** A modern izakaya with beautiful ceramics. Warm, confident, culturally rooted but not old-fashioned. The design should feel like sake culture translated for people who grew up on Instagram, not a traditional sake label copied onto a screen.
- **Reference sites:** Dassai (restraint, whitespace), Sakenomy (warmth, cultural patterns), 16Personalities (color-coded types, shareable results)

## Typography
- **Display/Hero:** Shippori Mincho 700 — connects to sake label typography, feels premium and culturally authentic for persona names and headings
- **Body:** Zen Maru Gothic 400/500 — rounded, friendly, warm. Approachable for young users without being childish
- **UI/Labels:** Zen Maru Gothic 500
- **Data/Tables:** Zen Maru Gothic (tabular-nums not available, use monospace for numbers)
- **Code:** JetBrains Mono (dev only)
- **Loading:** Google Fonts CDN
  ```html
  <link href="https://fonts.googleapis.com/css2?family=Shippori+Mincho:wght@400;600;700&family=Zen+Maru+Gothic:wght@300;400;500;700&display=swap" rel="stylesheet">
  ```
- **Scale:**
  - xs: 11px — tags, labels
  - sm: 13px — captions, secondary info
  - base: 16px — body text
  - lg: 18px — subtitle, lead text
  - xl: 22px — section titles (Shippori Mincho)
  - 2xl: 28px — page headings (Shippori Mincho)
  - 3xl: 42px — persona names (Shippori Mincho)
  - 4xl: 56px — hero/brand (Shippori Mincho)

## Color
- **Approach:** Restrained. Color is rare and meaningful. The accent is deep indigo, referencing traditional Japanese aizome (indigo dyeing) rather than the gold that every sake brand uses.
- **Background:** #FAF7F2 (warm cream)
- **Surface:** #FFFFFF (cards, inputs)
- **Surface raised:** #F5F0E8 (subtle distinction)
- **Text primary:** #1A1A1A (charcoal, not pure black)
- **Text secondary:** #5C5C5C
- **Text muted:** #8A8A8A
- **Accent:** #2B3A67 (deep indigo, aizome-inspired)
- **Accent hover:** #1E2A4A
- **Accent light:** #E8ECF4 (for hover backgrounds, tags)
- **Border:** #E5DDD3 (warm gray)
- **Semantic:**
  - Success: #2D6A4F
  - Warning: #B8860B
  - Error: #8B2500
  - Info: #2B3A67 (same as accent)
- **Dark mode strategy:** Invert surfaces (#121212 bg, #1E1E1E surface), reduce accent saturation to #7B8FC4, keep warm tone in raised surfaces (#2A2A2A)

### Persona Axis Colors
Each of the 4 taste axes has two colors. The combination creates 16 unique visual treatments for persona cards.

| Axis | First letter | Color | Second letter | Color |
|------|-------------|-------|---------------|-------|
| S/D | Sweet | #C2685A (terracotta) | Dry | #5A7FA0 (steel blue) |
| H/E | Heavy | #8B6F47 (warm brown) | Easy | #A8B89F (sage green) |
| R/L | Rich | #7B5EA7 (plum) | Light | #D4C5A9 (sand) |
| B/S | Bold | #3D3D3D (near-black) | Smooth | #B8B0A8 (warm gray) |

Persona cards use a gradient from the first axis color to the third axis color (e.g., SHRB = Sweet #C2685A to Rich #7B5EA7). Text on persona cards is always white.

## Spacing
- **Base unit:** 8px
- **Density:** Comfortable. Generous whitespace like premium sake brands.
- **Scale:**
  - 2xs: 2px
  - xs: 4px
  - sm: 8px
  - md: 16px
  - lg: 24px
  - xl: 32px
  - 2xl: 48px
  - 3xl: 64px
  - 4xl: 120px (hero padding)

## Layout
- **Approach:** Hybrid. Grid-disciplined for app screens (journal, results). Creative full-screen cards for the quiz flow.
- **Grid:** Single column on mobile (< 640px). 2 columns on tablet (640-1024px). Max 3 columns on desktop for card grids.
- **Max content width:** 960px
- **Border radius:**
  - sm: 4px (tags, small elements)
  - md: 8px (inputs, alerts)
  - lg: 12px (cards, modals)
  - full: 9999px (buttons, pills)

## Motion
- **Approach:** Intentional. Motion adds meaning, not decoration. No bouncy/playful animations.
- **Easing:** enter(ease-out) exit(ease-in) move(ease-in-out)
- **Duration:** micro(50-100ms) short(150-250ms) medium(250-400ms) long(400-700ms)
- **Key animations:**
  - Quiz: slide transition between questions (250ms, ease-in-out)
  - Result reveal: persona name fade-in (400ms) then code appear (200ms delay) then description slide-up (300ms)
  - Hover: border-color transition (200ms)
  - Page transitions: crossfade (200ms)

## Component Patterns
- **Buttons:** pill-shaped (border-radius: full). Primary = filled indigo. Secondary = outlined indigo. Ghost = outlined gray.
- **Cards:** white surface, warm gray border (#E5DDD3), 12px radius. Hover: border turns accent color.
- **Inputs:** white surface, warm gray border, 8px radius. Focus: border turns accent.
- **Tags/badges:** small pills with accent-light background and accent text. Used for serving temperature and seasonal indicators.
- **Alerts:** full-width, 8px radius, semantic color backgrounds with matching text.

## Shareable Card
- **Dimensions:** 1200x630 (landscape, optimized for LINE and Twitter/X)
- **Layout:** Persona code (top, monospace, small), persona name (center, Shippori Mincho 700), one-line description (below name). Background is the axis gradient.
- **Brand:** "AUN" text in bottom-right corner, small.

## Quiz UX
- **Layout:** Full-screen, one question at a time, mobile-first
- **Progress:** Thin 3px bar at top, accent color fill
- **Question text:** Shippori Mincho, 22px, centered
- **Choices:** Two full-width buttons, stacked vertically, 20px padding, large tap targets (min 48px)
- **Navigation:** Tap choice to advance. Swipe left to go back. No explicit next/back buttons.

## Decisions Log
| Date | Decision | Rationale |
|------|----------|-----------|
| 2026-03-28 | Initial design system created | Created by /design-consultation based on sake brand research + personality quiz design patterns |
| 2026-03-28 | Shippori Mincho + Zen Maru Gothic | Mincho connects to sake label typography (premium). Maru Gothic is friendly for young users (approachable). Two fonts, two moods. |
| 2026-03-28 | Deep indigo (#2B3A67) over gold | Every sake brand uses gold. Indigo references aizome (traditional dyeing) but feels modern. Differentiates AUN. |
| 2026-03-28 | Cream background (#FAF7F2) | Warm, not clinical. Standard for premium sake brands (Dassai, Hakkaisan). |
| 2026-03-28 | Axis-based persona color system | 4 axes x 2 colors = 16 unique gradients. Systematic, maintainable, no illustration dependency. |
