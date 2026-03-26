# 💃 Elite Dance Academy — Kakinada

**Master the art of movement. 9 world-class styles, 1 destination.**

[![Live on Railway](https://img.shields.io/badge/Live%20on-Railway-6366f1?style=for-the-badge&logo=railway&logoColor=white)](https://web-production-93d2c.up.railway.app)
[![Status](https://img.shields.io/website?url=https%3A%2F%2Fweb-production-93d2c.up.railway.app&style=for-the-badge&label=Status&up_message=Online&down_message=Offline&up_color=22c55e&down_color=ef4444)](https://web-production-93d2c.up.railway.app)
[![Python](https://img.shields.io/badge/Python-3.x-3b82f6?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org)
[![Flask](https://img.shields.io/badge/Flask-Backend-black?style=for-the-badge&logo=flask&logoColor=white)](https://flask.palletsprojects.com)
[![Supabase](https://img.shields.io/badge/Supabase-Database%20%26%20Auth-3ecf8e?style=for-the-badge&logo=supabase&logoColor=white)](https://supabase.com)

🌐 **[https://web-production-93d2c.up.railway.app](https://web-production-93d2c.up.railway.app)**

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Tech Stack](#%EF%B8%8F-tech-stack)
- [Project Structure](#-project-structure)
- [Local Setup](#-local-setup)
- [Supabase Setup](#%EF%B8%8F-supabase-setup)
- [Google OAuth Setup](#-google-oauth-setup)
- [API Endpoints](#-api-endpoints)
- [Dance Styles & Fees](#-dance-styles--fees)
- [Deployment](#-deployment-railway)
- [Email Setup](#-email-setup-brevo)
- [Contact](#-contact)
- [License](#-license)

---

## 🎯 Overview

Elite Dance Academy is a full-stack web application for a dance studio based in Kakinada, Andhra Pradesh. It allows students to browse 9 dance styles, sign in with Google, enroll in classes, and request mentor sessions — all from a single-page interface.

| Section | Feature |
|---|---|
| 🎬 Hero | Full-screen background with animated headline |
| 🩰 Dance Grid | 9 interactive style cards with detail modals |
| 🔐 Auth | Google Sign-In via Supabase OAuth |
| 📋 Enroll | Authenticated student registration form |
| ⭐ Reviews | Auto-scrolling testimonials marquee |
| 📬 Contact | Mentor / trial class request form |

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Backend | Python · Flask · Flask-CORS · Gunicorn |
| Database | Supabase (PostgreSQL) |
| Auth | Supabase Auth — Google OAuth |
| Email | Brevo Transactional API |
| Frontend | HTML · Tailwind CSS · Vanilla JS |
| Deployment | Railway |

**Language breakdown:** HTML 79% · Python 21%

---

## 📁 Project Structure

```
DANCE-ACADEMY-IN-A-CITY/
├── app.py              # Flask backend — routes, Supabase, Brevo email
├── templates/
│   └── index.html      # Single-page frontend (Tailwind + Supabase JS)
├── static/             # Images: hero, background, all 9 dance styles
├── Procfile            # Railway/Gunicorn process definition
├── requirements.txt    # Python dependencies
├── runtime.txt         # Python version pin
└── README.md
```

---

## 🚀 Local Setup

### 1. Clone the Repository

```bash
git clone https://github.com/24A31A05EH/DANCE-ACADEMY-IN-A-CITY.git
cd DANCE-ACADEMY-IN-A-CITY
```

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

### 3. Configure Environment Variables

Create a `.env` file in the root directory. **Never commit this file.**

```env
SUPABASE_URL=https://your-project.supabase.co
SUPABASE_KEY=your-supabase-anon-key
BREVO_API_KEY=your-brevo-api-key
BREVO_SENDER_EMAIL=admissions@elitedance.com
ADMIN_EMAIL=admin@elitedance.com
PORT=5000
```

> ⚠️ Make sure `.env` is listed in your `.gitignore` before pushing to GitHub.

### 4. Run the App

```bash
python app.py
```

Visit `http://localhost:5000` in your browser.

---

## 🗄️ Supabase Setup

Run the following SQL in your **Supabase SQL Editor**:

```sql
-- Student enrollments
CREATE TABLE enrollments (
  id               SERIAL PRIMARY KEY,
  name             TEXT NOT NULL,
  email            TEXT NOT NULL,
  phone            TEXT NOT NULL,
  age              INTEGER,
  dance_style      TEXT,
  experience_level TEXT,
  created_at       TIMESTAMPTZ DEFAULT NOW()
);

-- Mentor / trial class requests
CREATE TABLE mentor_requests (
  id         SERIAL PRIMARY KEY,
  name       TEXT NOT NULL,
  email      TEXT NOT NULL,
  message    TEXT NOT NULL,
  created_at TIMESTAMPTZ DEFAULT NOW()
);
```

Then enable **Row Level Security (RLS)** and configure policies as needed.

---

## 🔐 Google OAuth Setup

1. Go to **Supabase → Authentication → Providers → Google**
2. Enable the Google provider
3. Paste your **Google OAuth Client ID & Secret**
4. Set the redirect URL to your live domain:

```
https://web-production-93d2c.up.railway.app/
```

---

## 🌐 API Endpoints

| Method | Endpoint | Description | Auth Required |
|---|---|---|---|
| `GET` | `/` | Serve the frontend | No |
| `GET` | `/test-supabase` | Test DB connection | No |
| `GET` | `/test-email` | Send a Brevo test email | No |
| `POST` | `/enroll` | Submit enrollment form | ✅ Bearer token |
| `POST` | `/mentor-request` | Submit mentor/trial request | No |

### POST `/enroll` — Request Body

```json
{
  "name":             "Priya Nair",
  "email":            "priya@example.com",
  "phone":            "9000012345",
  "age":              22,
  "dance_style":      "Bharatanatyam",
  "experience_level": "Beginner"
}
```

On success: saves to Supabase, sends a confirmation email to the student, and sends a notification to the admin.

### POST `/mentor-request` — Request Body

```json
{
  "name":    "Arjun Mehta",
  "email":   "arjun@example.com",
  "message": "I want to learn Hip Hop from scratch."
}
```

---

## 🩰 Dance Styles & Fees

| Style | Monthly Fee | Experience Levels |
|---|---|---|
| Bharatanatyam | ₹2,500 | Beginner → Advanced |
| Hip Hop | ₹3,000 | Beginner → Advanced |
| Kathak | ₹2,800 | Beginner → Advanced |
| Salsa | ₹3,500 | Beginner → Advanced |
| Contemporary | ₹3,200 | Beginner → Advanced |
| Ballet | ₹4,000 | Beginner → Advanced |
| Western | ₹3,000 | Beginner → Advanced |
| Kuchipudi | ₹2,500 | Beginner → Advanced |
| Freestyle | ₹2,800 | Beginner → Advanced |

---

## 🚢 Deployment (Railway)

This project is deployed on **Railway** using Gunicorn.

**`Procfile`** content:
```
web: gunicorn app:app
```

**To redeploy:**
1. Push to GitHub — Railway auto-deploys on every push to `main`
2. Set all environment variables under **Railway → Variables**
3. Railway reads the `Procfile` and starts Gunicorn automatically

---

## 📧 Email Setup (Brevo)

| Variable | Description |
|---|---|
| `BREVO_API_KEY` | Your Brevo API key |
| `BREVO_SENDER_EMAIL` | A **verified** sender address in Brevo |
| `ADMIN_EMAIL` | Admin address for new enrollment alerts |

> ⚠️ `BREVO_SENDER_EMAIL` must be verified in your Brevo account, otherwise emails will fail silently.

---

## ✅ Python Dependencies

```
flask
flask-cors
supabase
gunicorn
requests
```

Install all with:

```bash
pip install -r requirements.txt
```

---

## 📞 Contact

| | |
|---|---|
| 📍 Studio | Bhanugudi Junction, Kakinada |
| ✉️ Email | admissions@elitedance.com |
| 📞 Phone | +91 90000 12345 |

---

## 👤 Author

**24A31A05EH** — [GitHub Profile](https://github.com/24A31A05EH)

---

## 📄 License

Copyright © 2025 Elite Dance Academy. All rights reserved.

This source code is proprietary. No part of this project may be used, copied, modified, or distributed without explicit written permission from the author.
