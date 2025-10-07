# Quickstart Guide for Vehicle Rental Web Application

## Prerequisites
- PHP 8.2+
- Composer
- Node.js 18+
- npm or yarn
- PostgreSQL

## Setup Instructions

### 1. Clone and Install Dependencies
```bash
git clone <repository-url>
cd vehicle-rental-app
composer install
npm install
```

### 2. Environment Configuration
```bash
cp .env.example .env
php artisan key:generate
```

Update the `.env` file with your database and WhatsApp API credentials:
```
DB_CONNECTION=pgsql
DB_HOST=127.0.0.1
DB_PORT=5432
DB_DATABASE=vehicle_rental
DB_USERNAME=your_username
DB_PASSWORD=your_password

WHATSAPP_API_TOKEN=your_whatsapp_token
WHATSAPP_BUSINESS_ID=your_business_id
```

### 3. Database Setup
```bash
# Create database
createdb vehicle_rental

# Run migrations
php artisan migrate

# Seed initial data (optional)
php artisan db:seed
```

### 4. Build Assets
```bash
npm run build
# or for development with hot reload
npm run dev
```

### 5. Start the Application
```bash
php artisan serve
```

## User Flow Validation

### Scenario 1: Customer Rents a Vehicle
1. Navigate to the vehicle rental website
2. Browse available vehicles (motorcycles and cars) with badges (Luxury, Sport, City, Touring)
3. Select a rental duration (days, weeks, months)
4. Optionally choose a package for discounts or additional features
5. Register or authenticate with phone number verification
6. Complete the rental process
7. Rental order is automatically sent to staff via WhatsApp

### Scenario 2: Admin Manages Vehicles
1. Access the admin dashboard
2. Use the calendar to view vehicle availability
3. Add new vehicles to the rental inventory
4. Monitor rental orders and history

## API Endpoints

### Authentication
- `POST /api/auth/register` - Register new user
- `POST /api/auth/login` - Login user

### Vehicles
- `GET /api/vehicles` - Get all available vehicles
- `GET /api/vehicles/{id}` - Get vehicle details

### Packages
- `GET /api/packages` - Get all available packages

### Rentals
- `POST /api/rentals/check-availability` - Check vehicle availability
- `POST /api/rentals` - Create a new rental order
- `GET /api/rentals/my-rentals` - Get user's rental history

### Admin
- `GET /api/admin/vehicles` - Get all vehicles (admin)
- `POST /api/admin/vehicles` - Add a new vehicle (admin)
- `GET /api/admin/rentals` - Get all rental orders (admin)
- `GET /api/admin/calendar` - Get vehicle availability calendar (admin)

## Testing the Application
```bash
# Run backend tests
composer test

# Run frontend type checking
npm run types

# Run frontend linting
npm run lint
```