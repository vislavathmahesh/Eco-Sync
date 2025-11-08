# 🌿 EcoSync - Local Waste Management Tracker

<div align="center">

[![React](https://img.shields.io/badge/React-18.2.0-61dafb?logo=react)](https://reactjs.org/)
[![Flask](https://img.shields.io/badge/Flask-3.0.0-000000?logo=flask)](https://flask.palletsprojects.com/)
[![Supabase](https://img.shields.io/badge/Supabase-PostgreSQL-3ECF8E?logo=supabase)](https://supabase.com/)

**A full-stack web application for citizen complaint reporting, waste management task tracking, and community engagement.**

[Features](#-features) • [Installation](#-installation) • [Tech Stack](#-tech-stack) • [Contributing](#-contributing)

</div>

---

## 🌍 Overview

**EcoSync** connects citizens, municipal staff, and administrators to streamline waste management complaint reporting, task management, and community engagement. Built with React, Flask, and Supabase, it features real-time updates, gamification, and an eco-themed UI.

### Key Capabilities

- **Citizen Portal**: Report issues with media uploads, track progress, earn rewards
- **Staff Dashboard**: Manage tasks, upload resolution photos, update status
- **Admin Panel**: Assign tasks, view analytics, detect duplicates, manage zones
- **Community Forum**: Discussion threads with voting and comments
- **Gamification**: Points, badges, and leaderboards

---

## ✨ Features

### 👤 Citizens
- Report issues with GPS location, photos/videos
- Real-time status tracking and notifications
- Rate staff performance after resolution
- Earn points and unlock achievements
- Community forum participation
- Live weather and air quality widgets

### 👨‍💼 Staff
- View assigned and available tasks
- Update task status (assigned → in-progress → resolved)
- Upload resolution photos to document work
- Claim tasks from shared pool

### 🔧 Admins
- Centralized complaint management
- Assign tasks to staff or make available to all
- Analytics dashboard with trends and metrics
- Duplicate detection using Haversine distance
- Zone management for service areas

---

## 🛠️ Tech Stack

**Frontend:** React 18, Vite, React Router, Tailwind CSS, shadcn/ui, Framer Motion, GSAP, Zustand, Recharts

**Backend:** Flask 3.0, Flask-CORS, Supabase Python Client, Gunicorn

**Database & Services:** Supabase (PostgreSQL, Auth, Storage), OpenWeatherMap API, Nominatim (OSM)

---

## 📦 Installation

### Prerequisites

Before you begin, ensure you have the following installed:

- **Node.js** (v18 or higher) - [Download](https://nodejs.org/)
- **Python** (v3.10 or higher) - [Download](https://www.python.org/)
- **npm** or **yarn** - Comes with Node.js
- **Git** - [Download](https://git-scm.com/)
- **Supabase Account** - [Sign up](https://supabase.com/)

### Backend Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/ecosync.git
   cd ecosync
   ```

2. **Navigate to backend directory**
   ```bash
   cd backend
   ```

3. **Create virtual environment**
   ```bash
   # Windows
   python -m venv venv
   venv\Scripts\activate

   # macOS/Linux
   python3 -m venv venv
   source venv/bin/activate
   ```

4. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

5. **Create `.env` file**
   ```bash
   cp .env.example .env
   ```

6. **Configure environment variables** (see [Environment Variables](#-environment-variables))

7. **Run the development server**
   ```bash
   # Development
   python run.py

   # Production (with Gunicorn)
   gunicorn -w 4 -b 0.0.0.0:5000 app:app
   ```

   Backend runs on `http://localhost:5000`

### Frontend Setup

1. **Navigate to frontend directory**
   ```bash
   cd ../frontend
   ```

2. **Install dependencies**
   ```bash
   npm install
   # or
   yarn install
   ```

3. **Create `.env` file**
   ```bash
   cp .env.example .env
   ```

4. **Configure environment variables** (see [Environment Variables](#-environment-variables))

5. **Run the development server**
   ```bash
   npm run dev
   # or
   yarn dev
   ```

   Frontend runs on `http://localhost:5173`

### Database Setup

1. **Create a Supabase project**
   - Go to [Supabase Dashboard](https://app.supabase.com/)
   - Click "New Project"
   - Note your **Project URL** and **Anon Key**

2. **Run database migrations**
   - Open the SQL Editor in Supabase Dashboard
   - Run scripts in order from `database/` folder:
     ```sql
     -- 1. Core schema
     database/setup.sql

     -- 2. Forum feature
     database/forum-schema.sql

     -- 3. Staff feedback
     database/add-staff-feedback-column.sql

     -- 4. Resolution photos
     database/add-resolution-media-urls.sql

     -- 5. RLS policies
     database/fix-rls-policies.sql
     database/fix-admin-complaints-rls.sql
     database/fix-users-rls-policy.sql
     ```

3. **Create storage buckets**
   - In Supabase Dashboard → Storage
   - Create bucket: `complaint-media` (public)
   - Set policies to allow authenticated uploads

4. **Create test users** (optional)
   ```sql
   -- Run this in SQL Editor
   database/create-staff-user.sql
   database/create-test-complaints.sql
   ```

5. **Set up Row Level Security (RLS)**
   - All policies are included in the migration files
   - Verify policies are active in Authentication → Policies

---

## 🔐 Environment Variables

### Backend (`.env`)

```env
# Supabase Configuration
SUPABASE_URL=https://your-project.supabase.co
SUPABASE_KEY=your-service-role-key-here

# Flask Configuration
FLASK_ENV=development
FLASK_DEBUG=True
SECRET_KEY=your-secret-key-here

# Server Configuration
PORT=5000
HOST=0.0.0.0
```

### Frontend (`.env`)

```env
# Supabase Configuration
VITE_SUPABASE_URL=https://your-project.supabase.co
VITE_SUPABASE_ANON_KEY=your-anon-key-here

# API Configuration
VITE_API_URL=http://localhost:5000/api

# External APIs
VITE_OPENWEATHER_API_KEY=your-openweather-api-key
```

> **Security Note**: Never commit `.env` files to version control. Use `.env.example` as a template.

---

## 🚀 Usage

### Creating Test Users

Register at `http://localhost:5173/register`, then update roles in Supabase SQL Editor:

```sql
UPDATE users SET role = 'admin' WHERE email = 'admin@test.com';
UPDATE users SET role = 'staff' WHERE email = 'staff@test.com';
```

### Quick Start

**Citizen:** Report issue → Upload media → Track status → Rate staff after resolution

**Staff:** View tasks → Claim/Start task → Upload resolution photos → Mark resolved

**Admin:** Assign tasks → View analytics → Detect duplicates → Manage zones

---

## 📡 API Documentation

### Base URL
```
http://localhost:5000/api
```

### Authentication
Protected endpoints require JWT token: `Authorization: Bearer <token>`

### Key Endpoints

**Complaints**
- `GET /complaints` - List with filters (user_id, status, category)
- `POST /complaints` - Create complaint
- `PUT /complaints/:id` - Update (Staff/Admin)
- `GET /complaints/stats` - Statistics

**Users**
- `GET /users` - List users (Admin)
- `GET /users/:id/stats` - User statistics

**Analytics**
- `GET /analytics/overview` - System metrics (Admin)
- `GET /analytics/trends` - Complaint trends (Admin)

**Response Format:**
```json
{
  "success": true,
  "data": { },
  "message": "Operation successful"
}
```

---

## 🗄️ Database Schema

**Key Tables:**

- `users` - User profiles with role (citizen/staff/admin), points, level
- `complaints` - Issues with location, status, media, resolution photos, staff feedback
- `forum_topics` - Community discussions with views and upvotes
- `zones` - Service areas with staff assignments

See `database/schema.md` for complete schema documentation.

---

## � Key Features

- **Duplicate Detection**: Haversine formula to find nearby complaints within configurable radius
- **Resolution Photos**: Staff upload before/after photos, visible to admin and citizens
- **Staff Feedback**: Citizens rate staff with 1-5 stars and optional comments
- **Community Forum**: Threaded discussions with voting and view tracking
- **Gamification**: Points (10-15 per report), badges, levels, leaderboard
- **Real-time Updates**: Supabase subscriptions for instant complaint notifications
- **Weather & AQI**: Live Hyderabad weather and air quality with LocalStorage caching

## ⚡ Performance

- Lazy loading images, code splitting, LocalStorage caching
- Parallel API queries with Promise.all
- GIN indexes on arrays, RLS policies for security
- Hardware-accelerated animations with GSAP

## 🔒 Security

- **JWT Authentication**: Supabase Auth with role-based access control
- **Row Level Security (RLS)**: Policy-based data access in PostgreSQL
- **Input Validation**: Backend validates all inputs, 10MB file limit
- **CORS**: Whitelist origins in Flask
- **SQL Injection Prevention**: Parameterized queries

RLS policies enforce citizens see only their complaints, staff update assigned tasks, and admins have full access.

## 🌐 Deployment

**Frontend (Vercel/Netlify):**
```bash
cd frontend && vercel --prod
```

**Backend (Railway/Render/Heroku):**
```bash
cd backend && railway up
```

See [docs/DEPLOYMENT.md](docs/DEPLOYMENT.md) for detailed instructions.

## 🤝 Contributing

Contributions are welcome! Please follow [Conventional Commits](https://www.conventionalcommits.org/).

1. Fork the repository
2. Create feature branch: `git checkout -b feature/amazing-feature`
3. Commit changes: `git commit -m "feat: add amazing feature"`
4. Push and create PR

See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed guidelines.

---

## 📞 Contact

**Contributors:** [@Dr-Venom29](https://github.com/Dr-Venom29) • [@vislavathmahesh](https://github.com/vislavathmahesh)

**Project:** [https://github.com/vislavathmahesh/Eco-Sync](https://github.com/vislavathmahesh/Eco-Sync)

---

## 🗺️ Roadmap

**Phase 1** ✅ - Core features, forum, gamification, resolution photos  
**Phase 2** 🚧 - Mobile app, push notifications, advanced analytics  
**Phase 3** 🔮 - AI categorization, IoT integration

---

<div align="center">

**Made with 💚 for a cleaner future**

⭐ [Star this project](https://github.com/vislavathmahesh/Eco-Sync) • [Report Bug](https://github.com/vislavathmahesh/Eco-Sync/issues)

</div>
