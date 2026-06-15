# QuayWall - Secure Port Request Management System

A modern, secure PHP web application for managing quay wall requests with staff authentication, real-time status updates, and comprehensive audit logging.

**Built with:** PHP 8.2 | MySQL 8.0 | JavaScript (ES6) | Docker

---

## ✨ Features

### 🎯 Core Functionality
- **Customer Request Submission** - Simple form for submitting quay wall requests
- **Staff Dashboard** - Manage requests with status updates and remarks
- **Audit Logging** - Complete history of all status changes
- **Payment Tracking** - Track payment status for approved requests
- **Email/SMS Notifications** - Automatic customer notifications

### 🔐 Security Features
- **JWT Authentication** - Secure token-based authentication
- **Prepared Statements** - 100% SQL injection protection
- **CSRF Protection** - Double-submit cookie pattern
- **XSS Prevention** - Content Security Policy + safe output
- **Rate Limiting** - Brute force attack protection
- **Bcrypt Hashing** - Secure password storage with adaptive hashing
- **HttpOnly Cookies** - Immune to JavaScript theft

### 🚀 Developer Features
- Clean MVC architecture
- RESTful API design
- Comprehensive error handling
- Automated database migrations
- Docker containerization
- Easy deployment (Docker or traditional hosting)

---

## 📋 API Endpoints

### Authentication
- `POST /api/auth/login` - Staff login
- `POST /api/auth/logout` - Logout
- `POST /api/auth/refresh` - Refresh token
- `GET /api/auth/me` - Current user

### Public
- `GET /api/requests/purposes` - List purposes
- `POST /api/requests` - Submit request
- `GET /api/requests/status/{id}` - Check status

### Protected (Staff)
- `GET /api/dashboard` - List requests
- `PUT /api/dashboard/{id}/status` - Update status
- `GET /api/audit` - Audit log

---

## 🚀 Quick Start

### Docker
```bash
cp backend/.env.example backend/.env
docker-compose up -d
```

### Traditional Hosting
See DEPLOYMENT.md for step-by-step instructions.

---

## 🔐 Security

- ✅ SQL Injection: 0% risk (prepared statements)
- ✅ XSS: Prevented (CSP + output escaping)
- ✅ CSRF: Protected (token validation)
- ✅ Passwords: Bcrypt (cost=12)
- ✅ Authentication: JWT with refresh tokens
- ✅ Rate Limiting: Brute force protection

---

## 📚 Documentation

- **README.md** - Project overview
- **DEPLOYMENT.md** - Deployment instructions
- **SECURITY.md** - Security architecture
- **PROGRESS.md** - Development status

---

## 📝 License

MIT License

---

**Made with ❤️ for maritime operations**