# AirBnB Clone Requirements

## Introduction

This document outlines the requirements for the AirBnB Clone project.

## User Requirements

### 1. User Authentication System

#### Functional Requirements

##### Registration

- Allow users to register as either a guest or a host by providing:
  - Full Name
  - Email Address
  - Password (hashed securely before storage)
  - Optional profile photo and phone number
- Validate email format and password strength during registration.
- Send a confirmation email after successful registration.

##### Login

- Enable users to log in using:
  - Email and password combination.
  - OAuth options for social login (e.g., Google, Facebook).

##### Authentication

- Use JSON Web Tokens (JWT) for managing user sessions.
- Token should include user roles (e.g., "guest," "host," "admin").

##### Forgot Password

- Sends a password reset link via email.
- Validates the token and expiration time for password resets.

#### Technical Requirements

- Authentication service built using Python Django framework.
- Secure password hashing using bcrypt.
- Implement role-based access control (RBAC) to restrict actions by user type.
- Configure OAuth providers (Google, Facebook) using Authlib.

#### Non-Functional Requirements

- Ensure login APIs respond within 200ms under normal load.
- Log all failed login attempts and lock accounts temporarily after 5 failed attempts.
- Encrypt all sensitive user data before storage.

### 2. Property Management System

#### Functional Requirements

##### Add Listings

- Hosts can add property details, including:
  - Title
  - Description
  - Location (address, city, country, geolocation coordinates)
  - Price per night
  - Amenities (Wi-Fi, pool, pet-friendly)
  - Photos (upload one or more images)
  - Availability (calendar-based).

##### Edit/Delete Listings

- Allow hosts to update or remove their property listings.

##### Listing Visibility

- Guests can view property details but cannot edit them.

##### Technical Requirements

- Use a relational database (e.g., PostgreSQL) to store property data.
- Implement file upload and storage for property images using AWS S3 or Cloudinary.
- Validate property details (e.g., price must be positive, availability dates must be valid).

##### Non-Functional Requirements

- Optimize database queries for search and filter operations.
- Handle up to 10,000 property listings with minimal performance degradation.

### 3. Booking Management System

#### Functional Requirements

##### Booking Creation:
- Guests can select a property, specify dates, and create a booking.
- Validate booking dates against the property’s availability to prevent conflicts.

##### Booking Cancellation:

- Allow guests to cancel a booking if within the allowed cancellation policy period.
- Notify the host via email or in-app notifications upon cancellation.

##### Booking Status:

- Track and update booking statuses:
  - Pending
  - Confirmed
  - Canceled
  - Completed

#### Technical Requirements

- Implement a database table for managing bookings:
  - Fields: Booking ID, Guest ID, Property ID, Start Date, End Date, Status, and Payment Details.
- Use transaction-based processing to ensure data consistency for payments and booking updates.
- Notify hosts and guests of booking changes via SendGrid email service.

#### Non-Functional Requirements

- Ensure that the booking process takes no longer than 1 second under normal load.
- Scale to handle up to 100,000 bookings per month.
- Log booking activities for monitoring and debugging purposes.
