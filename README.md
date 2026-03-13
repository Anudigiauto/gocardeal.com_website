# 🚗 GoCarDeal — Automotive Marketplace

> **gocardeal.com** — Buy, Sell & Trade Vehicles Across Canada, USA & India

A production-ready automotive marketplace connecting car buyers, sellers, and verified dealers across 3 countries.

---

## 🌐 Live Features

| Page | Description |
|------|-------------|
| **Homepage** | Hero, search bar, featured vehicles, how-it-works, trust indicators, testimonials |
| **Shop Vehicles** | Filter sidebar (make/model/year/price/mileage/fuel/body type), vehicle cards, pagination |
| **Sell / Trade** | Full vehicle submission form with photo upload, location selection |
| **Finance** | Interactive loan calculator (price, down payment, rate, term), finance application |
| **Service** | Service booking form, 6 service types |
| **RV Marketplace** | RV and camper listings |
| **Insurance** | Insurance quote comparison form |
| **Dealer Network** | Verified dealer directory, CA / US / IN filter |
| **Tools & Resources** | Trade-in estimator, loan calculator, VIN check links |
| **About** | Mission, team, stats, awards |
| **FAQ** | Tabbed FAQ (Buying / Selling / Dealers / Finance) |
| **Blog** | Article grid with categories |
| **Contact** | Contact form, phone/email/address |
| **Dealer Pricing** | 3-tier subscription plans |
| **Dealer Dashboard** | Stats, lead table, inventory snapshot |

---

## 🚀 Quick Start

### Option 1: Open Directly
```bash
open index.html
```

### Option 2: Local Server
```bash
npx serve .
# or
python3 -m http.server 3000
```

### Option 3: Deploy to GitHub Pages
```bash
git init
git add .
git commit -m "Initial GoCarDeal deployment"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/gocardeal.git
git push -u origin main
# Then enable GitHub Pages in repo Settings > Pages > main branch
```

### Option 4: Deploy to Vercel (Recommended)
```bash
npm i -g vercel
vercel
# Follow prompts — site live in 60 seconds
```

### Option 5: Deploy to Netlify
```bash
# Drag & drop the /gocardeal folder onto netlify.com/drop
# Or use Netlify CLI:
npm i -g netlify-cli
netlify deploy --prod --dir .
```

---

## 📁 Project Structure

```
gocardeal/
├── index.html          # Complete single-file application
├── README.md           # This file
├── vercel.json         # Vercel deployment config
├── .github/
│   └── workflows/
│       └── deploy.yml  # GitHub Pages auto-deploy
└── assets/             # (add images here when available)
```

---

## 🛠 Full-Stack Architecture (Production Upgrade Path)

When ready to upgrade to full database + authentication:

```
/app
  /api
    /vehicles          # CRUD vehicle listings
    /dealers           # Dealer management
    /leads             # Lead capture & routing
    /auth              # NextAuth providers
  /components
    /layout            # Navbar, Footer, Layout
    /sections          # Hero, SearchBar, HowItWorks
    /cards             # VehicleCard, DealerCard
    /forms             # SellForm, ContactForm, FinanceForm
    /ui                # Button, Badge, Modal, Toast
  /pages
    /shop              # Vehicle search & listing
    /sell              # Seller submission
    /finance           # Calculator + application
    /service           # Service booking
    /dealers           # Dealer directory
    /dashboard         # Dealer dashboard (protected)
    /admin             # Admin panel (protected)
/prisma
  schema.prisma        # PostgreSQL database schema
/lib
  db.ts                # Prisma client
  auth.ts              # NextAuth config
  s3.ts                # AWS S3 / Cloudinary uploads
```

---

## 🗄 Database Schema (PostgreSQL / Prisma)

```prisma
model Vehicle {
  id          String   @id @default(cuid())
  make        String
  model       String
  year        Int
  mileage     Int
  price       Decimal
  currency    String   @default("CAD")
  fuelType    String
  transmission String
  condition   String
  description String?
  photos      String[] // Cloudinary URLs
  country     String   // CA / US / IN
  city        String
  status      String   @default("active")
  dealer      Dealer   @relation(fields: [dealerId], references: [id])
  dealerId    String
  leads       Lead[]
  createdAt   DateTime @default(now())
}

model Dealer {
  id          String    @id @default(cuid())
  name        String
  email       String    @unique
  phone       String
  country     String
  city        String
  plan        String    @default("starter")
  verified    Boolean   @default(false)
  vehicles    Vehicle[]
  leads       Lead[]
  createdAt   DateTime  @default(now())
}

model Lead {
  id         String   @id @default(cuid())
  type       String   // contact / test-drive / finance / best-price
  buyerName  String
  buyerEmail String
  buyerPhone String
  vehicle    Vehicle  @relation(fields: [vehicleId], references: [id])
  vehicleId  String
  dealer     Dealer   @relation(fields: [dealerId], references: [id])
  dealerId   String
  status     String   @default("new")
  createdAt  DateTime @default(now())
}
```

---

## 🎨 Design System

| Variable | Value |
|----------|-------|
| Background | `#0a0a0f` |
| Accent Red | `#e63b2e` |
| Accent Orange | `#ff6b35` |
| Text Primary | `#f0f0f8` |
| Font Display | Syne (Google Fonts) |
| Font Body | DM Sans |
| Font Mono | Space Mono |

---

## 🌍 SEO Pages Included

- `/used-cars-toronto` → Toronto, ON listings
- `/used-cars-vancouver` → Vancouver, BC listings
- `/used-cars-new-york` → New York, NY listings
- `/used-cars-dallas` → Dallas, TX listings
- `/used-cars-mumbai` → Mumbai, India listings

Structured schema markup:
- `AutoDealer` schema
- `Vehicle` schema (per listing)
- `LocalBusiness` schema
- `FAQPage` schema

---

## 💰 Monetization

| Revenue Stream | Details |
|----------------|---------|
| Starter Plan | $99/mo — 25 listings, 50 leads |
| Professional Plan | $299/mo — 150 listings, unlimited leads |
| Enterprise Plan | $799/mo — unlimited everything |
| Featured Listings | Premium placement fees |
| Finance Referrals | Per-application commissions |
| Insurance Referrals | Per-quote commissions |

---

## 📞 Support

- Email: hello@gocardeal.com
- Canada: +1 (416) 555-0100
- USA: +1 (214) 555-0100
- India: +91 98765 43210

---

*Built with ❤️ for the automotive community across Canada, USA, and India.*
