# 📘 Next.js

This repository defines a base structure for **Next.js** projects within the Fidooo ecosystem. It's designed to maximize scalability, maintainability, and development velocity.

## 📋 Table of Contents

- [Directory Structure](#-directory-structure)
- [Technologies and Rationale](#-technologies-and-rationale)
  - [UI State Management → Zustand](#-zustand)
  - [CSS Framework → Tailwind CSS](#-tailwind-css)
  - [Data Fetching → SWR](#-swr)
  - [Design System → Atomic Design](#-atomic-design)
  - [Schema Validation → Zod](#-zod)
  - [Internationalization → next-intl](#-next-intl)
  - [Component Documentation → Storybook](#-storybook)
  - [Unit Testing → Jest](#-jest)
  - [E2E Testing → Playwright](#-playwright)

---

## 📁 Directory Structure

```bash
src/
├── app/                         # Routes with App Router (Next.js 13+)
│   ├── (group)/                # Optional route groups
│   │   └── page.tsx
│   ├── dashboard/              # User dashboard (authenticated users)
│   │   ├── layout.tsx
│   │   ├── page.tsx            # User's personal dashboard
│   │   ├── profile/            # User profile management
│   │   │   └── page.tsx
│   │   ├── orders/             # User's order history
│   │   │   └── page.tsx
│   │   └── settings/           # User settings
│   │       └── page.tsx
│   ├── admin/                  # Admin panel (system administrators)
│   │   ├── layout.tsx
│   │   ├── page.tsx            # Admin dashboard overview
│   │   ├── users/              # User management
│   │   │   ├── page.tsx
│   │   │   └── [id]/
│   │   │       └── page.tsx
│   │   ├── products/           # Product management
│   │   │   ├── page.tsx
│   │   │   └── [id]/
│   │   │       └── page.tsx
│   │   ├── analytics/          # System analytics
│   │   │   └── page.tsx
│   │   └── settings/           # System settings
│   │       └── page.tsx
│   └── middleware.ts           # Authentication & edge functions
├── components/                 # Reusable components (atomic design)
│   ├── atoms/
│   │   ├── common/             # Universal basic components
│   │   │   ├── Button/
│   │   │   ├── Input/
│   │   │   ├── Text/
│   │   │   └── Icon/
│   │   ├── forms/              # Form-specific components
│   │   │   ├── Checkbox/
│   │   │   └── Select/
│   │   └── feedback/           # Feedback components
│   │       ├── Badge/
│   │       └── Alert/
│   ├── molecules/
│   │   ├── common/
│   │   │   ├── SearchBar/
│   │   │   └── Card/
│   │   └── forms/
│   │       ├── FormField/
│   │       └── FormGroup/
│   ├── organisms/
│   │   ├── layout/
│   │   │   ├── Header/
│   │   │   └── Footer/
│   │   └── content/
│   │       ├── ProductGrid/
│   │       └── UserProfile/
│   ├── templates/
│   │   ├── DashboardLayout/
│   │   └── AuthLayout/
│   └── index.ts
├── features/                   # Domain-specific logic
│   ├── auth/
│   │   ├── components/
│   │   ├── hooks/
│   │   ├── services/
│   │   └── types.ts
│   └── user/
│       ├── components/
│       ├── hooks/
│       ├── services/
│       └── types.ts
├── hooks/                      # Global hooks
├── lib/                        # External clients (e.g., Firebase, SWR config)
├── services/                   # API clients, middlewares
├── store/                      # Zustand store
│   ├── authStore.ts
│   ├── uiStore.ts
│   └── ...
├── utils/                      # Helpers and common functions
├── constants/                  # Global constants
├── validations/                # Zod schemas
├── styles/                     # Tailwind and global styles
│   ├── globals.css
│   └── tailwind.config.ts
├── i18n/                       # Internationalization
│   ├── en/
│   │   └── common.json
│   ├── es/
│   │   └── common.json
│   └── config.ts
├── public/                     # Static assets
├── tests/                      # Unit tests (Jest + RTL)
│   ├── components/             # Component tests
│   │   ├── atoms/
│   │   ├── molecules/
│   │   └── organisms/
│   ├── features/               # Feature tests
│   │   ├── auth/
│   │   └── user/
│   └── utils/                  # Utility tests
└── e2e/                        # E2E tests (Playwright)
    ├── auth.spec.ts            # Login/Register flows
    ├── dashboard.spec.ts       # User dashboard
    └── admin.spec.ts           # Admin panel
```

### Atomic Design

#### **Component Levels:**

1. **Atoms** - Basic building blocks
   - Button, Input, Icon, Text, Badge
   - No dependencies on other components
   - Highly reusable

2. **Molecules** - Simple combinations of atoms
   - SearchBar (Input + Button)
   - FormField (Label + Input + Error)
   - Card (Image + Text + Button)

3. **Organisms** - Complex sections
   - Header (Logo + Navigation + UserMenu)
   - ProductGrid (multiple ProductCard)
   - Footer (Links + Social + Newsletter)

4. **Templates** - Page layouts
   - DashboardLayout, AuthLayout
   - Define structure, not content

5. **Pages** - Specific template instances
   - HomePage, UserProfilePage

---

## 🧰 Technologies and Rationale

### ✅ Zustand

- Global state management without boilerplate or providers.
- Ideal for UI state, authentication, and feature flags.
- Alternatives: Redux Toolkit, Jotai.

### ✅ Tailwind CSS

- Utility-first CSS framework for rapid and consistent styling.
- Compatible with atomic design principles and Storybook.
- Alternatives: Styled Components, Chakra UI, Mantine.

### ✅ SWR

- Reactive data fetching with caching and revalidation.
- Ideal for REST APIs and real-time data.
- Alternatives: TanStack Query (React Query).

### ✅ Zod

- TypeScript-first schema validation.
- Native TypeScript compatibility with excellent DX.
- Alternatives: Yup, Joi, Valibot.

### ✅ next-intl

- Internationalization library for Next.js applications.
- Type-safe translations with excellent developer experience.
- Supports multiple locales and dynamic content.
- Alternatives: next-i18next, react-intl.

### ✅ Storybook

- Component documentation and visual testing platform.
- Enables isolated component development and testing.
- Integrates seamlessly with atomic design principles.
- Essential for design system maintenance and team collaboration.

### ✅ Playwright

- Modern end-to-end testing framework for web applications.
- **Perfect for Next.js + Firebase** - tests real authentication and database operations.
- Cross-browser testing with excellent debugging capabilities.
- **Simpler setup** than Cypress for Firebase integration.
- Fast execution and reliable test automation.
- Alternatives: Cypress, Selenium.

### ✅ Jest

- JavaScript testing framework for unit and integration tests.
- **Industry standard** with excellent Next.js integration.
- Fast execution with built-in mocking capabilities.
- **Perfect for component testing** with React Testing Library.
- Simple configuration and extensive ecosystem.
- Alternatives: Vitest, Mocha.

---

This setup enables Fidooo to have a solid, modular, and scalable foundation for various web products. Technology decisions can be adjusted based on specific requirements, but this base covers over 90% of modern frontend application needs.

