# Event Management System - Backend API

A comprehensive RESTful backend API for managing events, user authentication, and booking operations. Built with Node.js, Express.js, and MongoDB, this system provides a complete solution for event organizers and attendees to create, manage, and book events efficiently.

## Table of Contents

- [Overview](#overview)
- [Core Features](#core-features)
- [Technology Stack](#technology-stack)
- [System Architecture](#system-architecture)
- [Installation Guide](#installation-guide)
- [Environment Configuration](#environment-configuration)
- [API Documentation](#api-documentation)
- [Authentication System](#authentication-system)
- [Database Schema](#database-schema)
- [Security Implementation](#security-implementation)
- [Application Workflow](#application-workflow)
- [Error Handling](#error-handling)

## Overview

The Event Management System is a production-ready backend application engineered to streamline event creation, discovery, and booking operations. The platform serves two distinct user personas: standard users who can explore and reserve event seats, and organizers who possess administrative capabilities to create and manage events.

### Key Capabilities

This system implements a complete event lifecycle management solution including user registration with email verification, secure JWT-based authentication, role-based access control, event CRUD operations with image management, intelligent booking management with seat tracking, automated email notifications, and comprehensive security measures against common web vulnerabilities.

## Core Features

### Authentication and User Management

- User registration with email validation and verification workflow
- Secure login system with JWT token-based authentication
- Role-based access control supporting two user types: User and Organizer
- Email verification using time-bound verification codes (5-minute validity)
- Password encryption using bcryptjs hashing algorithm
- Secure cookie-based token storage with HTTP-only flags
- User logout functionality with token invalidation

### Event Management System

- Complete CRUD operations for event management
- Event categorization across six categories: Technology, Music, Workshop, Seminar, Sports, and Entertainment
- Cloud-based image storage and retrieval using Cloudinary integration
- Real-time seat availability tracking and management
- Organizer-specific event dashboard and listings
- Public event discovery and browsing interface
- Event validation including date verification and capacity management

### Booking and Reservation System

- Authenticated user booking functionality with authorization checks
- Duplicate booking prevention mechanism
- Real-time seat availability validation before booking confirmation
- Automatic prevention of bookings for past events
- Automated email notifications with booking confirmations
- Separate booking management interfaces for users and organizers
- Relationship tracking between users, events, and organizers

### Communication and Notifications

- Automated welcome emails upon successful registration
- Verification code delivery via email
- Booking confirmation emails with comprehensive event details
- Dynamic email generation using EJS templating engine
- Configurable SMTP integration for reliable email delivery

## Technology Stack

### Core Framework and Runtime

- **Node.js**: JavaScript runtime for server-side execution
- **Express.js v5.1.0**: Web application framework for RESTful API development

### Database Layer

- **MongoDB**: NoSQL document database for data persistence
- **Mongoose v8.16.1**: Object Data Modeling (ODM) library for MongoDB

### Security and Authentication

- **jsonwebtoken**: JWT creation and verification for stateless authentication
- **bcryptjs**: Password hashing with salt generation
- **cookie-parser**: Signed cookie parsing and management
- **express-rate-limit**: API rate limiting to prevent abuse
- **helmet**: HTTP security headers configuration
- **xss-clean**: Cross-Site Scripting (XSS) attack prevention
- **express-mongo-sanitize**: NoSQL injection attack prevention
- **validator**: Input validation and sanitization

### File Management and Media Processing

- **Cloudinary v2.7.0**: Cloud-based image storage and CDN
- **express-fileupload v1.5.1**: Multipart file upload handling

### Email and Document Generation

- **Nodemailer v7.0.4**: Email delivery service
- **EJS v3.1.10**: Embedded JavaScript templating for emails
- **QRCode v1.5.4**: QR code generation for bookings
- **PDFKit v0.17.1**: PDF document generation

### Development and Monitoring

- **Morgan**: HTTP request logging middleware
- **express-async-handler**: Async error handling wrapper
- **CORS**: Cross-Origin Resource Sharing configuration
- **dotenv**: Environment variable management

## System Architecture

The application follows the MVC (Model-View-Controller) architectural pattern with a clear separation of concerns:

```
Application Layer (app.js)
    ├── Middleware Stack
    │   ├── Security Layer (Helmet, CORS, Rate Limiting)
    │   ├── Request Processing (JSON, Cookies, File Upload)
    │   └── Logging (Morgan)
    │
    ├── Route Layer
    │   ├── Authentication Routes (/api/v1/auth)
    │   ├── Event Routes (/api/v1/events)
    │   └── Booking Routes (/api/v1/bookings)
    │
    ├── Controller Layer
    │   ├── Business Logic Implementation
    │   └── Request/Response Handling
    │
    ├── Model Layer
    │   ├── Data Schema Definitions
    │   └── Database Interactions
    │
    └── Error Handling Layer
        ├── Custom Error Classes
        └── Global Error Handler
```

### Directory Structure

```
EventManagement-DB/
├── app.js                      # Application entry point and configuration
├── package.json                # Dependency management and scripts
│
├── controllers/                # Business logic and request handlers
│   ├── authController.js       # User authentication and authorization logic
│   ├── eventController.js      # Event management operations
│   └── bookingController.js    # Booking creation and management
│
├── models/                     # Mongoose schemas and models
│   ├── User.js                 # User data model with authentication methods
│   ├── Event.js                # Event data model with validation
│   └── Booking.js              # Booking relationship model
│
├── routes/                     # API endpoint definitions
│   ├── authRoute.js            # Authentication endpoint routes
│   ├── eventRoute.js           # Event management routes
│   └── bookingRoute.js         # Booking management routes
│
├── middlewares/                # Custom middleware functions
│   ├── authentication.js       # JWT verification and role authorization
│   ├── errorHandler.js         # Centralized error processing
│   └── notFound.js             # 404 route handler
│
├── utils/                      # Helper functions and utilities
│   ├── attachCookie.js         # Cookie configuration and attachment
│   ├── generateCode.js         # Random verification code generation
│   ├── generatePayload.js      # JWT payload construction
│   ├── nodemailerConfig.js     # Email service configuration
│   ├── sendEmail.js            # Email dispatch utility
│   ├── sendVerifyEmail.js      # Verification email sender
│   ├── verifyJwt.js            # JWT token verification
│   └── verifyPermission.js     # Resource ownership verification
│
├── emails/                     # Email template files
│   ├── bookingEmail.ejs        # Booking confirmation template
│   └── verifyEmail.ejs         # Email verification template
│
├── error/                      # Error handling classes
│   └── customError.js          # Custom error implementation
│
├── db/                         # Database configuration
│   └── connectDB.js            # MongoDB connection handler
│
├── public/                     # Static file serving
│   └── index.html              # API documentation landing page
│
└── tmp/                        # Temporary file storage for uploads
```

## Installation Guide

### Prerequisites

- Node.js (version 14.x or higher)
- MongoDB (version 4.x or higher)
- npm or yarn package manager
- Cloudinary account for image storage
- Email service provider (Gmail, SendGrid, etc.)

### Installation Steps

1. Clone the repository to your local environment:

```bash
git clone <repository-url>
cd EventManagement-DB
```

2. Install project dependencies:

```bash
npm install
```

3. Create a `.env` file in the project root directory and configure environment variables (refer to Environment Configuration section)

4. Ensure MongoDB is running on your system or configure MongoDB Atlas connection string

5. Start the application:

**Development Environment:**

```bash
npm run dev
```

This command uses nodemon for automatic server restart on file changes.

**Production Environment:**

```bash
npm start
```

The server will initialize on the configured PORT and establish database connection.

## Environment Configuration

Create a `.env` file in the root directory with the following configuration variables:

```env
# Server Configuration
PORT=5000
NODE_ENV=production

# Database Configuration
MONGO_URI=mongodb://localhost:27017/event-management
# For MongoDB Atlas: mongodb+srv://<username>:<password>@cluster.mongodb.net/event-management

# JWT Authentication
JWT_SECRET=your_secure_jwt_secret_key_minimum_32_characters
JWT_LIFETIME=1d

# Cloudinary Configuration (Image Storage)
CLOUD_NAME=your_cloudinary_cloud_name
CLOUDINARY_API_KEY=your_cloudinary_api_key
CLOUDINARY_API_SECRET=your_cloudinary_api_secret

# Email Service Configuration
EMAIL_HOST=smtp.gmail.com
EMAIL_PORT=587
EMAIL_USER=your_email@gmail.com
EMAIL_PASS=your_application_specific_password
EMAIL_FROM=Event Management <noreply@eventmanagement.com>
```

### Configuration Notes

- **JWT_SECRET**: Use a strong, randomly generated string (minimum 32 characters)
- **MONGO_URI**: Can point to local MongoDB or cloud-based MongoDB Atlas
- **EMAIL_PASS**: For Gmail, use App-specific passwords rather than account password
- **CLOUDINARY**: Register at cloudinary.com to obtain API credentials

## API Documentation

### Base URL

```
http://localhost:5000/api/v1
```

### Authentication Endpoints

**Base Path:** `/api/v1/auth`

| Method | Endpoint                     | Access Level  | Description                | Request Body                |
| ------ | ---------------------------- | ------------- | -------------------------- | --------------------------- |
| POST   | `/register`                  | Public        | Register new user account  | `{ name, email, password }` |
| POST   | `/login`                     | Public        | Authenticate existing user | `{ email, password }`       |
| POST   | `/verify-code?email=<email>` | Public        | Verify email with code     | `{ code }`                  |
| GET    | `/logout`                    | Authenticated | Terminate user session     | None                        |

#### Registration Response Flow

1. User submits registration data
2. System creates user account with `isVerified: false`
3. Returns user object (without password)
4. User must verify email before full access

#### Login Response Flow

1. User submits credentials
2. System validates email and password
3. If unverified: generates and sends verification code
4. If verified: generates JWT token and attaches to cookie
5. Returns user payload with authentication status

### Event Management Endpoints

**Base Path:** `/api/v1/events`

| Method | Endpoint              | Access Level       | Description              | Request Body                                                     |
| ------ | --------------------- | ------------------ | ------------------------ | ---------------------------------------------------------------- |
| GET    | `/`                   | Authenticated User | Retrieve all events      | None                                                             |
| POST   | `/`                   | Organizer          | Create new event         | `{ title, description, location, date, category, seats, image }` |
| GET    | `/showMyEvents`       | Organizer          | List organizer's events  | None                                                             |
| POST   | `/event-image-upload` | Organizer          | Upload event image       | `multipart/form-data: { image }`                                 |
| GET    | `/:id`                | Authenticated User | Get event details        | None                                                             |
| PATCH  | `/:id`                | Organizer (Owner)  | Update event information | `{ fields to update }`                                           |
| DELETE | `/:id`                | Organizer (Owner)  | Delete event             | None                                                             |

#### Event Categories

- Technology
- Music
- Workshop
- Seminar
- Sports
- Entertainment

#### Event Image Upload

- Accepts image files via multipart form data
- Uploads to Cloudinary cloud storage
- Returns secure URL for event association
- Automatically removes temporary files

### Booking Management Endpoints

**Base Path:** `/api/v1/bookings`

| Method | Endpoint                 | Access Level       | Description                              |
| ------ | ------------------------ | ------------------ | ---------------------------------------- |
| GET    | `/:id`                   | Authenticated User | Create booking for event (id = eventId)  |
| GET    | `/showUserBookings`      | Authenticated User | Retrieve user's bookings                 |
| GET    | `/showOrganizerBookings` | Organizer          | Retrieve bookings for organizer's events |

#### Booking Creation Process

1. Validates user authentication
2. Checks event existence and future date
3. Verifies seat availability
4. Prevents duplicate bookings
5. Creates booking record
6. Increments seatsOccupied counter
7. Sends confirmation email
8. Returns booking confirmation

### Response Format

All API responses follow a consistent JSON structure:

**Success Response:**

```json
{
  "status": "success",
  "data": { ... },
  "message": "Operation completed successfully"
}
```

**Error Response:**

```json
{
  "status": "error",
  "message": "Error description",
  "statusCode": 400
}
```

## Authentication System

### JWT-Based Authentication

The application implements stateless authentication using JSON Web Tokens (JWT). Tokens are securely stored in HTTP-only, signed cookies to prevent client-side JavaScript access and XSS attacks.

### Authentication Flow

1. **User Registration**

   - User submits registration data (name, email, password)
   - Password is hashed using bcryptjs with salt rounds
   - User record created with `isVerified: false`
   - Account created but requires verification

2. **Email Verification**

   - Upon login attempt with unverified account, system generates 6-digit verification code
   - Code validity: 5 minutes from generation
   - Code sent to registered email address
   - User submits code via verification endpoint
   - System validates code and expiration time
   - Updates `isVerified` to true
   - Generates and returns JWT token

3. **Authentication Token Generation**

   - Token payload includes: userId, name, email, role
   - Token signed with JWT_SECRET
   - Token attached to HTTP-only cookie
   - Cookie configuration: signed, secure (production), httpOnly

4. **Request Authentication**

   - Client automatically sends cookie with each request
   - Authentication middleware extracts and verifies token
   - User payload attached to request object
   - Request proceeds to route handler

5. **Authorization Checks**
   - Role-based middleware verifies user role
   - Resource ownership verified for update/delete operations
   - Unauthorized requests return 403 Forbidden

### Token Structure

```javascript
{
  userId: "user_mongodb_id",
  name: "User Name",
  email: "user@example.com",
  role: "user" | "organizer"
}
```

### Security Measures

- Passwords never stored in plain text
- JWT tokens time-limited (configurable expiration)
- Verification codes expire after 5 minutes
- HTTP-only cookies prevent XSS token theft
- Signed cookies prevent tampering
- HTTPS enforced in production (secure flag)

## Database Schema

### User Schema

```javascript
{
  name: {
    type: String,
    required: true
  },
  email: {
    type: String,
    required: true,
    unique: true,
    validated: true // Uses validator.isEmail
  },
  password: {
    type: String,
    required: true,
    minlength: 5,
    hashed: true // Pre-save hook hashes password
  },
  role: {
    type: String,
    enum: ['user', 'organizer'],
    default: 'user'
  },
  isVerified: {
    type: Boolean,
    default: false
  },
  code: {
    type: String // Temporary verification code
  },
  verifyDate: {
    type: Date // Code generation timestamp
  },
  refreshToken: {
    type: String
  }
}
```

**Methods:**

- `comparePassword(candidatePassword)`: Compares input with hashed password
- `createToken(payload)`: Generates JWT token

### Event Schema

```javascript
{
  title: {
    type: String,
    required: true,
    maxlength: 100
  },
  description: {
    type: String,
    required: true,
    maxlength: 300
  },
  location: {
    type: String,
    required: true
  },
  date: {
    type: Date,
    required: true
  },
  category: {
    type: String,
    enum: ['Technology', 'Music', 'Workshop', 'Seminar', 'Sports', 'Entertainment'],
    default: 'Technology'
  },
  seats: {
    type: Number,
    required: true
  },
  image: {
    type: String // Cloudinary URL
  },
  seatsOccupied: {
    type: Number,
    default: 0
  },
  organizer: {
    type: ObjectId,
    ref: 'User',
    required: true
  }
}
```

### Booking Schema

```javascript
{
  user: {
    type: ObjectId,
    ref: 'User',
    required: true
  },
  organizer: {
    type: ObjectId,
    ref: 'User',
    required: true
  },
  event: {
    type: ObjectId,
    ref: 'Event',
    required: true
  },
  createdAt: {
    type: Date,
    auto: true
  },
  updatedAt: {
    type: Date,
    auto: true
  }
}
```

**Indexes:**

- Composite unique index on (user, event) prevents duplicate bookings
- Reference indexes for efficient population queries

## Security Implementation

### Multi-Layer Security Architecture

1. **Rate Limiting**

   - Window: 15 minutes
   - Maximum requests: 100 per IP address
   - Protection against brute force and DDoS attacks
   - Custom error message on limit exceeded

2. **HTTP Security Headers (Helmet)**

   - Content Security Policy configuration
   - X-Frame-Options for clickjacking prevention
   - X-Content-Type-Options to prevent MIME sniffing
   - Strict-Transport-Security for HTTPS enforcement

3. **Cross-Origin Resource Sharing (CORS)**

   - Configured to allow specific origins
   - Credential support enabled for cookie-based authentication
   - Preflight request handling

4. **Input Sanitization**

   - **XSS Protection**: xss-clean middleware sanitizes user input
   - **NoSQL Injection Prevention**: express-mongo-sanitize removes prohibited characters
   - **Validation**: validator library for email and data format validation

5. **Password Security**

   - bcryptjs hashing with automatic salt generation
   - Minimum password length enforcement (5 characters)
   - Password comparison without timing attacks

6. **Cookie Security**

   - HTTP-only flag prevents JavaScript access
   - Signed cookies prevent tampering
   - Secure flag enforced in production (HTTPS only)
   - SameSite attribute for CSRF protection

7. **JWT Token Security**

   - Secret key based signing
   - Token expiration enforcement
   - Payload minimal to reduce token size
   - Token invalidation on logout

8. **Database Security**

   - Connection string environment variable isolation
   - MongoDB sanitization middleware
   - Indexed queries for performance and security

9. **File Upload Security**

   - Temporary file storage with cleanup
   - Cloud storage integration (Cloudinary)
   - File type validation

10. **Error Handling Security**
    - Production errors hide sensitive information
    - Stack traces disabled in production
    - Consistent error response format

## Application Workflow

### User Registration and Verification Workflow

1. User submits registration form with name, email, and password
2. System validates input data and checks email uniqueness
3. Password hashed and user record created with `isVerified: false`
4. User receives successful registration response
5. On login attempt, system detects unverified status
6. Six-digit verification code generated and stored with timestamp
7. Verification email sent using EJS template
8. User submits verification code within 5-minute window
9. System validates code and timestamp
10. Account marked as verified, JWT token generated and returned

### Event Creation and Booking Workflow

**Organizer Perspective:**

1. Organizer registers and verifies account
2. Logs in with organizer role
3. Optionally uploads event image to Cloudinary
4. Creates event with details and image URL
5. Event stored in database with organizer reference
6. Views bookings for created events via organizer dashboard

**User Perspective:**

1. User registers, verifies, and logs in
2. Browses all available events
3. Views detailed event information
4. Attempts to book event
5. System validates:
   - Event exists and is future-dated
   - Seats available (seatsOccupied < seats)
   - No duplicate booking exists
6. Booking created with user, event, and organizer references
7. Event seatsOccupied incremented
8. Confirmation email sent with booking details
9. User can view all bookings in personal dashboard

### Event Management Workflow

1. Organizer creates event with full details
2. Event appears in public event listings
3. Users discover and book available events
4. Seat counter updates in real-time
5. When capacity reached, booking disabled
6. Organizer can update event details (ownership verified)
7. Organizer can delete event (removes bookings)
8. Past events automatically ineligible for new bookings

## Error Handling

### Centralized Error Management

The application implements a global error handling strategy using custom error classes and middleware:

**Custom Error Class:**

```javascript
class CustomError extends Error {
  constructor(message, statusCode) {
    super(message);
    this.statusCode = statusCode;
  }
}
```

**Error Handler Middleware:**

- Catches all errors from async operations
- Formats error response consistently
- Logs errors for monitoring
- Hides sensitive information in production
- Returns appropriate HTTP status codes

**Common Error Scenarios:**

- 400 Bad Request: Invalid input data, validation failures
- 401 Unauthorized: Invalid credentials, missing/invalid token
- 403 Forbidden: Insufficient permissions, resource ownership violation
- 404 Not Found: Resource does not exist
- 409 Conflict: Duplicate booking, unique constraint violation
- 429 Too Many Requests: Rate limit exceeded
- 500 Internal Server Error: Unexpected server errors

### Async Error Handling

All asynchronous operations wrapped with express-async-handler to automatically catch and forward errors to the global error handler, eliminating the need for try-catch blocks in controllers.
