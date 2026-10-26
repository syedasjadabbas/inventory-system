# Inventory System

> Offline-first inventory and point-of-sale (POS) progressive web application for small retail and food businesses.

For the initial design requirements and feature specification, see [docs/ORIGINAL_SPEC.md](docs/ORIGINAL_SPEC.md).

---

## Overview

Inventory System is a zero-latency, local-first Progressive Web Application (PWA) providing inventory tracking, point-of-sale transactions, and business analytics. Designed to operate reliably without continuous internet connectivity, all database operations, product lookups, transactions, and receipt generations execute locally on the client device via IndexedDB.

---

## Key Features

### 1. Point of Sale (POS)
- **Fast Touch Order Entry**: Visual product grid with large touch targets, real-time search, and category filtering.
- **Dual Checkout Modes**: 1-tap quick sales directly from item tiles, or full multi-item cart drawer with tax, discount, and cash change computation.
- **Hardware Compatibility**: Supports USB and Bluetooth handheld barcode scanners via auto-focused keystroke capture.
- **Receipt Printing**: Print-optimized stylesheet (`@media print`) formatted for 58mm and 80mm thermal receipt printers, as well as standard A4 summary sheets.

### 2. Inventory & Stock Control
- **Unified Catalog**: Product SKU, barcode, unit measurements (pcs, kg, grams, ml), cost price, selling price, and photo attachments.
- **Event-Driven Ledger**: Stock movements (intake, sale, adjustment, spoilage) are recorded as an append-only event log.
- **Threshold Alerts**: Visual indicators and badges for items reaching or falling below minimum stock levels.
- **Bill of Materials (BOM) / Recipes**: Automatic raw ingredient decrementing when composite menu items (e.g., meals, burgers) are sold.

### 3. Register & Financials
- **Cash Drawer Management**: Opening and closing cash float records with shift reconciliation.
- **Customer & Supplier Records**: Contact management, purchase history, outstanding customer balances, and supplier purchase orders.

### 4. Reporting, Analytics & Data Safety
- **Business Dashboard**: Real-time sales volume, revenue KPIs, top-selling items, and total inventory valuation.
- **Data Export & Import**: Client-side CSV/Excel export for inventory audits and sales logs; bulk CSV import for initial catalogue onboarding.
- **Local Disaster Recovery**: 1-click full JSON database export and restore functionality to safeguard against device replacement or browser cache clearing.

---

## Architecture & Stack

- **Client Application**: Vanilla HTML5, CSS3, and modern modular ES6+ JavaScript.
- **Local Storage Engine**: IndexedDB (`js/db.js`) providing client-side persistence for products, orders, categories, and audit logs.
- **Offline Reliability**: Service Worker (`service-worker.js`) caching core application assets for uninterrupted offline functionality.
- **Installation**: Web App Manifest (`manifest.json`) enabling home screen installation on iOS, Android, macOS, and Windows.

---

## Project Structure

```
inventory-system/
├── index.html              # Main application shell and layout views
├── manifest.json           # Web App Manifest for PWA installation
├── service-worker.js       # Cache management and offline execution
├── docs/
│   └── ORIGINAL_SPEC.md    # Original architectural specification
├── js/
│   ├── db.js               # IndexedDB storage layer and transaction schemas
│   ├── router.js           # Client-side hash routing
│   ├── utils.js            # Formatting, calculation, and export helpers
│   ├── components/         # Reusable modal and alert UI elements
│   └── pages/              # Modular page controllers
│       ├── dashboard.js    # Executive KPI summary
│       ├── pos.js          # Point of sale interface
│       ├── inventory.js    # Stock management and batch tracking
│       ├── recipes.js      # Bill of materials and ingredient rules
│       ├── register.js     # Cash drawer floats and closing summaries
│       ├── customers.js    # Customer accounts and balances
│       ├── suppliers.js    # Supplier contact and purchase tracking
│       ├── reports.js      # Sales reports and CSV exports
│       ├── analytics.js    # Sales trend visual charts
│       └── settings.js     # Currency, tax rates, and backup/restore
├── styles/                 # Application stylesheets and print layouts
└── icons/                  # PWA application icons
```

---

## Getting Started

### Prerequisites

Because modern browsers restrict Service Workers and ES modules when opening files directly via `file://`, a static local HTTP web server is required.

- Python 3.x, or
- Node.js (with `serve` or `http-server`), or
- A code editor extension such as VS Code Live Server.

### Running Locally

Clone the repository and serve the root directory:

```bash
# Clone the repository
git clone https://github.com/syedasjadabbas/inventory-system.git
cd inventory-system

# Option A: Using Python
python -m http.server 8000

# Option B: Using Node.js npx
npx serve . -p 8000
```

Open your browser and navigate to:
```
http://localhost:8000
```

### PWA Installation

To install the application as a standalone desktop or mobile app:
1. Open the application in Google Chrome, Microsoft Edge, or Safari over `localhost` or HTTPS.
2. Click the **Install** icon in the browser address bar (or select "Add to Home Screen" on mobile devices).
