<div align="center">

# FreshCart

**A modern grocery storefront with live catalog data, search, filtering, cart, favorites and dark mode.**

![React](https://img.shields.io/badge/React-18-61DAFB?logo=react&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-5.6-3178C6?logo=typescript&logoColor=white)
![Vite](https://img.shields.io/badge/Vite-6-646CFF?logo=vite&logoColor=white)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-3-06B6D4?logo=tailwindcss&logoColor=white)
![Status](https://img.shields.io/badge/status-front--end_demo-lightgrey)

</div>

---

## Table of Contents

- [About](#about)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Getting Started](#getting-started)
- [Available Scripts](#available-scripts)
- [Routes](#routes)
- [Project Structure](#project-structure)
- [Architecture](#architecture)
- [Data Source](#data-source)
- [Local Storage](#local-storage)
- [Limitations](#limitations)
- [Roadmap](#roadmap)
- [License](#license)

## About

FreshCart is a single-page grocery storefront built with React and TypeScript. It loads a food-only catalog from the public [DummyJSON Products API](https://dummyjson.com/docs/products), groups products into food sections, and provides a complete browsing flow: discovery, search, filtering, product details, cart and favorites.

> **Project status:** Front-end demo. Checkout is simulated and no payment is collected.

## Features

**Catalog**
- Food-only catalog sourced from the `groceries` category; pet food and all non-food categories are excluded
- Six food sections generated from the product list: Dairy & Eggs, Meat & Fish, Fruits & Berries, Vegetables, Drinks and Pantry
- Product detail pages with related products

**Browsing**
- Text search across title, description, section and brand
- Section filtering, sorting and a sale-only filter
- Pagination with 12 products per page

**Shopping**
- Shopping cart with quantity controls and subtotal
- Favorites list
- Cart and favorites persisted in `localStorage`

**Experience**
- Light and dark themes with saved preference and system-theme detection
- Responsive navigation and layouts
- Skeleton loading states
- Retryable API error states
- Page animations with Framer Motion

## Tech Stack

| Technology | Purpose |
| --- | --- |
| [React 18](https://react.dev/) | Component-based UI |
| [TypeScript](https://www.typescriptlang.org/) | Static typing |
| [Vite](https://vitejs.dev/) | Development server and build tooling |
| [Tailwind CSS](https://tailwindcss.com/) | Utility-first styling |
| [React Router 6](https://reactrouter.com/) | Client-side routing |
| [Axios](https://axios-http.com/) | HTTP client |
| [Framer Motion](https://www.framer.com/motion/) | Animations |
| [Lucide React](https://lucide.dev/) | Icons |

## Getting Started

### Prerequisites

- Node.js 18 or newer
- npm 9 or newer

### Installation

```bash
git clone https://github.com/your-username/fresh-cart-landing.git
cd fresh-cart-landing
npm install
```

### Run Locally

```bash
npm run dev
```

Open the local URL printed by Vite (usually `http://localhost:5173`).

### Production Build

```bash
npm run build
npm run preview
```

The optimized output is generated in the `dist/` directory.

## Available Scripts

| Command | Description |
| --- | --- |
| `npm run dev` | Start the development server |
| `npm run build` | Type-check with `tsc -b` and create a production build |
| `npm run preview` | Serve the production build locally |

## Routes

| Path | Page |
| --- | --- |
| `/` | Home |
| `/shop` | Product listing with search, filters, sorting and pagination |
| `/categories` | All food sections |
| `/category/:slug` | Products in a single section |
| `/product/:id` | Product details and related products |
| `/cart` | Shopping cart and demo checkout |
| `/favorites` | Saved products |
| `/about` | About page |
| `*` | Not found |

## Project Structure

```text
fresh-cart-landing/
├── src/
│   ├── api/
│   │   └── productsApi.ts
│   ├── components/
│   │   ├── layout/
│   │   │   ├── Footer.tsx
│   │   │   ├── Header.tsx
│   │   │   └── MainLayout.tsx
│   │   └── products/
│   │       ├── Pagination.tsx
│   │       ├── ProductCard.tsx
│   │       └── ProductSkeleton.tsx
│   ├── context/
│   │   ├── CartContext.tsx
│   │   ├── FavoritesContext.tsx
│   │   └── ThemeContext.tsx
│   ├── pages/
│   │   ├── AboutPage.tsx
│   │   ├── CartPage.tsx
│   │   ├── CategoriesPage.tsx
│   │   ├── CategoryPage.tsx
│   │   ├── FavoritesPage.tsx
│   │   ├── HomePage.tsx
│   │   ├── NotFoundPage.tsx
│   │   ├── ProductDetailsPage.tsx
│   │   └── ShopPage.tsx
│   ├── types/
│   │   └── product.ts
│   ├── App.tsx
│   ├── index.css
│   └── main.tsx
├── index.html
├── package.json
├── postcss.config.js
├── tailwind.config.js
├── tsconfig.json
└── vite.config.ts
```

## Architecture

| Layer | Location | Responsibility |
| --- | --- | --- |
| API | `src/api/productsApi.ts` | Fetches the catalog once, caches the request, and performs filtering, sorting, searching and pagination on the client. A failed request clears the cache so it can be retried. |
| Context | `src/context/` | `CartProvider`, `FavoritesProvider` and `ThemeProvider` hold global state and persist it to `localStorage`. |
| Pages | `src/pages/` | Route-level screens. |
| Components | `src/components/` | Reusable layout and product UI. |
| Types | `src/types/product.ts` | Shared data contracts: `Product`, `ProductResponse`, `Category`, `CartItem`. |

## Data Source

Product data and images come from [DummyJSON](https://dummyjson.com/). The application requests only the `groceries` category and then:

1. Removes non-food items such as pet food.
2. Assigns each product to one of six sections by matching its title; the first matching rule wins and unmatched products fall into Pantry.
3. Treats products with a discount of 10% or more as on sale.

Section rules are defined in `SECTIONS` inside `src/api/productsApi.ts`.

## Local Storage

| Key | Content |
| --- | --- |
| `freshcart-cart` | Cart items and quantities |
| `freshcart-favorites` | Favorite product IDs |
| `freshcart-theme` | Selected theme (`light` or `dark`) |

## Limitations

- An internet connection is required to load API data and remote product images.
- Checkout is a front-end demo and does not process payments.
- Prices are sample catalog values from the API, not live grocery prices.
- Cart and favorites are stored per browser and are not synced across devices.

## Roadmap

- [ ] Real backend with authentication and order history
- [ ] Payment integration
- [ ] Automated tests
- [ ] Reduced-motion support and automated accessibility checks

## License

This project is provided as a learning and portfolio project. Add a license file before redistributing it as an open-source package.