# 🏢 CA Firm Internal Web App — Service Management System

An internal web application for a CA firm to manage employee skills, services, and learning resources.

---

## 🔐 Test Credentials

| Role | Email | Password |
|------|-------|----------|
| **Admin** | admin@gmail.com | admin123 |
| **Employee** | aditya@gmail.com | 123456 |

> **Note:** Login is handled via Firebase Authentication.

---

## 🗺️ Route Map

| Route | Page | Access |
|-------|------|--------|
| `/login` | Login | Public |
| `/register` | Register | Public |
| `/dashboard` | Dashboard | All Employees |
| `/profile` | My Profile | All Employees |
| `/services` | Services List | All Employees |
| `/services/:id` | Service Detail | All Employees |
| `/employees` | Employee Directory | All Employees |
| `/learning` | Want to Learn | All Employees |
| `/resources` | Resources / Lectures | All Employees |
| `/admin` | Admin Dashboard | Admin Only |

---

## 📁 Project Structure

```
ca-internal-app/
├── frontend/
│   ├── public/
│   └── src/
│       ├── components/
│       │   ├── Navbar.jsx
│       │   ├── Sidebar.jsx
│       │   └── ProtectedRoute.jsx
│       ├── context/
│       │   └── AuthContext.jsx
│       ├── hooks/
│       │   └── useAuth.js
│       ├── pages/
│       │   ├── auth/
│       │   │   ├── Login.jsx
│       │   │   └── Register.jsx
│       │   ├── dashboard/
│       │   │   └── Dashboard.jsx
│       │   ├── profile/
│       │   │   └── Profile.jsx
│       │   ├── services/
│       │   │   ├── Services.jsx
│       │   │   └── ServiceDetail.jsx
│       │   ├── employees/
│       │   │   └── Employees.jsx
│       │   ├── learning/
│       │   │   └── Learning.jsx
│       │   ├── resources/
│       │   │   └── Resources.jsx
│       │   └── admin/
│       │       └── AdminDashboard.jsx
│       ├── services/
│       │   └── api.js
│       ├── utils/
│       │   └── firebaseConfig.js
│       ├── App.jsx
│       ├── main.jsx
│       └── index.css
│
└── backend/
    ├── server.js
    ├── seedAdmin.js
    ├── .env
    ├── .env.example
    ├── config/
    │   ├── db.js
    │   └── firebase.js
    ├── middleware/
    │   └── authMiddleware.js
    ├── models/
    │   └── schema.sql
    ├── controllers/
    │   ├── authController.js
    │   ├── userController.js
    │   ├── serviceController.js
    │   ├── employeeController.js
    │   ├── learningController.js
    │   ├── resourceController.js
    │   └── adminController.js
    ├── routes/
    │   ├── authRoutes.js
    │   ├── userRoutes.js
    │   ├── serviceRoutes.js
    │   ├── employeeRoutes.js
    │   ├── learningRoutes.js
    │   ├── resourceRoutes.js
    │   └── adminRoutes.js
    └── utils/
        └── driveUpload.js
```

---

## 🛠️ Tech Stack

### Frontend

| Tool | Purpose |
|------|---------|
| React 18 | UI development |
| Vite | Fast build tool |
| Tailwind CSS | Styling |
| Axios | API calls |
| React Router v6 | Client-side routing |
| Firebase Auth | Login / Signup |
| Cloudinary | Profile photo upload |

### Backend

| Tool | Version | Purpose |
|------|---------|---------|
| Node.js | 18.x+ | Runtime |
| Express.js | 4.x | API Framework |
| PostgreSQL | 15.x | Main Database |
| Neon | — | Serverless PostgreSQL Hosting |
| Firebase Admin SDK | 12.x | Token Verification |
| pg | 8.x | PostgreSQL Client |
| dotenv | 16.x | Environment Variables |
| cors | 2.x | Cross-Origin Requests |

---

## 🏗️ Architecture

```
React (Frontend)  →  Express API (Backend)  →  PostgreSQL via Neon (Database)

Firebase  →  Auth + File Storage (separate from main DB)
Cloudinary  →  Profile photo storage
```

---

## 👥 User Roles

| Role | Permissions |
|------|------------|
| **Employee** | Add/edit skills, mark learning interests, browse services & resources |
| **Admin** | Full control — add, edit, delete + user management + stats dashboard |

---

## ⚙️ Setup & Run

### 1. Clone the Repo

```bash
git clone <your-repo-url>
cd ca-internal-app
```

---

### 2. Frontend Setup

```bash
cd frontend
npm install
```

Create `.env` in the `frontend/` folder:

```env
VITE_API_BASE_URL=http://localhost:5000/api
VITE_FIREBASE_API_KEY=your_firebase_api_key
VITE_FIREBASE_AUTH_DOMAIN=your_project.firebaseapp.com
VITE_FIREBASE_PROJECT_ID=your_project_id
VITE_FIREBASE_STORAGE_BUCKET=your_project.appspot.com
VITE_FIREBASE_MESSAGING_SENDER_ID=your_sender_id
VITE_FIREBASE_APP_ID=your_app_id
VITE_CLOUDINARY_CLOUD_NAME=your_cloudinary_cloud_name
VITE_CLOUDINARY_UPLOAD_PRESET=your_upload_preset
```

Start frontend:

```bash
npm run dev
# → http://localhost:3000
```

---

### 3. Backend Setup

```bash
cd backend
npm install
```

Create `.env` in the `backend/` folder:

```env
PORT=5000
NODE_ENV=development

# Neon PostgreSQL (no quotes around the URL)
DATABASE_URL=postgresql://user:password@ep-xxx.neon.tech/neondb?sslmode=require

# JWT
JWT_SECRET=your_super_secret_key

# Firebase Admin SDK
FIREBASE_PROJECT_ID=your_project_id
FIREBASE_PRIVATE_KEY="-----BEGIN PRIVATE KEY-----\n...\n-----END PRIVATE KEY-----\n"
FIREBASE_CLIENT_EMAIL=firebase-adminsdk@your_project.iam.gserviceaccount.com

# CORS
FRONTEND_URL=http://localhost:3000
```

> **How to get Firebase Admin credentials:**
> Firebase Console → Project Settings → Service Accounts → Generate New Private Key → download JSON → copy values into `.env`

Start backend:

```bash
npm start
# → http://localhost:5000
```

---

### 4. Database Setup (One-time)

1. Go to [console.neon.tech](https://console.neon.tech) → your project → **SQL Editor**
2. Copy the contents of `backend/models/schema.sql`
3. Paste into SQL Editor and click **Run**

---

### 5. Create Admin Account

After registering in the app, run this script to promote a user to Admin:

```bash
cd backend
node seedAdmin.js
```

Follow the prompts — enter the email you want to make Admin and confirm with `yes`.

Alternatively, run this directly in Neon SQL Editor:

```sql
UPDATE users SET role = 'admin' WHERE email = 'admin@gmail.com';
```

---

## 🗄️ Database Schema

### `users`
| Column | Type | Notes |
|--------|------|-------|
| id | SERIAL PK | Auto increment |
| firebase_uid | VARCHAR(128) UNIQUE | Primary identifier |
| email | VARCHAR(255) UNIQUE | |
| full_name | VARCHAR(255) | |
| role | VARCHAR(20) | `employee` or `admin` (default: employee) |
| designation | VARCHAR(255) | e.g. CA, Article Assistant |
| department | VARCHAR(255) | |
| phone | VARCHAR(20) | |
| avatar_url | TEXT | Cloudinary URL |
| created_at | TIMESTAMP | |
| updated_at | TIMESTAMP | |

### `services`
| Column | Type | Notes |
|--------|------|-------|
| id | SERIAL PK | |
| title | VARCHAR(255) | Service name |
| description | TEXT | |
| category | VARCHAR(100) | e.g. Audit, GST, ITR |
| created_by | VARCHAR(128) FK→users | firebase_uid |
| created_at | TIMESTAMP | |

### `employee_services` — who knows what
| Column | Type | Notes |
|--------|------|-------|
| firebase_uid | VARCHAR FK→users | |
| service_id | INT FK→services | |
| proficiency | VARCHAR(50) | beginner / intermediate / expert |
| UNIQUE | (firebase_uid, service_id) | No duplicates |

### `learning_interests` — who wants to learn what
| Column | Type | Notes |
|--------|------|-------|
| firebase_uid | VARCHAR FK→users | |
| service_id | INT FK→services | |
| status | VARCHAR(50) | interested / in_progress / completed |
| UNIQUE | (firebase_uid, service_id) | No duplicates |

### `resources`
| Column | Type | Notes |
|--------|------|-------|
| title | VARCHAR(255) | |
| url | TEXT | YouTube / Drive / External |
| resource_type | VARCHAR(50) | video / article / pdf / other |
| pdf_url | TEXT | Cloudinary PDF URL |
| service_id | INT FK→services | Optional |
| added_by | VARCHAR FK→users | firebase_uid |

---

## 🔌 API Reference

### Auth — `/api/auth`
| Method | Endpoint | Auth | Description |
|--------|----------|------|-------------|
| POST | `/register` | Public | Save Firebase user to DB |
| GET | `/me` | Token | Get current user's DB record |

### Users — `/api/users`
| Method | Endpoint | Auth | Description |
|--------|----------|------|-------------|
| GET | `/profile` | Token | Full profile with skills + learning |
| PUT | `/profile` | Token | Update name, designation, avatar, etc. |

### Services — `/api/services`
| Method | Endpoint | Auth | Description |
|--------|----------|------|-------------|
| GET | `/` | Token | All services |
| GET | `/:id` | Token | Single service + employees + resources |
| POST | `/` | Token | Create service |
| PUT | `/:id` | Token | Update service |
| DELETE | `/:id` | Admin | Delete service |

### Employees — `/api/employees`
| Method | Endpoint | Auth | Description |
|--------|----------|------|-------------|
| GET | `/` | Token | All employees with skills |
| GET | `/:uid` | Token | Single employee profile |
| POST | `/services` | Token | Add skill |
| POST | `/services/custom` | Token | Add custom skill |
| DELETE | `/services/:serviceId` | Token | Remove skill |

### Learning — `/api/learning`
| Method | Endpoint | Auth | Description |
|--------|----------|------|-------------|
| GET | `/` | Token | My learning interests |
| GET | `/all` | Admin | All employees' learning interests |
| POST | `/` | Token | Add learning interest |
| POST | `/custom` | Token | Add custom learning interest |
| PUT | `/:serviceId` | Token | Update status |
| DELETE | `/:serviceId` | Token | Remove interest |

### Resources — `/api/resources`
| Method | Endpoint | Auth | Description |
|--------|----------|------|-------------|
| GET | `/` | Token | All resources (filter by `?service_id=`) |
| POST | `/` | Token | Add resource |
| DELETE | `/:id` | Admin | Delete resource |

### Admin — `/api/admin`
| Method | Endpoint | Auth | Description |
|--------|----------|------|-------------|
| GET | `/stats` | Admin | Dashboard stats |
| GET | `/users` | Admin | All users |
| PUT | `/users/:uid/role` | Admin | Change user role |
| DELETE | `/users/:uid` | Admin | Delete user |

---

## 🔒 Middleware

### `verifyToken`
Reads `Authorization: Bearer <token>`, verifies Firebase ID Token, attaches `req.user` to request.

### `isAdmin`
Used after `verifyToken`. Checks `users.role = 'admin'` in DB. Returns 403 if not admin.

```js
router.delete('/:id', verifyToken, isAdmin, deleteService);
```

---

## 📌 Important Rules

1. Never use Firebase as the main database — only Auth + Storage
2. All DB reads/writes go through the Express API
3. Store only URLs in the database, never raw files
4. Use `firebase_uid` as the user identifier across all tables
5. Always protect routes with `verifyToken`; admin routes also need `isAdmin`
6. Never put single quotes around `DATABASE_URL` in `.env`