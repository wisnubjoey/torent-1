# Laravel React Starter Kit - Qwen Context

## Project Overview

This is a Laravel React Starter Kit application that combines the power of Laravel for the backend with React for the frontend, using Inertia.js as the bridge between them. The project uses TypeScript for type safety and Tailwind CSS for styling, with a modern component architecture.

**Key Technologies:**
- Backend: Laravel 12.x (PHP 8.2+)
- Frontend: React 19+, TypeScript, Inertia.js
- Styling: Tailwind CSS, Radix UI, Headless UI
- Build Tools: Vite, Laravel Vite Plugin
- Package Management: Composer (PHP), npm (JS)

## Architecture

The application follows a modern full-stack architecture:
- **Backend**: Laravel framework handling API endpoints, authentication, and business logic
- **Frontend**: React components managed by Inertia.js for server-side rendering and client-side interactions
- **Integration**: Inertia.js connects Laravel backend with React frontend without a traditional API
- **UI Components**: Radix UI primitives and custom components with Tailwind styling
- **Authentication**: Laravel Fortify for authentication flows

## Project Structure

```
torent-1/
├── app/                    # Laravel application code
│   ├── Http/Controllers/   # Request controllers
│   ├── Models/            # Eloquent models
│   └── Providers/         # Service providers
├── resources/             # Frontend assets
│   ├── css/              # Stylesheets
│   └── js/               # JavaScript/TypeScript source
│       ├── components/   # React components
│       ├── hooks/        # React hooks
│       ├── layouts/      # Layout components
│       └── pages/        # Page components
├── routes/               # Route definitions
├── composer.json         # PHP dependencies
├── package.json          # JavaScript dependencies
└── vite.config.ts        # Vite build configuration
```

## Building and Running

### Initial Setup
```bash
# Install dependencies
composer install
npm install

# Set up environment
cp .env.example .env
php artisan key:generate

# Set up database (uses SQLite by default)
touch database/database.sqlite

# Run migrations
php artisan migrate

# Build assets
npm run build
```

### Development Commands
```bash
# Start development server with hot reloading
npm run dev

# Alternative: Use composer dev script for full stack
composer run dev

# For SSR (Server-Side Rendering)
composer run dev:ssr

# Build for production
npm run build

# Type checking
npm run types

# Linting
npm run lint

# Formatting
npm run format
```

### Testing
```bash
# Run PHP tests
composer run test
# or
php artisan test

# Run frontend type checking
npm run types
```

## Key Features

1. **Authentication System**:
   - Login, registration, password reset
   - Email verification
   - Two-factor authentication
   - Password confirmation

2. **Settings Management**:
   - Profile updates
   - Password changes
   - Two-factor authentication setup
   - Appearance/theme settings

3. **UI Components**:
   - Reusable component library using Radix UI primitives
   - Responsive sidebar navigation
   - Form components with validation
   - Modal dialogs and alerts

4. **Theming**:
   - Light/dark mode support
   - Theme persistence using localStorage/cookies
   - CSS variables for theming

## Important Files and Configurations

- `app/Http/Middleware/HandleInertiaRequests.php` - Shares data with frontend components
- `resources/js/app.tsx` - Main React application entry point
- `vite.config.ts` - Vite configuration for asset building
- `composer.json` - PHP dependency management and scripts
- `package.json` - JavaScript dependency management and scripts
- `routes/web.php` - Main web routes
- `app/Providers/FortifyServiceProvider.php` - Authentication service configuration

## Development Conventions

1. **Frontend Components**:
   - Located in `resources/js/components/`
   - Use TypeScript with proper typing
   - Follow React best practices
   - Use Tailwind for styling

2. **Pages**:
   - Located in `resources/js/pages/`
   - Mapped to Laravel routes via Inertia
   - Use layout components for consistent structure

3. **Routing**:
   - Backend routes in `routes/` directory
   - Frontend pages automatically resolved by Inertia

4. **Styling**:
   - Tailwind CSS utility classes
   - Custom components in `resources/js/components/ui/`
   - Consistent design system using Radix UI primitives

5. **Type Safety**:
   - Strict TypeScript configuration
   - Type checking enforced in CI/CD pipeline
   - Proper typing for props and API responses

## Common Tasks

- **Creating a new page**: Add a new file in `resources/js/pages/` and define a route in `routes/`
- **Adding a new component**: Create in `resources/js/components/` following existing patterns
- **Sharing data with frontend**: Use the `share()` method in `HandleInertiaRequests` middleware
- **Adding environment variables**: Update `.env` and `.env.example` files