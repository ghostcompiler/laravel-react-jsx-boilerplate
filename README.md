<p align="center">
  <img src="https://res.cloudinary.com/djgvfl1tv/image/upload/v1780666791/logo_mqnqn4.png" alt="Ghost Compiler Logo" width="180">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Laravel-13-FF2D20?style=for-the-badge&logo=laravel&logoColor=white" alt="Laravel">
  <img src="https://img.shields.io/badge/React-19-61DAFB?style=for-the-badge&logo=react&logoColor=000000" alt="React">
  <img src="https://img.shields.io/badge/Inertia.js-3-9553E9?style=for-the-badge" alt="Inertia.js">
  <img src="https://img.shields.io/badge/Vite-8-646CFF?style=for-the-badge&logo=vite&logoColor=white" alt="Vite">
  <img src="https://img.shields.io/badge/Tailwind-4-38B2AC?style=for-the-badge&logo=tailwindcss&logoColor=white" alt="Tailwind CSS">
  <img src="https://img.shields.io/badge/Built%20By-Ghost%20Compiler-0F172A?style=for-the-badge" alt="Ghost Compiler">
</p>

# Laravel React JSX Boilerplate

A blank, production-ready **boilerplate** for building modern Laravel apps with **React and JSX** — not TypeScript.

Laravel’s official starter kits ship with React + TSX. This boilerplate gives you the same modern stack (Inertia, Vite, Tailwind, Wayfinder) in plain **JavaScript/JSX**, so you can move fast without TypeScript tooling if that is not your preference.

---

## What is in this project

### Backend

| Piece | Details |
|-------|---------|
| **Laravel 13** | Latest framework with streamlined routing, middleware, and config |
| **Inertia Laravel** | Server-driven SPA responses — no separate API layer required for page loads |
| **Wayfinder** | Type-safe route and action helpers generated from your Laravel routes |
| **SQLite by default** | Ready for local dev; swap to MySQL/PostgreSQL in `.env` |
| **Queue & jobs tables** | Migrations included for background work when you need it |
| **PHPUnit** | Feature and unit test scaffolding |

### Frontend

| Piece | Details |
|-------|---------|
| **React 19 + JSX** | Components in `.jsx` — no `.tsx` required |
| **Inertia React** | Page navigation without full client-side routing setup |
| **Vite 8** | Fast HMR in dev, optimized builds for production |
| **Tailwind CSS 4** | Utility-first styling via the Vite plugin |
| **React Compiler** | Enabled through Babel for optimized React rendering |
| **Instrument Sans** | Loaded via Laravel Vite font plugin (Bunny Fonts) |

### App features (included out of the box)

- **Welcome page** — Laravel-style landing page at `/`, built as an Inertia React page
- **Dark / light / system theme** — `use-appearance` hook + cookie-backed preference, no flash on load
- **Shared Inertia props** — App name, auth user, and layout state wired in `HandleInertiaRequests`
- **Single root Blade view** — `resources/views/app.blade.php` mounts the React app
- **Wayfinder-generated helpers** — Route/action modules under `resources/js/routes` and `resources/js/actions`

### Developer experience

- **`composer dev`** — Runs PHP server, queue worker, log tail (Pail), and Vite together
- **`composer setup`** — One-shot install: Composer, `.env`, key, migrations, npm, build
- **Linting & formatting** — Laravel Pint (PHP), ESLint + Prettier (JS/JSX)
- **GitHub Actions** — CI tests (PHP 8.3–8.5) and quality checks on push/PR

---

## Project structure

```
app/
  Http/Middleware/
    HandleAppearance.php      # Theme cookie → Blade
    HandleInertiaRequests.php # Shared Inertia props
resources/
  js/
    app.jsx                   # Inertia bootstrapping
    pages/welcome.jsx         # Example page
    hooks/use-appearance.js   # Theme toggle logic
    routes/                   # Wayfinder-generated routes
    actions/                  # Wayfinder-generated actions
  css/app.css                 # Tailwind entry
  views/app.blade.php         # Root HTML shell
routes/web.php                # Route::inertia('/', 'welcome')
tests/                        # PHPUnit feature & unit tests
.github/workflows/            # tests.yml + lint.yml
```

---

## Requirements

- PHP **8.3+**
- Composer **2.x**
- Node.js **22+** (recommended)

---

## Getting started

### Create a new project

**Option A — Laravel installer**

```bash
laravel new my-app --using=ghostcompiler/laravel-react-jsx-boilerplate.git
cd my-app
composer install && npm install
composer run dev
```

**Option B — Composer**

```bash
composer create-project ghostcompiler/laravel-react-jsx-boilerplate.git my-app
cd my-app
composer install && npm install
composer run dev
```

**Option C — Clone the repository**

```bash
git clone https://github.com/ghostcompiler/laravel-react-jsx-boilerplate.git
cd laravel-react-jsx-boilerplate
composer install && npm install
composer run dev
```

### Start development

```bash
composer run dev
```

Visit [http://localhost:8000](http://localhost:8000).

### Manual setup (alternative)

If you skipped `composer setup`, run:

```bash
composer install
cp .env.example .env
php artisan key:generate
php artisan migrate
npm install
npm run build
```

For local development with HMR:

```bash
npm run dev
```

In a second terminal:

```bash
php artisan serve
```

---

## Scripts

### Composer

| Command | Description |
|---------|-------------|
| `composer setup` | Full project bootstrap |
| `composer dev` | Server + queue + logs + Vite |
| `composer test` | Pint check + PHPUnit |
| `composer lint` | Fix PHP style with Pint |
| `composer lint:check` | Check PHP style (CI mode) |

### npm

| Command | Description |
|---------|-------------|
| `npm run dev` | Vite dev server with HMR |
| `npm run build` | Production asset build |
| `npm run lint` | ESLint on `resources/js` |
| `npm run lint:fix` | ESLint with auto-fix |
| `npm run format` | Prettier check |
| `npm run format:fix` | Prettier write |

---

## Adding a new page

1. Create a React page, e.g. `resources/js/pages/dashboard.jsx`
2. Register a route in `routes/web.php`:

```php
Route::inertia('/dashboard', 'dashboard')->name('dashboard');
```

3. Use Wayfinder helpers (regenerated on build) for type-safe links from JSX

---

## What you can build from this

This is intentionally **minimal** — a blank boilerplate, not a full auth dashboard or starter kit. That makes it a strong base for:

| Use case | How this boilerplate helps |
|----------|-------------------|
| **SaaS dashboards** | Add auth (Fortify/Breeze), layouts, and Inertia pages on top of the existing middleware stack |
| **Internal tools** | Laravel for data, permissions, and queues; React for interactive UI without a separate SPA repo |
| **CRUD admin panels** | Models, migrations, controllers, and Inertia forms — Wayfinder keeps routes in sync |
| **Marketing sites + app** | Blade or Inertia landing pages, shared Tailwind theme, dark mode already wired |
| **API-backed products** | Start Inertia-first; add API routes later if mobile or third-party clients are needed |
| **Learning Laravel + React** | Official Laravel docs apply; frontend examples use JSX instead of TSX |

Typical next steps:

- Add **authentication** (Laravel Fortify or Breeze adapted for JSX)
- Create a **layout component** and shared navigation
- Add **form components** with Inertia `useForm`
- Connect **Eloquent models** and policies for your domain
- Enable **queues** for emails, imports, or webhooks (tables already migrated)

---

## CI / quality

GitHub Actions run on pushes and pull requests to `main`, `master`, `develop`, and `workos`:

- **tests.yml** — PHPUnit across PHP 8.3, 8.4, and 8.5
- **lint.yml** — Pint, Prettier, and ESLint

Run the same checks locally:

```bash
composer lint:check
npm run format
npm run lint
./vendor/bin/phpunit
```

Or simulate CI with [act](https://github.com/nektos/act):

```bash
act -j ci -W .github/workflows/tests.yml
act -j quality -W .github/workflows/lint.yml
```

---

## Repository

https://github.com/ghostcompiler/laravel-react-jsx-boilerplate

---

## Development Environment

Built using **ServBay**

<p align="left">
  <img src="https://res.cloudinary.com/djgvfl1tv/image/upload/v1780667063/servbay_edc7jz.png" alt="ServBay" width="120">
</p>

- Mac M4 Tested
- macOS Apple Silicon
- Powered by ServBay

---

## Repository

https://github.com/ghostcompiler/laravel-react-jsx-boilerplate

---

## License

MIT License

---
