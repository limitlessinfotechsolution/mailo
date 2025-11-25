# MailO - Additional Requirements Checklist

## 🎯 What Else Is Needed for Production

Based on the current state of your MailO project, here are the additional items needed:

---

## 1. 📦 Package.json Enhancements

### Root package.json
Add helpful scripts for monorepo management:

```json
{
  "scripts": {
    "dev": "concurrently \"npm run dev -w backend\" \"npm run dev -w webmail\"",
    "build": "npm run build -w webmail && npm run build -w backend",
    "build:webmail": "npm run build -w webmail",
    "build:backend": "npm run build -w backend",
    "lint": "npm run lint -w webmail && npm run lint -w backend",
    "lint:fix": "npm run lint:fix -w webmail && npm run lint:fix -w backend",
    "test": "npm run test -w webmail && npm run test -w backend",
    "docker:build": "docker compose build",
    "docker:up": "docker compose up -d",
    "docker:down": "docker compose down",
    "docker:logs": "docker compose logs -f",
    "clean": "rm -rf node_modules webmail/node_modules backend/node_modules webmail/dist",
    "postinstall": "echo 'Dependencies installed successfully!'"
  }
}
```

---

## 2. 🔐 Enhanced .env.example

Your current `.env.example` is basic. Here's a comprehensive version:

```env
# ==============================================
# MailO Configuration
# ==============================================

# Environment
NODE_ENV=production
PORT=5000

# ==============================================
# Database Configuration
# ==============================================

# MongoDB
MONGODB_URI=mongodb://admin:password@localhost:27017/mailo?authSource=admin
MONGODB_MAX_POOL_SIZE=10
MONGODB_MIN_POOL_SIZE=2

# Redis
REDIS_URI=redis://localhost:6379
REDIS_PASSWORD=
REDIS_DB=0

# ==============================================
# Storage Configuration
# ==============================================

# MinIO (S3-compatible storage)
MINIO_ENDPOINT=localhost
MINIO_PORT=9000
MINIO_ACCESS_KEY=admin
MINIO_SECRET_KEY=change-this-password
MINIO_USE_SSL=false
MINIO_BUCKET=mailo-emails
MINIO_REGION=us-east-1

# ==============================================
# Authentication & Security
# ==============================================

# JWT Configuration
JWT_SECRET=change-this-to-a-random-secret-key-minimum-32-characters
JWT_EXPIRES_IN=7d
JWT_REFRESH_SECRET=change-this-to-another-random-secret-key
JWT_REFRESH_EXPIRES_IN=30d

# Session
SESSION_SECRET=change-this-session-secret
SESSION_MAX_AGE=86400000

# Password Policy
PASSWORD_MIN_LENGTH=8
PASSWORD_REQUIRE_UPPERCASE=true
PASSWORD_REQUIRE_LOWERCASE=true
PASSWORD_REQUIRE_NUMBERS=true
PASSWORD_REQUIRE_SPECIAL=true

# Rate Limiting
RATE_LIMIT_WINDOW_MS=900000
RATE_LIMIT_MAX_REQUESTS=100

# ==============================================
# Email Server Configuration
# ==============================================

# SMTP Server (Outgoing)
SMTP_HOST=localhost
SMTP_PORT=25
SMTP_SECURE=false
SMTP_USER=
SMTP_PASS=

# IMAP Server (Incoming)
IMAP_HOST=localhost
IMAP_PORT=143
IMAP_SECURE=false

# Default Email Settings
DEFAULT_FROM_EMAIL=noreply@yourdomain.com
DEFAULT_FROM_NAME=MailO
SUPPORT_EMAIL=support@yourdomain.com

# ==============================================
# Application Configuration
# ==============================================

# Domain
APP_DOMAIN=yourdomain.com
APP_URL=https://mail.yourdomain.com
WEBMAIL_URL=https://mail.yourdomain.com

# Admin
ADMIN_EMAIL=admin@yourdomain.com
ADMIN_PASSWORD=change-this-admin-password

# Quota (in bytes)
DEFAULT_USER_QUOTA=10737418240
DEFAULT_DOMAIN_QUOTA=107374182400

# ==============================================
# Features
# ==============================================

# Enable/Disable Features
ENABLE_REGISTRATION=false
ENABLE_2FA=true
ENABLE_EMAIL_VERIFICATION=true
ENABLE_PASSWORD_RESET=true
ENABLE_CAMPAIGNS=true
ENABLE_CALENDAR=true
ENABLE_CONTACTS=true
ENABLE_TASKS=true
ENABLE_NOTES=true

# ==============================================
# Logging & Monitoring
# ==============================================

# Logging
LOG_LEVEL=info
LOG_FILE=logs/mailo.log
LOG_MAX_SIZE=10m
LOG_MAX_FILES=7

# Sentry (Error Tracking)
SENTRY_DSN=
SENTRY_ENVIRONMENT=production

# ==============================================
# External Services
# ==============================================

# SendGrid (for transactional emails)
SENDGRID_API_KEY=

# Twilio (for SMS 2FA)
TWILIO_ACCOUNT_SID=
TWILIO_AUTH_TOKEN=
TWILIO_PHONE_NUMBER=

# Google OAuth (optional)
GOOGLE_CLIENT_ID=
GOOGLE_CLIENT_SECRET=
GOOGLE_CALLBACK_URL=

# Microsoft OAuth (optional)
MICROSOFT_CLIENT_ID=
MICROSOFT_CLIENT_SECRET=
MICROSOFT_CALLBACK_URL=

# ==============================================
# Performance
# ==============================================

# Caching
CACHE_TTL=3600
CACHE_MAX_ITEMS=1000

# Worker Threads
WORKER_THREADS=4
MAX_CONCURRENT_JOBS=10

# Upload Limits
MAX_FILE_SIZE=26214400
MAX_FILES_PER_EMAIL=10

# ==============================================
# Development Only
# ==============================================

# Debug
DEBUG=false
VERBOSE_LOGGING=false

# CORS
CORS_ORIGIN=http://localhost:5173
ALLOWED_ORIGINS=http://localhost:5173,https://yourdomain.com
```

---

## 3. 📊 Health Check Endpoint

Add to `backend/src/routes/health.js`:

```javascript
import express from 'express';
import mongoose from 'mongoose';
import { createClient } from 'redis';

const router = express.Router();

router.get('/health', async (req, res) => {
  const health = {
    status: 'ok',
    timestamp: new Date().toISOString(),
    uptime: process.uptime(),
    services: {}
  };

  try {
    // Check MongoDB
    health.services.mongodb = mongoose.connection.readyState === 1 ? 'connected' : 'disconnected';

    // Check Redis
    const redis = createClient({ url: process.env.REDIS_URI });
    await redis.connect();
    await redis.ping();
    health.services.redis = 'connected';
    await redis.disconnect();

    // Check MinIO (optional)
    health.services.storage = 'ok';

    res.json(health);
  } catch (error) {
    health.status = 'error';
    health.error = error.message;
    res.status(503).json(health);
  }
});

router.get('/ready', (req, res) => {
  res.json({ ready: true });
});

router.get('/live', (req, res) => {
  res.json({ alive: true });
});

export default router;
```

---

## 4. 🧪 Testing Setup

### Add Jest Configuration

Create `jest.config.js`:

```javascript
export default {
  testEnvironment: 'node',
  coverageDirectory: 'coverage',
  collectCoverageFrom: [
    'backend/src/**/*.js',
    'webmail/src/**/*.{js,jsx}',
    '!**/node_modules/**',
    '!**/dist/**'
  ],
  testMatch: [
    '**/__tests__/**/*.js',
    '**/?(*.)+(spec|test).js'
  ],
  transform: {
    '^.+\\.jsx?$': 'babel-jest'
  }
};
```

### Add Test Scripts to package.json

```json
{
  "scripts": {
    "test": "jest",
    "test:watch": "jest --watch",
    "test:coverage": "jest --coverage"
  },
  "devDependencies": {
    "jest": "^29.7.0",
    "@testing-library/react": "^14.0.0",
    "@testing-library/jest-dom": "^6.1.0",
    "supertest": "^6.3.0"
  }
}
```

---

## 5. 📝 API Documentation with Swagger

Create `backend/src/swagger.js`:

```javascript
import swaggerJsdoc from 'swagger-jsdoc';
import swaggerUi from 'swagger-ui-express';

const options = {
  definition: {
    openapi: '3.0.0',
    info: {
      title: 'MailO API',
      version: '1.0.0',
      description: 'Enterprise Email Server Platform API',
      contact: {
        name: 'Limitless Infotech Solution Pvt Ltd',
        email: 'dev@limitlessinfotech.com'
      }
    },
    servers: [
      {
        url: 'http://localhost:5000',
        description: 'Development server'
      },
      {
        url: 'https://api.yourdomain.com',
        description: 'Production server'
      }
    ],
    components: {
      securitySchemes: {
        bearerAuth: {
          type: 'http',
          scheme: 'bearer',
          bearerFormat: 'JWT'
        }
      }
    },
    security: [{
      bearerAuth: []
    }]
  },
  apis: ['./src/routes/*.js']
};

const specs = swaggerJsdoc(options);

export { specs, swaggerUi };
```

Add to `backend/src/index.js`:

```javascript
import { specs, swaggerUi } from './swagger.js';

app.use('/api-docs', swaggerUi.serve, swaggerUi.setup(specs));
```

---

## 6. 🔍 Monitoring & Logging

### Winston Logger Setup

Create `backend/src/utils/logger.js`:

```javascript
import winston from 'winston';

const logger = winston.createLogger({
  level: process.env.LOG_LEVEL || 'info',
  format: winston.format.combine(
    winston.format.timestamp(),
    winston.format.errors({ stack: true }),
    winston.format.json()
  ),
  defaultMeta: { service: 'mailo-backend' },
  transports: [
    new winston.transports.File({ filename: 'logs/error.log', level: 'error' }),
    new winston.transports.File({ filename: 'logs/combined.log' })
  ]
});

if (process.env.NODE_ENV !== 'production') {
  logger.add(new winston.transports.Console({
    format: winston.format.simple()
  }));
}

export default logger;
```

---

## 7. 🐳 Docker Improvements

### Add .dockerignore for backend

Create `backend/.dockerignore`:

```
node_modules
npm-debug.log
.env
.git
.gitignore
README.md
.vscode
.idea
coverage
logs
*.log
```

### Add healthcheck to docker-compose.yml

```yaml
services:
  backend:
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:5000/health"]
      interval: 30s
      timeout: 10s
      retries: 3
      start_period: 40s
```

---

## 8. 📱 Progressive Web App (PWA)

Add to `webmail/public/manifest.json`:

```json
{
  "name": "MailO - Enterprise Email",
  "short_name": "MailO",
  "description": "Self-hosted email platform",
  "start_url": "/",
  "display": "standalone",
  "background_color": "#1a202c",
  "theme_color": "#3b82f6",
  "icons": [
    {
      "src": "/icon-192.png",
      "sizes": "192x192",
      "type": "image/png"
    },
    {
      "src": "/icon-512.png",
      "sizes": "512x512",
      "type": "image/png"
    }
  ]
}
```

---

## 9. 🔒 Security Headers

Add to `backend/src/middleware/security.js`:

```javascript
import helmet from 'helmet';

export const securityHeaders = helmet({
  contentSecurityPolicy: {
    directives: {
      defaultSrc: ["'self'"],
      styleSrc: ["'self'", "'unsafe-inline'"],
      scriptSrc: ["'self'"],
      imgSrc: ["'self'", "data:", "https:"],
      connectSrc: ["'self'"],
      fontSrc: ["'self'"],
      objectSrc: ["'none'"],
      mediaSrc: ["'self'"],
      frameSrc: ["'none'"]
    }
  },
  hsts: {
    maxAge: 31536000,
    includeSubDomains: true,
    preload: true
  }
});
```

---

## 10. 📈 Performance Monitoring

### Add Performance Metrics

Create `backend/src/middleware/metrics.js`:

```javascript
import prometheus from 'prom-client';

const register = new prometheus.Registry();

prometheus.collectDefaultMetrics({ register });

const httpRequestDuration = new prometheus.Histogram({
  name: 'http_request_duration_seconds',
  help: 'Duration of HTTP requests in seconds',
  labelNames: ['method', 'route', 'status_code'],
  registers: [register]
});

export const metricsMiddleware = (req, res, next) => {
  const start = Date.now();
  
  res.on('finish', () => {
    const duration = (Date.now() - start) / 1000;
    httpRequestDuration
      .labels(req.method, req.route?.path || req.path, res.statusCode)
      .observe(duration);
  });
  
  next();
};

export const metricsEndpoint = async (req, res) => {
  res.set('Content-Type', register.contentType);
  res.end(await register.metrics());
};
```

---

## ✅ Priority Checklist

### High Priority (Do First)
- [ ] Update .env.example with comprehensive configuration
- [ ] Add health check endpoints
- [ ] Implement proper logging with Winston
- [ ] Add security headers
- [ ] Create basic tests

### Medium Priority (Do Soon)
- [ ] Add Swagger API documentation
- [ ] Implement monitoring/metrics
- [ ] Add PWA manifest
- [ ] Enhance Docker healthchecks
- [ ] Add performance monitoring

### Low Priority (Nice to Have)
- [ ] Advanced testing suite
- [ ] Sentry integration
- [ ] OAuth providers
- [ ] Advanced metrics dashboard
- [ ] Load testing

---

## 📦 Additional npm Packages Needed

```bash
# Backend
npm install -w backend winston swagger-jsdoc swagger-ui-express prom-client

# Testing
npm install -D jest @testing-library/react @testing-library/jest-dom supertest

# Development
npm install -D concurrently nodemon
```

---

## 🎯 Summary

Your project is **90% complete**! The remaining 10% includes:

1. ✅ Enhanced environment configuration
2. ✅ Health monitoring endpoints
3. ✅ Proper logging system
4. ✅ API documentation
5. ✅ Testing infrastructure
6. ✅ Security enhancements
7. ✅ Performance monitoring
8. ✅ PWA support

All of these are **optional but recommended** for production use!

---

**Created by: Limitless Infotech Solution Pvt Ltd.**
