# Data Model for Vehicle Rental Web Application

## User Entity
- **Fields**:
  - id (UUID/Integer, Primary Key)
  - name (String, required)
  - phone (String, required, unique, verified)
  - email (String, nullable)
  - role (Enum: 'user', 'admin', default: 'user')
  - phone_verified_at (DateTime, nullable)
  - created_at (DateTime)
  - updated_at (DateTime)
- **Validations**:
  - Phone number must be unique and properly formatted
  - Name is required
  - Role must be either 'user' or 'admin'
- **Relationships**:
  - Has many: rental_orders
  - Has many: user_rentals (active rentals)

## Vehicle Entity
- **Fields**:
  - id (UUID/Integer, Primary Key)
  - name (String, required)
  - type (Enum: 'motorcycle', 'car', required)
  - badge (Enum: 'luxury', 'sport', 'city', 'touring', or custom string, required)
  - description (Text, optional)
  - daily_rate (Decimal, required, positive)
  - weekly_rate (Decimal, optional, positive)
  - monthly_rate (Decimal, optional, positive)
  - is_available (Boolean, default: true)
  - vehicle_category_id (Integer, Foreign Key)
  - created_at (DateTime)
  - updated_at (DateTime)
- **Validations**:
  - Name is required
  - Type must be 'motorcycle' or 'car'
  - Badge must be one of the predefined values or custom string
  - Rates must be positive
  - Vehicle category must exist
- **Relationships**:
  - Belongs to: vehicle_category
  - Has many: rental_orders
  - Has many: rental_calendars (through rental orders)

## VehicleCategory Entity
- **Fields**:
  - id (UUID/Integer, Primary Key)
  - name (String, required)
  - description (Text, optional)
  - created_at (DateTime)
  - updated_at (DateTime)
- **Validations**:
  - Name is required and unique
- **Relationships**:
  - Has many: vehicles

## VehicleBadge Entity
- **Fields**:
  - id (UUID/Integer, Primary Key)
  - name (String, required)
  - description (Text, optional)
  - created_at (DateTime)
  - updated_at (DateTime)
- **Validations**:
  - Name is required and unique
- **Relationships**:
  - Many to many: vehicles

## Package Entity
- **Fields**:
  - id (UUID/Integer, Primary Key)
  - name (String, required)
  - description (Text, optional)
  - discount_percentage (Decimal, nullable)
  - additional_features (JSON, nullable)
  - is_active (Boolean, default: true)
  - created_at (DateTime)
  - updated_at (DateTime)
- **Validations**:
  - Name is required
  - Discount percentage must be between 0 and 100 if provided
- **Relationships**:
  - Has many: rental_orders

## RentalOrder Entity
- **Fields**:
  - id (UUID/Integer, Primary Key)
  - user_id (Integer, Foreign Key, required)
  - vehicle_id (Integer, Foreign Key, required)
  - package_id (Integer, Foreign Key, nullable)
  - start_date (Date, required)
  - end_date (Date, required)
  - total_amount (Decimal, required)
  - rental_period_type (Enum: 'day', 'week', 'month', required)
  - status (Enum: 'pending', 'confirmed', 'active', 'completed', 'cancelled', default: 'pending')
  - whatsapp_sent (Boolean, default: false)
  - created_at (DateTime)
  - updated_at (DateTime)
- **Validations**:
  - User must exist
  - Vehicle must exist
  - Start date must be before end date
  - Rental period type must be valid
  - Total amount must be positive
  - Status must be one of the allowed values
- **Relationships**:
  - Belongs to: user
  - Belongs to: vehicle
  - Belongs to: package
  - Has many: rental_histories

## RentalCalendar Entity
- **Fields**:
  - id (UUID/Integer, Primary Key)
  - vehicle_id (Integer, Foreign Key, required)
  - rental_order_id (Integer, Foreign Key, required)
  - start_date (Date, required)
  - end_date (Date, required)
  - status (Enum: 'booked', 'available', 'maintenance', default: 'booked')
  - created_at (DateTime)
  - updated_at (DateTime)
- **Validations**:
  - Vehicle must exist
  - Rental order must exist
  - Start date must be before end date
- **Relationships**:
  - Belongs to: vehicle
  - Belongs to: rental_order

## State Transitions
- RentalOrder status transitions:
  - pending → confirmed (when admin confirms)
  - confirmed → active (when rental period starts)
  - active → completed (when rental period ends)
  - pending/confirmed → cancelled (when user/admin cancels)
  - active → cancelled (in case of early return)