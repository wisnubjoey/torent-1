# Tasks: Vehicle Rental Web Application

**Input**: Design documents from `/specs/001-i-would-like/`
**Prerequisites**: plan.md (required), research.md, data-model.md, contracts/

## Execution Flow (main)
```
1. Load plan.md from feature directory
   → If not found: ERROR "No implementation plan found"
   → Extract: tech stack, libraries, structure
2. Load optional design documents:
   → data-model.md: Extract entities → model tasks
   → contracts/: Each file → contract test task
   → research.md: Extract decisions → setup tasks
3. Generate tasks by category:
   → Setup: project init, dependencies, linting
   → Tests: contract tests, integration tests
   → Core: models, services, CLI commands
   → Integration: DB, middleware, logging
   → Polish: unit tests, performance, docs
4. Apply task rules:
   → Different files = mark [P] for parallel
   → Same file = sequential (no [P])
   → Tests before implementation (TDD)
5. Number tasks sequentially (T001, T002...)
6. Generate dependency graph
7. Create parallel execution examples
8. Validate task completeness:
   → All contracts have tests?
   → All entities have models?
   → All endpoints implemented?
9. Return: SUCCESS (tasks ready for execution)
```

## Format: `[ID] [P?] Description`
- **[P]**: Can run in parallel (different files, no dependencies)
- Include exact file paths in descriptions

## Path Conventions
- **Web app structure**: Backend files in `app/`, `database/`, `routes/`, `tests/`, Frontend files in `resources/js/`
- Following Laravel React Starter Kit architecture with Inertia 2, Shadcn UI, and React 19

## Phase 3.1: Setup
- [ ] T001 Update .env to include PostgreSQL and WhatsApp API configurations in .env
- [ ] T002 [P] Create database migrations for User, Vehicle, VehicleCategory, VehicleBadge, Package, RentalOrder, and RentalCalendar in database/migrations/
- [ ] T003 [P] Install WhatsApp Business API client library (composer require for PHP backend)

## Phase 3.2: Tests First (TDD) ⚠️ MUST COMPLETE BEFORE 3.3
**CRITICAL: These tests MUST be written and MUST FAIL before ANY implementation**
- [ ] T004 [P] Contract test POST /api/auth/register in tests/Feature/Auth/RegisterTest.php
- [ ] T005 [P] Contract test POST /api/auth/login in tests/Feature/Auth/LoginTest.php
- [ ] T006 [P] Contract test GET /api/vehicles in tests/Feature/Vehicle/IndexTest.php
- [ ] T007 [P] Contract test GET /api/vehicles/{id} in tests/Feature/Vehicle/ShowTest.php
- [ ] T008 [P] Contract test GET /api/packages in tests/Feature/Package/IndexTest.php
- [ ] T009 [P] Contract test POST /api/rentals/check-availability in tests/Feature/Rental/CheckAvailabilityTest.php
- [ ] T010 [P] Contract test POST /api/rentals in tests/Feature/Rental/StoreTest.php
- [ ] T011 [P] Contract test GET /api/rentals/my-rentals in tests/Feature/Rental/IndexUserTest.php
- [ ] T012 [P] Contract test GET /api/admin/vehicles in tests/Feature/Admin/Vehicle/IndexTest.php
- [ ] T013 [P] Contract test POST /api/admin/vehicles in tests/Feature/Admin/Vehicle/StoreTest.php
- [ ] T014 [P] Contract test GET /api/admin/rentals in tests/Feature/Admin/Rental/IndexTest.php
- [ ] T015 [P] Contract test GET /api/admin/calendar in tests/Feature/Admin/Calendar/IndexTest.php
- [ ] T016 [P] Integration test user registration and verification flow in tests/Integration/UserRegistrationTest.php
- [ ] T017 [P] Integration test vehicle rental process in tests/Integration/VehicleRentalTest.php
- [ ] T018 [P] Integration test WhatsApp notification for new rentals in tests/Integration/WhatsAppNotificationTest.php

## Phase 3.3: Core Implementation (ONLY after tests are failing)
- [ ] T019 [P] User model in app/Models/User.php
- [ ] T020 [P] Vehicle model in app/Models/Vehicle.php
- [ ] T021 [P] VehicleCategory model in app/Models/VehicleCategory.php
- [ ] T022 [P] VehicleBadge model in app/Models/VehicleBadge.php
- [ ] T023 [P] Package model in app/Models/Package.php
- [ ] T024 [P] RentalOrder model in app/Models/RentalOrder.php
- [ ] T025 [P] RentalCalendar model in app/Models/RentalCalendar.php
- [ ] T026 [P] User factory in database/factories/UserFactory.php
- [ ] T027 [P] Vehicle factory in database/factories/VehicleFactory.php
- [ ] T028 [P] RentalOrder factory in database/factories/RentalOrderFactory.php
- [ ] T029 [P] Package factory in database/factories/PackageFactory.php
- [ ] T030 [P] Create/UpdateUserRequest in app/Http/Requests/User/CreateUpdateUserRequest.php
- [ ] T031 [P] CreateVehicleRequest in app/Http/Requests/Vehicle/CreateVehicleRequest.php
- [ ] T032 [P] CheckAvailabilityRequest in app/Http/Requests/Rental/CheckAvailabilityRequest.php
- [ ] T033 [P] CreateRentalOrderRequest in app/Http/Requests/Rental/CreateRentalOrderRequest.php
- [ ] T034 [P] User resource in app/Http/Resources/UserResource.php
- [ ] T035 [P] Vehicle resource in app/Http/Resources/VehicleResource.php
- [ ] T036 [P] Package resource in app/Http/Resources/PackageResource.php
- [ ] T037 [P] RentalOrder resource in app/Http/Resources/RentalOrderResource.php
- [ ] T038 [P] CalendarItem resource in app/Http/Resources/CalendarItemResource.php
- [ ] T039 [P] UserVehicleRental resource in app/Http/Resources/UserVehicleRentalResource.php
- [ ] T040 [P] AdminRentalOrder resource in app/Http/Resources/AdminRentalOrderResource.php
- [ ] T041 [P] Phone verification service in app/Services/PhoneVerificationService.php
- [ ] T042 [P] WhatsApp notification service in app/Services/WhatsAppNotificationService.php
- [ ] T043 [P] Vehicle availability check service in app/Services/VehicleAvailabilityService.php
- [ ] T044 [P] Rental pricing calculation service in app/Services/RentalPricingService.php
- [ ] T045 [P] User registration controller in app/Http/Controllers/Auth/RegisterController.php
- [ ] T046 [P] User login controller in app/Http/Controllers/Auth/LoginController.php
- [ ] T047 [P] Vehicle controller in app/Http/Controllers/VehicleController.php
- [ ] T048 [P] Package controller in app/Http/Controllers/PackageController.php
- [ ] T049 [P] Rental controller in app/Http/Controllers/RentalController.php
- [ ] T050 [P] Admin vehicle controller in app/Http/Controllers/Admin/VehicleController.php
- [ ] T051 [P] Admin rental controller in app/Http/Controllers/Admin/RentalController.php
- [ ] T052 [P] Admin calendar controller in app/Http/Controllers/Admin/CalendarController.php
- [ ] T053 [P] Vehicle availability policy in app/Policies/VehiclePolicy.php
- [ ] T054 [P] Rental order policy in app/Policies/RentalOrderPolicy.php
- [ ] T055 [P] Admin policy in app/Policies/AdminPolicy.php
- [ ] T056 POST /api/auth/register endpoint implementation
- [ ] T057 POST /api/auth/login endpoint implementation
- [ ] T058 GET /api/vehicles endpoint implementation
- [ ] T059 GET /api/vehicles/{id} endpoint implementation
- [ ] T060 GET /api/packages endpoint implementation
- [ ] T061 POST /api/rentals/check-availability endpoint implementation
- [ ] T062 POST /api/rentals endpoint implementation
- [ ] T063 GET /api/rentals/my-rentals endpoint implementation
- [ ] T064 GET /api/admin/vehicles endpoint implementation
- [ ] T065 POST /api/admin/vehicles endpoint implementation
- [ ] T066 GET /api/admin/rentals endpoint implementation
- [ ] T067 GET /api/admin/calendar endpoint implementation
- [ ] T068 Input validation for all endpoints
- [ ] T069 Error handling and logging for all endpoints

## Phase 3.4: Integration
- [ ] T070 Connect models to PostgreSQL database
- [ ] T071 Auth middleware for protected routes
- [ ] T072 Role-based access control middleware
- [ ] T073 Request/response logging
- [ ] T074 CORS and security headers
- [ ] T075 WhatsApp notification integration in rental creation flow

## Phase 3.5: Frontend Implementation
- [ ] T076 [P] Create base layout components for user and admin in resources/js/layouts/
- [ ] T077 [P] Create vehicle listing component in resources/js/components/vehicle/
- [ ] T078 [P] Create vehicle detail component in resources/js/components/vehicle/
- [ ] T079 [P] Create rental form component in resources/js/components/rental/
- [ ] T080 [P] Create package selection component in resources/js/components/package/
- [ ] T081 [P] Create user dashboard component in resources/js/pages/user/
- [ ] T082 [P] Create admin dashboard component in resources/js/pages/admin/
- [ ] T083 [P] Create vehicle calendar component for admin in resources/js/components/admin/
- [ ] T084 [P] Create vehicle management component for admin in resources/js/components/admin/
- [ ] T085 [P] Create rental management component for admin in resources/js/components/admin/
- [ ] T086 [P] Create authentication pages in resources/js/pages/auth/
- [ ] T087 [P] Create custom hooks for API calls in resources/js/hooks/
- [ ] T088 [P] Create Shadcn UI components for the application in resources/js/components/ui/
- [ ] T089 Integrate backend API endpoints with Inertia.js
- [ ] T090 Implement phone verification flow in frontend
- [ ] T091 Implement responsive design with Tailwind CSS

## Phase 3.6: Polish
- [ ] T092 [P] Unit tests for services in tests/Unit/
- [ ] T093 [P] Unit tests for validation in tests/Unit/
- [ ] T094 Performance tests (<200ms for API endpoints)
- [ ] T095 [P] Update documentation files
- [ ] T096 Remove duplication in code
- [ ] T097 Run manual-testing.md scenarios
- [ ] T098 Update README with vehicle rental feature details

## Dependencies
- Tests (T004-T018) before implementation (T019-T069)
- T019 (User model) blocks T024 (RentalOrder model)
- T020 (Vehicle model) blocks T024 (RentalOrder model)
- T023 (Package model) blocks T024 (RentalOrder model)
- T024 (RentalOrder model) blocks T042 (WhatsApp notification service)
- T041 (Phone verification service) blocks T045 (Registration controller)
- T042 (WhatsApp service) blocks T049 (Rental controller)
- T043 (Availability service) blocks T049 (Rental controller)
- T044 (Pricing service) blocks T049 (Rental controller)
- Implementation (T019-T069) before frontend (T076-T091)
- Backend API (T056-T067) before frontend integration (T089)
- Frontend before polish (T092-T098)

## Parallel Example
```
# Launch T004-T015 (contract tests) together:
Task: "Contract test POST /api/auth/register in tests/Feature/Auth/RegisterTest.php"
Task: "Contract test POST /api/auth/login in tests/Feature/Auth/LoginTest.php"
Task: "Contract test GET /api/vehicles in tests/Feature/Vehicle/IndexTest.php"
Task: "Contract test GET /api/vehicles/{id} in tests/Feature/Vehicle/ShowTest.php"
Task: "Contract test GET /api/packages in tests/Feature/Package/IndexTest.php"
Task: "Contract test POST /api/rentals/check-availability in tests/Feature/Rental/CheckAvailabilityTest.php"
Task: "Contract test POST /api/rentals in tests/Feature/Rental/StoreTest.php"
Task: "Contract test GET /api/rentals/my-rentals in tests/Feature/Rental/IndexUserTest.php"
Task: "Contract test GET /api/admin/vehicles in tests/Feature/Admin/Vehicle/IndexTest.php"
Task: "Contract test POST /api/admin/vehicles in tests/Feature/Admin/Vehicle/StoreTest.php"
Task: "Contract test GET /api/admin/rentals in tests/Feature/Admin/Rental/IndexTest.php"
Task: "Contract test GET /api/admin/calendar in tests/Feature/Admin/Calendar/IndexTest.php"
```

## Notes
- [P] tasks = different files, no dependencies
- Verify tests fail before implementing
- Commit after each task
- Avoid: vague tasks, same file conflicts

## Task Generation Rules
*Applied during main() execution*

1. **From Contracts**:
   - Each contract file → contract test task [P]
   - Each endpoint → implementation task
   
2. **From Data Model**:
   - Each entity → model creation task [P]
   - Relationships → service layer tasks
   
3. **From User Stories**:
   - Each story → integration test [P]
   - Quickstart scenarios → validation tasks

4. **Ordering**:
   - Setup → Tests → Models → Services → Endpoints → Frontend → Polish
   - Dependencies block parallel execution

## Validation Checklist
*GATE: Checked by main() before returning*

- [ ] All contracts have corresponding tests
- [ ] All entities have model tasks
- [ ] All tests come before implementation
- [ ] Parallel tasks truly independent
- [ ] Each task specifies exact file path
- [ ] No task modifies same file as another [P] task