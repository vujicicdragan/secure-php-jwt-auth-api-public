# Secure PHP JWT Auth API

Production-ready PHP authentication core designed for real backend applications.

Secure PHP JWT Auth API provides a structured backend authentication system built with a clean modular architecture.  
It implements short-lived access tokens, refresh token rotation, database-backed token invalidation, and middleware-based request protection.

The project is designed as a reusable authentication core that can be integrated into SaaS platforms, admin panels, mobile backends, or any PHP API environment.

---

# Key Features

• JWT Access Token authentication  
• Refresh Token Rotation  
• Database-backed token invalidation  
• Centralized logout control  
• Middleware-based authorization  
• Rate limiting protection  
• CORS middleware support  
• Clean router architecture  
• Environment configuration system  
• Modular service layer

---

# Architecture Overview

The system is organized using a layered architecture to keep responsibilities clearly separated.

```
--> Client

--> Router
--> 
--> Middleware
--> 
--> Controller
--> 
--> Service
--> 
--> Repository
--> 
--> Database
```

This structure ensures that authentication logic remains reusable and scalable across different applications.

---

# Project Structure

```
src/

Controllers/
    AuthController.php
    UserController.php
    HealthController.php

Core/
    Router.php
    Database.php
    Response.php
    Env.php
    Validator.php
    ApiException.php

Http/
    Request.php

Middleware/
    AuthMiddleware.php
    CorsMiddleware.php
    RateLimitMiddleware.php

Repositories/
    UserRepository.php
    RefreshTokenRepository.php

Services/
    JwtService.php
```

Additional directories:

```
database/        database schema
storage/         token storage / runtime data
tools/           CLI utilities
vendor/          composer dependencies
```

---

# Authentication Flow

The authentication model follows modern token security practices.

### Login

1. User sends credentials
2. Server validates credentials
3. Server generates

• short-lived access token  
• long-lived refresh token

4. Refresh token stored in database
5. Access token returned to client

---

### Token Refresh

When access token expires:

1. Client sends refresh token
2. Server validates token in database
3. Old refresh token invalidated
4. New refresh token issued
5. New access token generated

This process prevents token replay attacks.

---

### Logout

Logout invalidates the refresh token in the database.

This immediately revokes future session renewals.

---

# Security Features

### Refresh Token Rotation

Each refresh operation replaces the previous refresh token.

Benefits:

• prevents replay attacks  
• protects stolen tokens  
• improves session control

---

### Database Token Invalidation

Refresh tokens are stored and validated in the database.

Advantages:

• central logout control  
• session revocation  
• compromised token protection

---

### Rate Limiting

Rate limiting middleware prevents brute force attacks.

Typical protections:

• login attempts  
• token refresh abuse  
• API flooding

---

### CORS Protection

CORS middleware ensures secure cross-origin API usage.

---

# Environment Configuration

Environment variables are loaded through the internal `Env` system.

Example `.env`:

```
DB_HOST=localhost
DB_NAME=auth_db
DB_USER=root
DB_PASS=password

JWT_SECRET=your_secret_key
JWT_EXPIRE=900
REFRESH_EXPIRE=604800
```

---

# Installation

### 1 Clone repository

```
git clone https://github.com/vujicicdragan/secure-php-jwt-auth-api-public.git
```

---

### 2 Install dependencies

```
composer install
```

---

### 3 Configure environment

Copy example environment file.

```
cp .env.example .env
```

Edit database credentials and JWT configuration.

---

### 4 Import database

Import schema from:

```
database/
```

---

### 5 Start server

Using PHP built-in server:

```
php -S localhost:8000
```

---

# API Endpoints

### Authentication

```
POST /api/v1/auth/register
POST /api/v1/auth/login
POST /api/v1/auth/refresh
POST /api/v1/auth/logout
```

---

### User

```
GET /api/v1/auth/me
```

Requires valid access token.

---

### Health Check

```
GET /api/v1/health
```

Used for service monitoring.

---

# Example Login Request

```
POST /api/v1/auth/login
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "password"
}
```

Response:

```
{
  "access_token": "JWT_TOKEN",
  "refresh_token": "REFRESH_TOKEN"
}
```

---

# CLI Tools

The repository contains CLI utilities for development.

```
tools/cli.php
tools/seed_user.php
```

Example:

```
php tools/seed_user.php
```

Creates a test user for development.

---

# Use Cases

Secure PHP JWT Auth API can serve as an authentication core for:

• SaaS platforms  
• admin dashboards  
• mobile application backends  
• REST API services  
• microservice architectures

---

# Development Philosophy

This project focuses on:

• security-first authentication design  
• minimal dependencies  
• modular architecture  
• backend reusability

The system is intended to act as a foundation for real production applications rather than a tutorial project.

---

# License

MIT License

---

# Author

SecureCoreAuth
