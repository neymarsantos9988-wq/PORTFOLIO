# Bijoy Chakma — Full-Stack Developer Portfolio

A modern, responsive, database-backed personal developer portfolio and administrative suite built for **Bijoy Chakma** (BCA Student at Akash Global College of Management and Science, Expected Graduation: 2027, Aspiring Frontend Developer & Fresher).

Designed with a futuristic dark theme, neon cyan/violet accents, smooth micro-interactions, complete MongoDB persistence, JWT authentication, and an administrative control panel.

---

## 🚀 Key Features

- **Futuristic UI/UX**: Near-black palette (`#07090e`), neon cyan (`#00f5ff`) and violet (`#8b5cf6`) accents, glassmorphic cards, and subtle background glow effects.
- **Light & Dark Mode**: Persistent theme toggle storing user preference locally.
- **Dynamic Projects Showcase**: Real-time project catalog with category filtering (`Frontend`, `Full Stack`, `All`) and detailed inspection modals with feature checklists.
- **Contact Form with Database Persistence**: Validated inquiry form with anti-spam honeypot protection, rate-limiting, and automatic storage in MongoDB with optional SMTP notification forwarding.
- **Interactive Resume Download**: One-click preview and download for PDF resume with configurable path.
- **Protected Admin Dashboard (`/admin`)**:
  - Secure JWT authentication with HttpOnly cookies & Bearer tokens.
  - Project CRUD (Create, Read, Update, Delete) with live state updates.
  - Contact inbox with unread tracking, status updates (`unread`, `read`, `replied`), and deletion.
  - Profile customization (update headline, about narrative, college, graduation year, social links, resume URL).
- **Backend API Security**: Helmet headers, CORS origin filtering, express-rate-limit protection, bcrypt password hashing, input sanitization, and express-validator.
- **Automated Backend Tests**: Built-in test suite verifying health check, project listings, contact form validation, admin login, and route protections.

---

## 🛠️ Technology Stack

| Layer | Technologies |
|---|---|
| **Frontend** | React 19, Vite, JavaScript, CSS3 (Vanilla design system), React Router 7, Axios, Lucide React, Framer Motion |
| **Backend** | Node.js, Express.js (ES Modules), Mongoose, REST API |
| **Database** | MongoDB (supports MongoDB Atlas, local MongoDB, and zero-config in-memory mode) |
| **Security & Auth** | JSON Web Tokens (JWT), bcryptjs, Helmet, CORS, express-rate-limit, express-validator, cookie-parser |
| **Testing** | Node test runner (`node:test`, `node:assert`), Supertest |

---

## 📂 Project Architecture

```
PORTFOLIO/
├── package.json              # Monorepo root scripts (concurrently dev runner)
├── .gitignore                # Git ignore for node_modules, build artifacts, env files
├── README.md                 # Complete documentation and setup guide
│
├── server/                   # Express.js REST API
│   ├── config/
│   │   └── db.js             # Mongoose connection with in-memory / Atlas fallback
│   ├── controllers/
│   │   ├── publicController.js # Public endpoints (profile, projects, contact)
│   │   └── adminController.js  # Protected admin endpoints (CRUD, messages, auth)
│   ├── middleware/
│   │   ├── auth.js           # JWT authentication middleware
│   │   ├── rateLimiter.js    # Rate limiting for API, login, and contact forms
│   │   └── errorHandler.js   # Centralized error handler & 404 handler
│   ├── models/
│   │   ├── Project.js        # Project schema with categories, status, features
│   │   ├── ContactMessage.js # Contact message schema with status tracking
│   │   ├── Admin.js          # Admin credentials with bcrypt comparison
│   │   └── PortfolioProfile.js # Profile, education, skills, social links
│   ├── routes/
│   │   ├── healthRoutes.js   # GET /api/health
│   │   ├── publicRoutes.js   # Public API endpoints
│   │   └── adminRoutes.js    # Protected /api/admin endpoints
│   ├── scripts/
│   │   ├── seed.js           # Seeds Bijoy's profile and initial 3 projects
│   │   └── createAdmin.js    # One-time secure admin generator
│   ├── tests/
│   │   └── api.test.js       # Automated backend integration tests
│   ├── utils/
│   │   └── emailService.js   # Optional SMTP email notification helper
│   ├── .env.example          # Template environment file
│   ├── .env                  # Local environment file
│   ├── app.js                # Express app setup with middleware
│   ├── server.js             # Server entry point
│   └── package.json
│
└── client/                   # React.js + Vite Frontend
    ├── public/
    │   ├── favicon.svg       # Custom BC neon monogram icon
    │   ├── resume.pdf        # Downloadable PDF resume placeholder
    │   └── images/projects/  # Project illustration previews (SVG)
    ├── src/
    │   ├── components/
    │   │   ├── Navbar.jsx    # Monogram logo, links, mobile menu, theme toggle
    │   │   ├── Footer.jsx    # Tagline, dynamic year, socials, back to top
    │   │   ├── ProjectCard.jsx # Showcase card with badges & details modal
    │   │   ├── ProjectModal.jsx # Detailed project popup with feature checklist
    │   │   ├── ResumeModal.jsx  # Resume preview and download modal
    │   │   └── ThemeToggle.jsx  # Dark/light mode switcher
    │   ├── context/
    │   │   ├── ThemeContext.jsx # Theme state persistence
    │   │   └── AuthContext.jsx  # Admin authentication session state
    │   ├── pages/
    │   │   ├── Home.jsx         # Main one-page portfolio assembly
    │   │   ├── AdminLogin.jsx   # /admin/login authentication page
    │   │   ├── AdminDashboard.jsx # /admin protected management dashboard
    │   │   └── NotFound.jsx     # 404 error page
    │   ├── sections/
    │   │   ├── HeroSection.jsx  # Intro headline, animated role text, visual IDE
    │   │   ├── AboutSection.jsx # BCA student details, objective, learning goals
    │   │   ├── SkillsSection.jsx # Skill cards with technical descriptions
    │   │   ├── ProjectsSection.jsx # Filterable gallery (GauConnect, Crypto, Portfolio)
    │   │   ├── EducationSection.jsx # Degree details, college, coursework
    │   │   ├── ResumeSection.jsx # PDF download banner & preview
    │   │   └── ContactSection.jsx # Form with validation and database storage
    │   ├── services/
    │   │   └── api.js           # Axios client with interceptors
    │   ├── styles/
    │   │   └── index.css        # Vanilla CSS design system
    │   ├── App.jsx              # Routing setup
    │   ├── main.jsx             # React entry point
    │   └── vite.config.js       # Vite config with API proxy to port 5000
    └── package.json
```

---

## ⚡ Quick Start Guide

### 1. Prerequisites
- **Node.js**: v18.0.0 or higher (v22.15.0 recommended). Check with:
  ```bash
  node -v
  ```
- **npm**: v9.0.0 or higher. Check with:
  ```bash
  npm -v
  ```

### 2. Installation
Install all dependencies across root, server, and client with a single command:
```bash
npm run install:all
```
*(Alternatively, run `npm install` inside the root, `server/`, and `client/` directories).*

### 3. Environment Configuration
The server includes a configured `server/.env` file. You can customize settings using `server/.env.example` as a template:

```env
PORT=5000
NODE_ENV=development
MONGODB_URI=mongodb://127.0.0.1:27017/bijoy_portfolio
USE_IN_MEMORY_DB=true
JWT_SECRET=super_secret_bijoy_portfolio_jwt_key_2026_dev_32chars
JWT_EXPIRES_IN=7d
CLIENT_URL=http://localhost:5173
CONTACT_RECEIVER_EMAIL=joychk9999@gmail.com
ADMIN_EMAIL=admin@bijoy.dev
ADMIN_PASSWORD=AdminPass2027!
```

> **Note on MongoDB**: If you don't have a local MongoDB service running, leaving `USE_IN_MEMORY_DB=true` enables a fast, zero-configuration in-memory database automatically! For persistence across server restarts, connect to MongoDB Atlas by providing your cluster URI in `MONGODB_URI` and setting `USE_IN_MEMORY_DB=false`.

### 4. Seed the Database
Populate initial profile information and initial projects (*GauConnect*, *Cryptocurrency Trading*, *Personal Portfolio*):
```bash
npm run seed
```

### 5. Create / Update Admin Account
Create your secure admin login credentials:
```bash
npm run create-admin
```
*(Uses the credentials in `.env` or interactively prompts you).*

### 6. Start Development Servers
Run both backend and frontend concurrently:
```bash
npm run dev
```

- **Frontend Public Portfolio**: [http://localhost:5173](http://localhost:5173)
- **Admin Portal**: [http://localhost:5173/admin](http://localhost:5173/admin)
- **Admin Login**: [http://localhost:5173/admin/login](http://localhost:5173/admin/login)
- **Backend API**: [http://localhost:5000/api/health](http://localhost:5000/api/health)

---

## 🧪 Testing

### Automated Backend Tests
Run the automated test suite testing health, projects, validation, auth, and protected routes:
```bash
npm run test:server
```
All 9 critical test suites execute and report passing assertions.

### Manual Verification Checklist
1. **Navigation**: Click each navbar link (`Home`, `About`, `Skills`, `Projects`, `Education`, `Resume`, `Contact`) and verify smooth scrolling.
2. **Theme Switcher**: Click the Sun/Moon icon in the navbar. Verify transition between futuristic dark mode and crisp light mode. Refresh the page to confirm persistence.
3. **Project Details**: Click "Learn More" on GauConnect, Crypto Trading, or Portfolio. Verify the modal opens with key features and technology chips.
4. **Category Filtering**: Click "All", "Frontend", and "Full Stack" filters in the Projects section.
5. **Resume Download**: Click "Download Resume" in the Hero or Resume sections. Verify the `Bijoy_Chakma_Resume.pdf` file opens/downloads cleanly.
6. **Contact Submission**:
   - Submit an empty form to verify frontend validation warnings.
   - Enter a valid name, email, subject, and message. Click "Submit Message".
   - Confirm the success message displays and the fields reset.
7. **Admin Portal**:
   - Visit [http://localhost:5173/admin](http://localhost:5173/admin) (redirects to `/admin/login`).
   - Enter `admin@bijoy.dev` and `AdminPass2027!`.
   - Access the dashboard overview.
   - Click "Contact Inquiries" tab to inspect the message you submitted.
   - Mark the message as "Read" or "Replied".
   - Click "Projects Management" to create, edit, or delete a project.
   - Click "Profile & Settings" to update social links or biography.
   - Click "Logout" to end the session.

---

## 🔒 Security Measures

- **No Hardcoded Passwords**: Admin accounts are created strictly via one-time script with `bcrypt` (12 rounds) password hashing.
- **JWT Protection**: Public routes are decoupled from admin endpoints; all modifications require valid bearer/cookie tokens.
- **Rate Limiting**: Protects against brute-force logins and contact form spam.
- **Helmet**: Enforces HTTP security headers.
- **CORS**: Restricts API calls to permitted frontend origins.
- **Honeypot Anti-Spam**: Invisible bot trap field protects the contact endpoint.

---

## 📦 Production Build & Deployment

### Build Client Bundle
```bash
npm run build:client
```
Generates production-optimized static files in `client/dist/`.

### Deployment Recommendations
1. **Frontend**: Deploy `client/dist/` to **Vercel**, **Netlify**, or **Cloudflare Pages**.
2. **Backend**: Deploy `server/` to **Render**, **Railway**, or **Fly.io**.
3. **Database**: Create a free M0 cluster on **MongoDB Atlas** and set `MONGODB_URI` in server environment variables.

---

## 👤 Personal Information
- **Name**: Bijoy Chakma
- **Role**: BCA Student | Aspiring Frontend Developer
- **College**: Akash Global College of Management and Science
- **Expected Graduation**: 2027
- **Experience**: Fresher
- **Email**: [joychk9999@gmail.com](mailto:joychk9999@gmail.com)
- **Social Handle**: `@bijoy.ftbl`
