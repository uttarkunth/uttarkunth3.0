# Uttarkunth Stays 3.0

> **Learn by Doing • Grow by Serving**  
> Complete full-stack Himalayan accommodation platform, built for Cloudflare deployment with Next.js App Router, Tailwind CSS, TypeScript, and Supabase PostgreSQL.

---

## 1. Project Overview

**Uttarkunth Stays 3.0** is an authentic Himalayan accommodation marketplace connecting conscious travelers with independent homestays, retreats, and cottages across Himachal Pradesh, India.

- **Origin & Focus:** Jari, Kasol, Kullu, Parvati Valley, Himachal Pradesh
- **Founder:** Gaurav Negi
- **Design Language:** Forest green (`#13612E`), Brand Orange (`#C85A20`), Warm Ivory (`#FAF7F0`), Cormorant Garamond (Editorial Serif), and Poppins (UI Sans).
- **Core Booking Principle:** Host Approval Required (Request-to-Book workflow; no automated overbooking).
- **Host Commission Policy:** 0% introductory commission for the first 12 months under signed host agreements; 10% standard thereafter.

---

## 2. Technical Stack

- **Framework:** Next.js (App Router, Server Components, Route Handlers)
- **Deployment Platform:** Cloudflare Workers (via OpenNext adapter `@opennextjs/cloudflare`)
- **Database & Auth:** Supabase PostgreSQL, Supabase Auth (`@supabase/ssr`), and Storage
- **Validation:** Zod schemas
- **Styling & UI:** Tailwind CSS, Lucide React icons, Shadcn UI architectural patterns
- **Type Safety:** Strict TypeScript with types generated from live Supabase schema

---

## 3. Directory Structure

```text
uttarkunth3.0/
├── app/
│   ├── layout.tsx                     # Root HTML layout with Header, Footer, SEO
│   ├── globals.css                    # Tailwind directives & design tokens
│   ├── page.tsx                       # Homepage (Hero, Search, Featured Stays, Heritage)
│   ├── about/page.tsx                 # Brand story, philosophy & founder message
│   ├── contact/page.tsx               # Direct support channels & local concierge
│   ├── login/page.tsx                 # Supabase authentication login
│   ├── signup/page.tsx                # Guest & Host registration
│   ├── forgot-password/page.tsx       # Password recovery
│   ├── properties/
│   │   ├── page.tsx                   # Accommodation search & discovery with multi-filters
│   │   └── [slug]/page.tsx            # Property detail, room units & Request-to-Book panel
│   ├── guest/
│   │   ├── trips/page.tsx             # Guest upcoming and past trips ledger
│   │   ├── trips/[id]/page.tsx        # Individual booking detail & cancellation
│   │   └── profile/page.tsx           # Guest account profile
│   ├── host/
│   │   ├── dashboard/page.tsx         # Host metrics, recent requests & property quick-view
│   │   ├── properties/page.tsx        # Host properties management
│   │   ├── properties/new/page.tsx    # Property registration & moderation submission
│   │   ├── properties/[id]/page.tsx   # Edit property details, rooms & rates
│   │   ├── bookings/page.tsx          # Approve or decline guest booking requests
│   │   ├── calendar/page.tsx          # Stay calendar & availability schedule
│   │   └── profile/page.tsx           # Host partnership terms & 0% commission status
│   ├── admin/
│   │   ├── dashboard/page.tsx         # Platform overview & audit log
│   │   ├── properties/page.tsx        # Property verification & moderation actions
│   │   ├── bookings/page.tsx          # Master booking oversight
│   │   ├── users/page.tsx             # Administrator & host registry
│   │   ├── reviews/page.tsx           # Guest reviews integrity & moderation
│   │   └── settings/page.tsx          # Centralized commission & policy settings
│   └── api/
│       ├── properties/route.ts        # Server-side properties endpoint with rooms
│       ├── bookings/
│       │   ├── request/route.ts       # Server-validated booking request submission
│       │   ├── decision/route.ts      # Host/admin accept or decline action
│       │   └── cancel/route.ts        # Guest booking cancellation action
│       └── auth/callback/route.ts     # Supabase auth session exchange callback
├── components/
│   ├── header.tsx                     # Brand header with logo, navigation, auth status
│   ├── footer.tsx                     # Complete brand footer with philosophy & contact
│   ├── logo.tsx                       # Official Uttarkunth logo (#C85A20 on transparent)
│   ├── search-bar.tsx                 # Destination, dates, guest capacity picker
│   ├── property-card.tsx              # Property card with photos, badges, pricing in INR
│   ├── booking-widget.tsx             # Sticky booking panel with date math & price breakdown
│   ├── host-nav.tsx                   # Host portal navigation tabs
│   └── admin-nav.tsx                  # Administrator portal navigation tabs
├── lib/
│   ├── supabase/
│   │   ├── client.ts                  # Browser Supabase client (@supabase/ssr)
│   │   ├── server.ts                  # Server Supabase client with cookies (@supabase/ssr)
│   │   ├── admin.ts                   # Privileged server-only client (service_role)
│   │   └── types.ts                   # Generated TypeScript types from live Supabase DB
│   ├── booking-calculator.ts          # Nights math, price calculation, date conflict checks
│   ├── commission.ts                  # 0% intro (12 months) and 10% standard commission rules
│   ├── constants.ts                   # Brand constants, destinations, amenities, fallback data
│   ├── utils.ts                       # Tailwind merge & INR currency formatter
│   └── validations.ts                 # Zod runtime schemas
├── public/
│   ├── logo.png                       # Official Uttarkunth brand mark
│   └── images/
├── supabase/
│   └── migrations/                    # SQL migrations matching live Supabase project
├── tests/
│   ├── booking-pricing.test.ts        # Night bounds & price breakdown tests
│   ├── date-validation.test.ts        # Date validation & checkout exclusive boundary tests
│   ├── commission.test.ts             # 0% 12-month intro & 10% standard commission tests
│   └── zod-schemas.test.ts            # Zod validation tests
├── middleware.ts                      # Route protection & Supabase session refresh
├── open-next.config.ts                # OpenNext Cloudflare configuration
├── wrangler.jsonc                     # Cloudflare Workers configuration
├── package.json
├── tsconfig.json
├── next.config.mjs
├── tailwind.config.ts
├── postcss.config.mjs
├── .gitignore
└── .env.example
```

---

## 4. Local Installation & Development

### 1. Clone or Extract
Ensure you are in the project root:
```bash
cd uttarkunth3.0
```

### 2. Install Dependencies
```bash
npm install
```

### 3. Configure Environment Variables
Copy `.env.example` to `.env.local`:
```bash
cp .env.example .env.local
```

Fill in your Supabase project keys in `.env.local`:
```ini
NEXT_PUBLIC_SUPABASE_URL=https://xyplgugxpmlnjsvlosdg.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key
SUPABASE_SERVICE_ROLE_KEY=your_supabase_service_role_key
```

### 4. Run Development Server
```bash
npm run dev
```
Open [http://localhost:3000](http://localhost:3000) in your browser.

### 5. Run Automated Unit Tests
```bash
npm test
```
Runs the 17+ automated test suites verifying date arithmetic, checkout exclusive boundaries, pricing breakdowns in INR, and commission snapshots.

---

## 5. Live Properties & Database Schema

The application is wired directly to the live Supabase project `uttarkunth-stays` (`xyplgugxpmlnjsvlosdg`):

### Live Properties:
1. **Yash Home Stay** (`yash-home-stay`)
   - ID: `d9bba1a1-23bc-4844-a70b-aebcc820cf37`
   - Village: Jari, Kullu, Himachal Pradesh
   - Room: Mountain View Room (Max 2 Guests)
   - Published Rate: ₹900 / night
2. **Wonderway Retreat** (`wonderway-retreat`)
   - ID: `b1a8c6a7-e73c-431c-8727-c8e385dbd173`
   - Village: Jari, Kullu, Himachal Pradesh
   - Room: Mountain View Room (Max 2 Guests)
   - Published Rate: ₹3,500 / night

### Core Database Safeguards:
- `stay_bookings_no_overlapping_active_dates`: PostgreSQL exclusion constraint preventing concurrent confirmed or pending bookings for the same room.
- `enforce_property_ownership_and_moderation`: Database trigger ensuring host updates reset status to `pending`, preventing unauthorized instant publishing.
- `is_platform_admin`: Secure RPC verifying administrative roles.

---

## 6. Manual Upload to GitHub Repository `uttarkunth3.0`

Follow these exact steps to upload the project to your GitHub repository:

### Method A: Using Git CLI (Recommended)

1. Open a terminal in `uttarkunth3.0`:
   ```bash
   cd uttarkunth3.0
   ```
2. Initialize git (if not already initialized):
   ```bash
   git init
   git branch -M main
   ```
3. Add your remote repository:
   ```bash
   git remote add origin https://github.com/<YOUR_GITHUB_USERNAME>/uttarkunth3.0.git
   ```
4. Stage and commit all project files:
   ```bash
   git add .
   git commit -m "feat: complete Uttarkunth Stays 3.0 full-stack website for Cloudflare deployment"
   ```
5. Push to GitHub:
   ```bash
   git push -u origin main
   ```

### Method B: Using GitHub Web UI / ZIP

1. Use the pre-built `uttarkunth3.0.zip` deliverable provided in the project directory.
2. In your GitHub repository `uttarkunth3.0`, click **Add file** -> **Upload files**.
3. Drag and drop the extracted contents of `uttarkunth3.0` into the repository.
4. Commit the changes to `main`.

---

## 7. Cloudflare Deployment Configuration

Cloudflare is connected to your repository `uttarkunth3.0`.

### Cloudflare Build Settings:
Under **Cloudflare Dashboard** -> **Workers & Pages** -> **uttarkunth3** -> **Settings** -> **Builds & Deployments**:
- **Framework Preset:** None (or OpenNext / Next.js)
- **Build Command:** `npx @opennextjs/cloudflare build` (or `npm run build:worker`)
- **Deploy Command:** `npx wrangler deploy`
- **Output Directory:** `.open-next/assets`
- **Root Directory:** `/`
- **Compatibility Flag:** `nodejs_compat`
- **Compatibility Date:** `2024-12-30`

### Cloudflare Environment Variables & Secrets:
Under **Settings** -> **Variables and Secrets**:
1. `NEXT_PUBLIC_SUPABASE_URL` = `https://xyplgugxpmlnjsvlosdg.supabase.co`
2. `NEXT_PUBLIC_SUPABASE_ANON_KEY` = *(Your publishable anon key)*
3. `SUPABASE_SERVICE_ROLE_KEY` = *(Your service role key - set as Secret)*
4. `NODE_VERSION` = `20`

Once pushed to `main`, Cloudflare will automatically build, package with OpenNext, and deploy your edge worker globally!

---

## 8. Verification & Security Summary

- **Zero Secrets in Repository:** `.gitignore` protects `.env*`, `.next`, and `node_modules`.
- **Server-Side Price Authority:** Client inputs are never trusted for pricing or booking decisions. Total INR calculation is performed server-side.
- **Request-to-Book Enforcement:** Hosts review and approve every stay request.
- **Automated Tests:** 17 unit tests verifying pricing, night calculation, exclusive checkout boundary conflicts, and commission models.
