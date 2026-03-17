<div align="center">


# <img width="675" height="105" alt="image" src="https://github.com/user-attachments/assets/8f42da58-64b2-4149-9aa6-422d0f8c8393" />

### Vehicle Defect Intelligence Platform

Real-time vehicle defect intelligence powered by live NHTSA data — built for legal professionals.

[![React](https://img.shields.io/badge/React-19-61DAFB?style=flat-square&logo=react)](https://react.dev)
[![TypeScript](https://img.shields.io/badge/TypeScript-5-3178C6?style=flat-square&logo=typescript)](https://www.typescriptlang.org)
[![Vite](https://img.shields.io/badge/Vite-8-646CFF?style=flat-square&logo=vite)](https://vitejs.dev)
[![NHTSA](https://img.shields.io/badge/Data-NHTSA%20Public%20API-navy?style=flat-square)](https://api.nhtsa.gov)
[![License](https://img.shields.io/badge/License-Proprietary-gold?style=flat-square)](#license)

</div>

---

## Overview

The **Vehicle Defect Intelligence Platform** gives legal professionals and researchers instant access to comprehensive vehicle safety data from the National Highway Traffic Safety Administration (NHTSA). Decode any VIN, browse safety recalls, analyze consumer complaints, and visualize defect trends — all with live data, no login required.

- **No database. No API keys. No login.** All data sourced directly from NHTSA's public APIs.
- **One VIN unlocks everything** — decode once and every tab auto-populates for that vehicle.
- **Built for law firms** — deep navy and gold aesthetic with Playfair Display typography.

---

## System Architecture

> The diagram below illustrates the full system — from the React SPA in the browser, through the Vite dev proxy (CORS resolution), to the two NHTSA public API endpoints.

<img width="1980" height="1400" alt="Untitled-2026-03-16-1920" src="https://github.com/user-attachments/assets/61af4577-efd2-459f-acf5-ae6d02f4b02d" />

The app is a single-page React application. In development, a Vite proxy forwards requests to NHTSA to solve CORS. In production, this is replaced by Vercel/Netlify redirects. No backend server is required at any stage.

---

## Features

| Page | What it does |
|---|---|
| **Overview** | Hero landing page with platform introduction and live stats |
| **VIN Lookup** | Decode any 17-character VIN — auto-populates all sections |
| **Recalls** | Browse NHTSA safety recalls by brand, model, and year |
| **Complaints** | Consumer complaints with expandable row details |
| **Analytics** | Charts: top components, timeline, crashes vs fires, US choropleth map |
| **Methodology** | Explains data sources and how to interpret results |

### Highlights

- **Format-validated VIN input** — rejects malformed VINs before making any API call
- **38 bundled brand logos** — official manufacturer logos, no CDN dependency
- **Accordion recall cards** — smooth animated expand/collapse for each recall
- **Interactive US choropleth map** — complaint density by state with hover tooltips
- **Composed charts** — bar, pie, line, and composed chart types via Recharts
- **Page transitions** — Framer Motion animations between tabs

---

## Tech Stack

| Category | Technology | Version |
|---|---|---|
| Framework | React + TypeScript | 19.x |
| Build Tool | Vite | 8.x |
| Styling | Inline CSS + CSS Custom Properties | — |
| Animations | Framer Motion | 12.x |
| Charts | Recharts | 3.x |
| Map | react-simple-maps + d3-scale | 3.x / 4.x |
| HTTP Client | Axios | 1.x |
| Icons | Lucide React | 0.577+ |
| Data Source | NHTSA vPIC API + NHTSA Complaints/Recalls API | Public |

---

## Project Structure

```
app/
├── public/
│   ├── slp-logo.png
│   ├── brand-logos/               # 38 manufacturer logos (local, no CDN)
│   │   ├── ford.png
│   │   ├── toyota.png
│   │   ├── bmw.png
│   │   └── ...
│   └── vite.svg
├── docs/
│   └── architecture.png           # System architecture diagram
├── src/
│   ├── api/
│   │   └── nhtsa.ts               # All NHTSA API calls
│   ├── components/
│   │   ├── BrandLogo.tsx
│   │   ├── ComplaintRow.tsx
│   │   ├── Header.tsx
│   │   ├── RecallCard.tsx
│   │   ├── USMap.tsx
│   │   └── VINQuickSearch.tsx
│   ├── pages/
│   │   ├── HomePage.tsx
│   │   ├── VINLookupPage.tsx
│   │   ├── VehicleSearchPage.tsx
│   │   ├── ComplaintsPage.tsx
│   │   ├── AnalyticsPage.tsx
│   │   └── AboutPage.tsx
│   ├── types.ts
│   ├── App.tsx
│   ├── index.css
│   └── main.tsx
├── vite.config.ts
├── tsconfig.json
├── tsconfig.app.json
├── package.json
└── README.md
```

---

## Prerequisites

| Tool | Minimum Version | Download |
|---|---|---|
| Node.js | v18.0.0 | [nodejs.org](https://nodejs.org) |
| npm | v9.0.0 | Included with Node |
| Git | Any | [git-scm.com](https://git-scm.com) |

Verify your versions:

```bash
node -v    # v18.0.0 or higher
npm -v     # v9.0.0 or higher
git --version
```

---

## Installation & Setup

### 1. Clone the repository

```bash
git clone https://github.com/SreekarJenepalli/Strategic-Legal-Practices.git
cd Strategic-Legal-Practices
```

### 2. Install dependencies

```bash
npm install --legacy-peer-deps
```

> **Why `--legacy-peer-deps`?**
> `react-simple-maps` (used for the US choropleth map) has not yet updated its peer dependency declaration for React 19. This flag skips that conflict check — the package works correctly at runtime and there is no functional impact.

You may see deprecation warnings during install — these are safe to ignore.

---

## Running Locally

```bash
npm run dev
```

Then open your browser at:

```
http://localhost:5173
```

The app supports **hot module replacement** — changes to any file are reflected instantly without a full page reload.

---

## Data Sources

All data is fetched live from two NHTSA public APIs — no API key or authentication required.

### NHTSA vPIC API
**Base URL:** `https://vpic.nhtsa.dot.gov/api/vehicles`

| Endpoint | Returns |
|---|---|
| `GET /DecodeVinValues/{vin}?format=json` | Make, model, year, engine, error codes |
| `GET /GetAllMakes?format=json` | All registered vehicle makes |
| `GET /GetModelsForMakeYear/make/{m}/modelyear/{y}` | Models for a given make and year |

### NHTSA Complaints & Recalls API
**Base URL:** `https://api.nhtsa.gov`

| Endpoint | Returns |
|---|---|
| `GET /complaints/complaintsByVehicle?make=&model=&modelYear=` | Crashes, fires, injuries, deaths, ODI#, components, summary |
| `GET /recalls/recallsByVehicle?make=&model=&modelYear=` | Campaign#, component, consequence, remedy, units affected |

### CORS Handling

In development, `vite.config.ts` proxies API calls:

```
/api/vpic/*  →  vpic.nhtsa.dot.gov/api/vehicles
/api/nhtsa/* →  api.nhtsa.gov
```

In production, replace with Vercel `vercel.json` rewrites or Netlify `_redirects`.

---

## Design System

| Token | Value |
|---|---|
| Primary color | `#0d1f3c` (deep navy) |
| Accent color | `#b8962e` (gold) |
| Heading font | Playfair Display |
| Body font | Inter |
| Base font size | 16px |
| Border radius | 8px |

---

## License

Built exclusively for **Strategic Legal Practice**. All rights reserved.

No part of this codebase may be reproduced, distributed, or used outside the scope of its original commission without explicit written permission.
