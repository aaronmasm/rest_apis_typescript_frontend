# Product Admin Dashboard — Client (React + TypeScript + Vite)

Frontend for a products admin dashboard. This client consumes a REST API and provides CRUD operations for products (list, create, edit, delete, toggle availability). Built with React 19, Vite 6, TypeScript, React Router, Tailwind CSS, Axios, and Valibot for runtime validation.

Live app: https://restapistypescriptfrontend.vercel.app/
Related backend (external): https://github.com/aaronmasm/Uptask_Backend

Note: This README documents this repository (the client). The linked backend is a separate project.

## Stack
- Language: TypeScript
- Framework/Library: React 19
- Build tool/dev server: Vite 6 (@vitejs/plugin-react-swc)
- Styling: Tailwind CSS 4
- Router: react-router-dom 7
- HTTP client: axios
- Validation: valibot
- Linting/formatting: ESLint + typescript-eslint, Prettier
- Deployment config: Vercel (vercel.json SPA rewrites)

## Requirements
- Node.js 18+ (required by Vite 6)
- npm (package-lock.json present)

## Getting started
1. Clone and install dependencies
   - npm install
2. Configure environment variables (see Environment variables below)
3. Start the dev server
   - npm run dev
4. Build for production
   - npm run build
5. Preview the production build locally
   - npm run preview

## Scripts
- npm run dev — Start Vite dev server with HMR
- npm run build — Type-check (tsc -b) and build with Vite
- npm run preview — Preview the production build locally
- npm run lint — Run ESLint

## Environment variables
This project uses Vite env vars (must be prefixed with VITE_):

- VITE_API_URL — Base URL of the backend API.
  - Example (development): http://localhost:5000
  - Local override file example: create .env.local with VITE_API_URL=http://localhost:5000

Env files are not committed. See .env.local in this repo as an example of the required variable in development.

## Entry points and routing
- HTML entry: index.html (mounts #root and loads src/main.tsx)
- App entry: src/main.tsx (creates root and mounts RouterProvider)
- Router: src/router.tsx with routes for:
  - / — Product list (loader fetches products; action toggles availability)
  - /productos/nuevo — Create product (action posts new product)
  - /productos/:id/editar — Edit product (loader fetches product; action updates)
  - /productos/:id/eliminar — Delete product (action deletes)

## API service
- src/services/productService.ts uses axios and VITE_API_URL to call the REST API under /api/products

## Project structure (selected)
- index.html — App HTML shell
- src/
  - main.tsx — App bootstrap
  - router.tsx — Route configuration
  - index.css — Global styles (Tailwind CSS)
  - layouts/
    - Layout.tsx — App layout and header
  - components/
    - ProductForm.tsx, ProductDetails.tsx, ErrorMessage.tsx
  - views/
    - Products.tsx, NewProduct.tsx, EditProduct.tsx
  - services/
    - productService.ts — API calls
  - types/
    - index.ts — Valibot schemas and Product type
  - utils/ (if present) — Utility helpers (e.g., toBoolean)
- vite.config.ts — Vite configuration (React SWC + Tailwind CSS plugins)
- vercel.json — SPA routing for Vercel deploys
- eslint.config.js — ESLint configuration
- tsconfig*.json — TypeScript configs

## Development notes
- Tailwind CSS 4 is enabled via the @tailwindcss/vite plugin in vite.config.ts.
- React Router Data APIs (loader/action) are used for data fetching and mutations per route.
- All network requests derive their base from VITE_API_URL to avoid hardcoding.

## License
This project is licensed under the MIT License — see the LICENSE file for details.
