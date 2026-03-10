# ◈ StockFlow — Inventory Management MVP

> A lightweight, single-file SaaS inventory management app built with pure HTML, CSS & JavaScript. Zero dependencies. No build step. Works by opening directly in any browser.

![StockFlow](https://img.shields.io/badge/version-v0.1.0-f5a623?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-4caf7d?style=flat-square)
![Dependencies](https://img.shields.io/badge/dependencies-zero-4caf7d?style=flat-square)
![Build](https://img.shields.io/badge/build-none%20required-4caf7d?style=flat-square)

---

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Getting Started](#getting-started)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [Screens](#screens)
- [Demo Credentials](#demo-credentials)
- [Deployment](#deployment)
- [Roadmap](#roadmap)
- [Contributing](#contributing)
- [License](#license)

---

## Overview

StockFlow is a Phase 1 MVP for a multi-tenant SaaS inventory management system. It was designed to be shipped in ~6 hours for demo or internal use. The goal is simplicity — a small seller or internal team can sign up, add products, track stock levels, and get alerted on low-stock items instantly.

All data is scoped per organization (multi-tenant), and the entire app ships as a **single `.html` file** with no external dependencies beyond Google Fonts.

---

## ✨ Features

### Authentication
- ✅ Sign up with email, password & organization name
- ✅ Login with email & password
- ✅ Form validation with inline error messages
- ✅ One organization created per user on signup
- ✅ All data scoped by organization (no cross-tenant leaks)

### Dashboard
- ✅ Total products count
- ✅ Total units in stock
- ✅ Total inventory value (at selling price)
- ✅ Low stock alert count
- ✅ Low stock items table with status badges

### Products
- ✅ Create product (Name, SKU, Qty, Cost Price, Selling Price, Threshold, Description)
- ✅ Edit product — all fields editable
- ✅ Delete product with confirmation dialog
- ✅ Search/filter by name or SKU (live, client-side)
- ✅ Inline stock adjustment (`± Adj` button: enter `+10` or `-5`)
- ✅ SKU uniqueness validation per organization
- ✅ Status badges: `IN STOCK` / `LOW STOCK` / `OUT OF STOCK`

### Settings
- ✅ View organization name and account email
- ✅ Set global default low stock threshold
- ✅ Per-product threshold overrides the global default

---

## 🛠 Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Pure HTML5, CSS3, Vanilla JavaScript (ES2020) |
| Fonts | Google Fonts — Syne (UI) + Space Mono (data) |
| Data Storage | In-memory JavaScript object (session only) |
| Auth | Simple email/password matching (in-memory) |
| Build Tool | None required |
| Dependencies | None (zero npm packages) |

> **Note:** This is an MVP / prototype. Data does not persist between page refreshes. For production, replace the in-memory store with a real backend (Node.js + PostgreSQL recommended).

---

## 🚀 Getting Started

### Option 1 — Open directly (simplest)

```bash
# Just download stockflow.html and open it in your browser
open stockflow.html
```

No server, no install, no build — it just works.

### Option 2 — VS Code with Live Server

1. Open `stockflow.html` in VS Code
2. Install the **Live Server** extension (by Ritwick Dey)
3. Right-click the file → **Open with Live Server**
4. App opens at `http://127.0.0.1:5500`

### Option 3 — Local HTTP server

```bash
# Python
python3 -m http.server 3000

# Node.js
npx serve .

# Then open http://localhost:3000/stockflow.html
```

---

## 📖 Usage

### 1. Sign Up or Use Demo Account

Open the app and either:
- Click **"Create one free"** to register a new organization
- Or use the pre-loaded demo account (see [Demo Credentials](#demo-credentials))

### 2. Dashboard

After login you land on the Dashboard. You'll see:
- Summary cards with total products, units, value, and alerts
- A low stock table listing all products at or below their threshold

### 3. Add Products

Navigate to **Products → + Add Product**. Fill in:

| Field | Required | Notes |
|---|---|---|
| Name | ✅ | Display name |
| SKU | ✅ | Unique per org, auto-uppercased |
| Qty on Hand | ✅ | Current stock count |
| Description | ❌ | Optional |
| Cost Price | ❌ | Purchase cost |
| Selling Price | ❌ | Used for inventory value calculation |
| Low Stock Threshold | ❌ | Overrides global default if set |

### 4. Adjust Stock

When editing a product, click **± Adj** to quickly add or subtract units:
```
Enter: +10   → adds 10 units
Enter: -5    → removes 5 units (min 0)
```

### 5. Low Stock Alerts

A product is flagged as **LOW STOCK** when:
```
Qty on Hand  <=  Product Threshold  (or Global Default if not set)
```

Set the global default in **Settings → Default Low Stock Threshold**.

---

## 📁 Project Structure

```
stockflow/
│
├── stockflow.html        # The entire application (HTML + CSS + JS)
├── README.md             # This file
└── StockFlow.jsx         # Original React source (reference only)
```

### Inside `stockflow.html`

```
stockflow.html
├── <head>
│   ├── Google Fonts import
│   └── <style> — all CSS variables, layout, components
│
├── <body>
│   ├── #auth-screen       — Login & Signup forms
│   ├── #app-shell
│   │   ├── #sidebar       — Navigation + org info + logout
│   │   └── #main-content
│   │       ├── #page-dashboard   — Stats cards + low stock table
│   │       ├── #page-products    — Product list + search
│   │       └── #page-settings    — Global threshold setting
│   ├── #prod-modal        — Create / Edit product form
│   └── #del-modal         — Delete confirmation dialog
│
└── <script>
    ├── DB {}              — In-memory data store
    ├── Auth functions     — signup(), login(), enterApp()
    ├── Navigation         — navigate()
    ├── Dashboard          — renderDash()
    ├── Products           — renderProdsPage(), saveProduct()
    ├── Settings           — saveSettings()
    └── Utilities          — toast(), esc(), fmt2()
```

---

## 🖥 Screens

| Screen | Route/Trigger | Description |
|---|---|---|
| Login | Default | Email + password sign in |
| Sign Up | Click "Create one free" | Register with org name |
| Dashboard | `navigate('dashboard')` | Stats + low stock list |
| Products | `navigate('products')` | Full product table + search |
| Add Product | Click "+ Add Product" | Modal form |
| Edit Product | Click "Edit" on a row | Pre-filled modal form |
| Delete Product | Click "Delete" on a row | Confirmation modal |
| Settings | `navigate('settings')` | Global threshold config |

---

## 🔑 Demo Credentials

```
Email:     demo@stockflow.io
Password:  demo1234
Org:       Demo Store
```

The demo account is pre-seeded with **5 sample products**:

| Product | SKU | Qty | Threshold | Status |
|---|---|---|---|---|
| Wireless Earbuds Pro | WEP-001 | 3 | 5 | 🟡 LOW STOCK |
| USB-C Hub 7-in-1 | HUB-007 | 12 | 10 | 🟢 IN STOCK |
| Mechanical Keyboard | MKB-TKL | 2 | 5 | 🟡 LOW STOCK |
| Webcam 4K HD | CAM-4K1 | 8 | 5 | 🟢 IN STOCK |
| Desk Lamp LED | LMP-LED3 | 4 | 8 | 🟡 LOW STOCK |

---

## 🌐 Deployment

Since the app is a single HTML file, deployment is simple:

### Netlify Drop (30 seconds)
1. Rename `stockflow.html` → `index.html`
2. Go to [netlify.com/drop](https://netlify.com/drop)
3. Drag and drop the file

### GitHub Pages
```bash
git init
mv stockflow.html index.html
git add . && git commit -m "deploy"
git remote add origin https://github.com/YOUR_USERNAME/stockflow.git
git push -u origin main
# Enable Pages in repo Settings → Pages → Branch: main
```

### Vercel
```bash
npm install -g vercel
mv stockflow.html index.html
vercel deploy
```

### Nginx / VPS
```bash
scp stockflow.html user@your-server:/var/www/html/index.html
```

---

## 🗺 Roadmap

These features are **out of scope for MVP** but planned for future phases:

### Phase 2
- [ ] Real backend (Node.js + Express + PostgreSQL)
- [ ] Persistent data with proper database
- [ ] JWT-based authentication
- [ ] Password reset via email

### Phase 3
- [ ] Multi-user support per organization (invites, roles)
- [ ] Stock movement history / audit log
- [ ] CSV import/export
- [ ] Email notifications for low stock

### Phase 4
- [ ] Multi-warehouse support
- [ ] Product variants (size, color, etc.)
- [ ] Purchase orders & supplier management
- [ ] Shopify / WooCommerce integrations
- [ ] Billing & subscription management

---

## 🤝 Contributing

Contributions are welcome! To get started:

```bash
# 1. Fork the repository
# 2. Clone your fork
git clone https://github.com/YOUR_USERNAME/stockflow.git
cd stockflow

# 3. Make your changes to stockflow.html
# 4. Test by opening in browser

# 5. Commit and push
git add .
git commit -m "feat: your feature description"
git push origin main

# 6. Open a Pull Request
```

### Guidelines
- Keep the app as a single HTML file for MVP phase
- Test in Chrome, Firefox, and Safari before submitting
- Follow the existing CSS variable naming conventions
- Add comments for any new JavaScript functions

---

## 📄 License

```
MIT License

Copyright (c) 2026 StockFlow

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
```

---

<div align="center">

Built with ◈ by the StockFlow team · [Report a Bug](https://github.com/YOUR_USERNAME/stockflow/issues) · [Request a Feature](https://github.com/YOUR_USERNAME/stockflow/issues)

</div>
