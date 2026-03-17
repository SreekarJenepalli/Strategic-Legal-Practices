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
A professional web application that provides real-time vehicle defect intelligence using live data from the **National Highway Traffic Safety Administration (NHTSA)** public API. Built for Strategic Legal Practice to support case evaluation, recall tracking, and consumer complaint analysis.

---
## Table of Contents

1. [Project Overview](#project-overview)
2. [System Architecture](#system-architecture)
3. [Live Features](#live-features)
4. [Tech Stack](#tech-stack)
5. [Project Structure](#project-structure)
6. [Prerequisites](#prerequisites)
7. [Installation & Setup](#installation--setup)
8. [Running Locally](#running-locally)


---

## Project Overview

This platform allows legal professionals and researchers to:

- Decode any **17-character Vehicle Identification Number (VIN)** and instantly retrieve full vehicle specs
- View all **NHTSA Safety Recalls** for a specific vehicle
- Browse all **Consumer Complaints** filed against a vehicle
- Analyze defect trends with **interactive charts and a live US choropleth map**
- Identify the most commonly reported failure components

All data is sourced **live** from NHTSA's public APIs — no database, no login, no API keys required.

---

## System Architecture

> The diagram below illustrates the full system — from the React SPA running in the browser, through the Vite dev proxy (which resolves CORS), down to the two NHTSA public API endpoints.

<img width="1980" height="1400" alt="Untitled-2026-03-16-1920" src="https://github.com/user-attachments/assets/d9f07049-aa7f-4756-ad90-6b19fbbf1e64" />

The app is a fully client-side React SPA. In development, `vite.config.ts` proxies all `/api/vpic/*` and `/api/nhtsa/*` calls to their respective NHTSA origins to bypass browser CORS restrictions. In production, these proxies are replaced by Vercel rewrite rules or Netlify `_redirects` — no backend server is needed at any stage.

---

## Live Features

| Page | Description |
|---|---|
| **Overview** | Hero landing page with platform introduction and key stats |
| **VIN Lookup** | Decode any VIN — auto-populates all sections globally |
| **Recalls** | Browse safety recalls by brand, model, and year |
| **Complaints** | Browse consumer complaints with expandable row details |
| **Analytics** | Charts: top components, complaints timeline, crashes vs fires, US map |
| **Methodology** | Explains data sources and how to interpret results |

### Key Highlights
- **One VIN, all sections** — decode once, every tab auto-loads data for that vehicle
- **Brand logos** — official manufacturer logos displayed (38 brands bundled locally, no CDN)
- **Accordion recalls** — click to expand each recall card with smooth animation
- **Invalid VIN detection** — format-validated before API call with clear error messaging
- **Interactive US map** — complaint density by state with hover tooltips
- **Deep navy + gold theme** — Playfair Display + Inter fonts for a law-firm aesthetic

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
│   ├── brand-logos/                 
│   │   ├── ford.png
│   │   ├── toyota.png
│   │   ├── bmw.png
│   │   └── ... (35 more brands)
│   └── vite.svg
├── docs/
│   └── architecture.png             # System architecture diagram
├── src/
│   ├── api/
│   │   └── nhtsa.ts                 # All NHTSA API calls (VIN decode, recalls, complaints)
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

Install the following before proceeding:

### 1. Node.js v18 or later
Download: [https://nodejs.org](https://nodejs.org)

```bash
node -v     # Must be v18.0.0 or higher
npm -v      # Must be v9.0.0 or higher
```

### 2. Git
Download: [https://git-scm.com](https://git-scm.com)

```bash
git --version
```

---

## Installation & Setup

### Step 1 — Clone the repository

```bash
git clone https://github.com/SreekarJenepalli/Strategic-Legal-Practices.git
cd Strategic-Legal-Practices
```

### Step 2 — Install all dependencies

```bash
npm install --legacy-peer-deps
```

> **Why `--legacy-peer-deps`?**
> The `react-simple-maps` package (used for the US map) has not yet updated its peer dependency declaration for React 19. This flag tells npm to skip that conflict check. The package works correctly at runtime — this flag does not affect the app in any way.

You will likely see some deprecation warnings in the terminal — these are safe to ignore.

---

## Running Locally

```bash
npm run dev
```

Open your browser and go to:
```
http://localhost:5173
```

The app hot-reloads automatically on every file save. No restart needed during development.

## License

Built exclusively for **Strategic Legal Practice**. All rights reserved.
