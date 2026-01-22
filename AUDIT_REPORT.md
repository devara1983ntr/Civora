# Repository Audit & Customer Web Analysis

## 1. Repository Structure
The repository `food-delivery-multivendor` contains the following major components:
- **`enatega-multivendor-web`**: Customer Web Application (Next.js) - **Primary Focus**.
- **`enatega-multivendor-admin`**: Admin Dashboard.
- **`enatega-multivendor-app`**: Customer Mobile App.
- **`enatega-multivendor-rider`**: Rider App.
- **`enatega-multivendor-store`**: Store/Vendor App.

## 2. Customer Web Application Analysis
**Location:** `food-delivery-multivendor/enatega-multivendor-web/`

### Tech Stack
- **Framework:** Next.js 14 (App Router)
- **Language:** TypeScript
- **Styling:** Tailwind CSS, PrimeReact, CSS Variables
- **State/API:** Apollo Client (GraphQL), Context API
- **Maps:** Google Maps API

### Architecture
- **Entry Point:** `app/layout.tsx` (Root Layout)
- **Routing:** File-system based routing under `app/(localized)/`.
  - Main Pages: `(home)`, `(restaurant-store)`, `order`, `profile`, `mapview`.
- **Internationalization:** Implemented using `next-intl` and `(localized)` route groups.

### Styling & Theming
- **Global Styles:** `app/(localized)/global.css`
- **Theme Configuration:**
  - CSS Variables in `global.css` (`:root`) define core colors (`--primary-color`, etc.).
  - `tailwind.config.ts` maps these variables to Tailwind classes.
- **Component Library:** PrimeReact (theme: `lara-light-blue` imported in global css).

### Branding Touchpoints
To rebrand the application, modifications are needed in:
1.  **App Name:**
    - Defined as `APP_NAME` in `lib/utils/constants/global.ts`.
2.  **Colors:**
    - Primary and Secondary colors defined in `app/(localized)/global.css`.
3.  **Logos:**
    - Located in `public/assets/images/` (needs visual verification of specific files).
    - Referenced in `lib/utils/constants/global.ts` (`LOGO_URL`).
4.  **Icons:**
    - `public/favicon.ico` and manifest files.

## 3. Backend & Environment Configuration
- **API URLs:**
  - Hardcoded in `environment.ts` for `DEV`, `STAGE`, and `PROD`.
  - Currently, the app is forced to `STAGE` via the `ENV` constant in `lib/utils/constants/global.ts`.
  - `lib/hooks/useSetApollo.tsx` attempts to use `process.env.NEXT_PUBLIC_SERVER_URL`, but `ConfigurationContext` relies on `environment.ts`.
- **Constraint:** The backend is proprietary. We must ensure the web app points to a valid environment (likely the `STAGE` one provided) or a mocked equivalent if provided later.

## 4. Compatibility
- The application is a standard web application.
- No native-mobile dependencies (e.g., React Native) were found in the web project `package.json`.
- Fully compatible with modern browsers.

## 5. Recommendations for Phase 2
1.  **Environment Setup:** Create a `.env.local` file to override hardcoded values if possible, or modify `lib/utils/constants/global.ts` to switch environments.
2.  **Rebranding:**
    - Start by updating CSS variables in `app/(localized)/global.css`.
    - Replace logo assets in `public/assets/images/`.
    - Update `APP_NAME` in constants.
3.  **Feature Customization:** Use the `app/` directory structure to add new routes or modify existing layouts.
