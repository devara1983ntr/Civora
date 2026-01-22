# Civora Rebranding & Customization Plan (Phase 2)

## 1. Objective
Transform the `enatega-multivendor-web` application into **Civora**, a discovery-first platform with a premium dark aesthetic. This plan outlines the steps to prepare the codebase for rebranding, terminology refactoring, and feature extension.

## 2. Brand Identity & Visual Strategy
**Goal:** Create a sophisticated, "Dark Mode" native feel using the provided palette.

### 2.1 Color Palette
These variables will replace the existing ones in `app/(localized)/global.css`:
- **Background:** `#0C0C0F` (Deep Black) - Replaces white/light backgrounds.
- **Primary Color:** Deep Indigo (Value TBD, e.g., `#4F46E5` or similar dark-friendly indigo).
- **Accent Color:** Emerald (Value TBD, e.g., `#10B981`) - For call-to-actions and highlights.
- **Text:** High contrast white/grey on black.

### 2.2 Terminology Refactoring (Domain Model)
Systematic replacement of terms in UI text (`locales/en.json`) and eventually code (where safe):
| Current Term | New Civora Term | Context |
| :--- | :--- | :--- |
| **Restaurant** | **Place** | General establishment (Cafe, School, etc.) |
| **Vendor** | **Business** | The entity managing the place |
| **Rider** | **Courier** | Delivery agent |
| **Store** | **Shop** / **Business** | Retail specific |
| **Enatega** | **Civora** | Brand Name |

### 2.3 Assets
- **Logo:** Replace `public/assets/images/logo.png` (and variants) with Civora branding.
- **Favicon:** Replace `public/favicon.ico`.
- **Manifest:** Update `public/manifest.json`.

## 3. Safe Modification Order
To minimize risk, changes will be applied in this specific order:

1.  **Preparation (Current Phase):** Audit and Planning.
2.  **Asset Replacement:** Swap images and icons.
3.  **Global Styling:** Update `global.css` variables and `tailwind.config.ts`.
4.  **UI Text Refactoring:** Bulk update `locales/en.json`.
5.  **Component Styling:** Tweak individual components (`lib/ui/useable-components`) that have hardcoded styles incompatible with the dark theme.
6.  **Layout Adjustments:** Modify `app/layout.tsx` and headers for the new "Discovery" focus.

## 4. UI Component Inventory & Modification Strategy
Most components are in `lib/ui/useable-components/`.

| Component Group | Key Components | Action |
| :--- | :--- | :--- |
| **Cards** | `Home-Card`, `Moveable-Card`, `TinyTile` | Apply dark background, shadow inversion. |
| **Navigation** | `Footer`, `Home-Buttons` | Update links, apply brand colors. |
| **Inputs** | `Home-search`, `text-field` | Ensure text contrast on dark background. |
| **Modals** | `reviews-modal`, `filter-modal` | Dark theme styling. |

## 5. Feature Extension Points
Future features (Phase 3+) will plug into these locations:

- **Search-First Browsing:**
  - *Location:* `lib/ui/useable-components/Home-search`
  - *Plan:* Expand to a global search bar with filters (Schools, Cafes, etc.) available on the landing page immediately.
- **Reviews & Ratings:**
  - *Location:* `reviews-modal`
  - *Plan:* Expose ratings on `Moveable-Card` without needing click-through.
- **Map-Based Discovery:**
  - *Location:* `app/(localized)/mapview`
  - *Plan:* Enhance `google-map-component` to show different pins for "Places" vs "Shops".

## 6. Risks & Constraints Report
- **Backend Coupling:** The app uses a hardcoded `ENV` constant pointing to `STAGE` APIs. We cannot modify the backend logic yet.
- **Hardcoded Styles:** Some components likely use hardcoded hex values (e.g., white backgrounds) in `styles.module.css` or inline styles, requiring manual hunting.
- **Mobile-First Design:** The current layout is heavily mobile-optimized (e.g., "Moveable-Card"). Adapting this to a premium desktop "Web" experience might require significant layout refactoring.
- **Serverless API:** The PRD mentions a `/api` serverless backend, but the current repo uses an external GraphQL API. This discrepancy means backend features might be limited until the backend source is available or mocked.

## 7. Next Immediate Steps
1.  Execute the **Asset Replacement**.
2.  Apply the **Color Palette** changes in a new branch.
3.  Run the **Terminology Refactor** on `en.json`.
