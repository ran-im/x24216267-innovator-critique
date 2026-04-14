# Prototype & Design Specifications

## Product Name: SilkAI
## Version: Alpha Prototype (MVP Scope)

---

## Brand Guidelines

### Color Palette
| Token | Hex | Usage |
|---|---|---|
| `--dark` | `#0A0E1A` | Primary background |
| `--darker` | `#060912` | Deep background, footer |
| `--gold` | `#C9A84C` | Primary accent, CTAs, highlights |
| `--gold-bright` | `#E5C55A` | Hover states |
| `--cream` | `#F5EDD6` | Primary text on dark |
| `--text-muted` | `#9A8B6E` | Secondary text |
| `--burgundy` | `#8B1C1C` | Error states, warnings |
| `--green` | `#4CAF50` | Success states, positive price movement |

### Typography
| Role | Font | Weight | Size |
|---|---|---|---|
| Display / H1 | Cormorant Garamond | 700 | clamp(2.8rem, 6vw, 5.5rem) |
| Section Heading / H2 | Cormorant Garamond | 600 | clamp(2rem, 4vw, 3.5rem) |
| Card Heading / H3 | Cormorant Garamond | 600 | clamp(1.3rem, 2.5vw, 1.9rem) |
| Body Text | DM Sans | 400 | clamp(0.95rem, 1.5vw, 1.1rem) |
| Labels / Caps | DM Sans | 500 | 0.78–0.85rem, letter-spacing 0.08–0.12em |
| Buttons | DM Sans | 500 | 0.9rem |

### Logo
Simple wordmark: "Silk" (cream) + "AI" (gold). Icon: Stylised "S" letterform inside a rounded rectangle, gold on dark. Used as favicon.

---

## Architecture Overview

```
SilkAI Platform
├── Mobile App (React Native)
│   ├── Onboarding (language selection → farm profile)
│   ├── My Listings (create, manage crop listings)
│   ├── Matches (AI-suggested buyers with profiles)
│   ├── Messages (translated buyer-seller chat)
│   ├── Documents (generate, sign, download)
│   ├── Prices (real-time commodity dashboard)
│   └── Profile & Settings
├── Web Dashboard (React PWA)
│   ├── All mobile features +
│   ├── Cooperative management panel
│   ├── Analytics & reporting
│   └── API settings
└── Backend Services
    ├── Auth Service (JWT, OAuth2)
    ├── Listing Service (CRUD, AI enrichment)
    ├── Matching Engine (ML model)
    ├── Price Feed Service (external APIs)
    ├── Document Service (template + AI generation)
    ├── Translation Service (LLM-powered)
    ├── Notification Service (SMS, push, email)
    └── Escrow Service (payment rails integration)
```

---

## Core User Flows

### Flow 1: Producer Lists a Harvest
1. Open app → "New Listing"
2. Select crop type from visual picker (icons, no text required)
3. Enter or voice-input: quantity (kg), quality grade, harvest date, price expectation
4. AI enriches listing: suggests international grade equivalent, adds market context
5. Review and publish → listing goes live to buyer network
6. Receive match notifications within 24 hours

### Flow 2: Producer Receives a Match
1. Push notification: "3 buyers matched your sesame listing"
2. Open Matches tab → see buyer cards (name, country, trade volume, rating, offer price)
3. Tap buyer card → view full profile + comparable trades
4. "Respond" → AI-translated message composer opens
5. Negotiate terms in Turkmen; AI translates to buyer's language in real time
6. Agree terms → "Generate Contract" button appears

### Flow 3: Document Generation
1. After agreeing terms → tap "Generate Contract"
2. AI generates: export contract, certificate of origin, phytosanitary certificate
3. Preview documents in platform
4. E-sign via OTP verification
5. Buyer countersigns → documents locked
6. Escrow payment initiated by buyer
7. Producer receives shipment notification and payment release upon delivery confirmation

---

## Screen Specifications (Key Screens)

### Screen 1: Home Dashboard
- **Top bar:** Farm name, notification bell, language flag selector
- **Hero card:** "Your market today" — current gold price for user's primary crop + % vs yesterday
- **Active listings:** 2-3 card scroll (crop, quantity, days active, matches count)
- **Market alert banner:** Animated gold bar — "Peanut prices up 8% in Hamburg this week"
- **Quick actions:** New Listing / My Matches / Documents

### Screen 2: Match Card
- **Header:** Buyer company name + verified badge + country flag
- **Offer details:** Price per kg / Payment terms / Delivery window
- **Buyer profile:** Trade volume, years active, rating (out of 5), past crops purchased
- **Actions:** "I'm Interested" / "Decline" / "View Profile"
- **Language note:** "This conversation will be in Turkmen"

### Screen 3: Price Intelligence
- **Hero number:** Current international spot price for selected crop (large, gold)
- **Comparison:** vs local market price (smaller, muted) — delta in green/red
- **7-day chart:** CSS sparkline
- **Exchange selector:** Tabs for CME / Euronext / China / Regional
- **Alert setting:** "Notify me when price exceeds X"

### Screen 4: Document Generator
- **Step indicator:** 1. Details → 2. Review → 3. Sign → 4. Complete
- **Auto-filled fields:** From agreed trade terms (read-only preview)
- **Editable fields:** Highlighted in gold border
- **Legal note:** AI-generated disclaimer at bottom
- **Export buttons:** Download PDF / Share via WhatsApp / Email

---

## MVP Development Timeline

| Phase | Duration | Deliverables |
|---|---|---|
| **Phase 0: Foundation** | Weeks 1–4 | Auth, farm profiles, basic listing CRUD, Turkmen/Russian/English UI |
| **Phase 1: Core Loop** | Weeks 5–10 | Buyer database (200 verified), matching engine v1, in-app messaging + AI translation |
| **Phase 2: Intelligence** | Weeks 11–16 | Price feed integration (3 exchanges), price alert system, document generator v1 (3 doc types) |
| **Phase 3: Trust & Scale** | Weeks 17–22 | Escrow integration, cooperative dashboard, extended language support (Kazakh, Uzbek), iOS + Android launch |
| **Beta Launch** | Week 23 | 500 producer onboarding campaign, 3 cooperative partnerships active |

---

## Design Principles

1. **Icon-first, text-optional** — producers with low literacy must complete core flows using visuals alone
2. **Offline-first** — all listings and matches cached locally; sync when connectivity resumes
3. **Speed over features** — core loop (list → match → respond) must complete in under 3 minutes
4. **Trust signals everywhere** — verified badges, ratings, trade history visible at every decision point
5. **One action per screen** — no cognitive overload; every screen has one primary action

---

## Technical Stack

| Layer | Technology | Rationale |
|---|---|---|
| Mobile | React Native + Expo | Cross-platform, large talent pool in target region |
| Web | Next.js 15 (App Router) | SSR for SEO, PWA support |
| API | Node.js + Express, GraphQL | Flexible, widely known |
| Database | PostgreSQL (primary), Redis (cache) | Reliability, ACID compliance for trade records |
| AI/ML | Claude API (document gen + translation), custom scikit-learn model (matching) | Cost-effective, multilingual excellence |
| Infrastructure | AWS (Frankfurt) | EU data residency, GDPR compliance |
| Payments | Stripe Connect + regional SWIFT integration | International + local payment support |
| Notifications | AWS SNS + Twilio (SMS fallback) | Reach low-data users via SMS |
