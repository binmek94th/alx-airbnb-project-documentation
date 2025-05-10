
# 📄 Backend Requirement Specifications

**Repository**: `alx-airbnb-project-documentation`  
**File**: `requirements.md`

This document outlines the technical and functional specifications for three key backend features of the Airbnb Clone project.

---

## 🔐 1. User Authentication

### Description
Enable users to register, log in, and authenticate using secure JWT tokens.

### API Endpoints

- `POST /api/auth/register` – Register as guest or host.
- `POST /api/auth/login` – Authenticate and get token.
- `GET /api/auth/profile` – Get logged-in user profile.

### Input Example (Register)
```json
{
  "first_name": "John",
  "last_name": "Doe",
  "email": "john@example.com",
  "password": "SecurePass123!",
  "role": "guest"
}
```

### Output Example (Login)
```json
{
  "token": "<jwt_token>",
  "user": {
    "id": "uuid",
    "email": "john@example.com",
    "role": "guest"
  }
}
```

### Validation Rules
- Email: must be a valid and unique format.
- Password: minimum 8 characters, with letters and numbers.
- Role: must be either `guest` or `host`.

---

## 🏠 2. Property Management

### Description
Hosts can add, update, or delete property listings.

### API Endpoints

- `POST /api/properties` – Create a new listing.
- `PUT /api/properties/:id` – Update a listing.
- `DELETE /api/properties/:id` – Delete a listing.
- `GET /api/properties/:id` – Get listing details.
- `GET /api/properties` – Get all listings with filtering support.

### Input Example (Create)
```json
{
  "name": "Modern Loft",
  "description": "Spacious loft in downtown.",
  "location": "New York",
  "price_per_night": 120,
  "amenities": ["Wi-Fi", "Air Conditioning"]
}
```

### Validation Rules
- Name, description, location are required.
- `price_per_night` must be a positive decimal.
- Only `host` role users can create, update, or delete listings.

---

## 📅 3. Booking System

### Description
Guests can request bookings for properties and manage their reservations.

### API Endpoints

- `POST /api/bookings` – Book a property.
- `PUT /api/bookings/:id/cancel` – Cancel a booking.
- `GET /api/bookings/:id` – View a single booking.
- `GET /api/bookings` – View user's bookings (past and upcoming).

### Input Example (Create Booking)
```json
{
  "property_id": "uuid",
  "start_date": "2025-07-01",
  "end_date": "2025-07-05"
}
```

### Output Example
```json
{
  "booking_id": "uuid",
  "status": "confirmed",
  "total_price": 480
}
```

### Validation Rules
- Start date must be before end date.
- Check for booking conflicts (prevent double bookings).
- Only users with `guest` role can create bookings.

---

## ⏱️ Performance Criteria

- API responses should return within **800ms** under normal load.
- Paginated results for lists over 20 items.
- JWT tokens expire after **1 hour**.
- Passwords must be hashed using bcrypt or Argon2.

---

## ✅ Optional Enhancements

- Use caching for property search results.
- Implement rate limiting on authentication endpoints.
- Add GraphQL layer for flexible frontend queries (optional).

---
