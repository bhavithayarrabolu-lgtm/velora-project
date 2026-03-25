# ✦ Velora – Intelligent Web Application

A full-stack notes management app with user authentication built with **React**, **Node.js/Express**, and **MongoDB**.

---

## 📁 Project Structure

```
velora/
├── backend/
│   ├── config/         # MongoDB connection
│   ├── controllers/    # Auth & Notes logic
│   ├── middleware/     # JWT auth middleware
│   ├── models/         # Mongoose schemas (User, Note)
│   ├── routes/         # Express route definitions
│   ├── .env            # Environment variables
│   └── server.js       # Entry point
└── frontend/
    └── src/
        ├── api/        # Axios instance
        ├── components/ # Navbar, PrivateRoute
        ├── context/    # AuthContext (global state)
        └── pages/      # Login, Register, Dashboard
```

---

## ⚙️ Prerequisites

- [Node.js](https://nodejs.org/) v18+
- [MongoDB](https://www.mongodb.com/try/download/community) running locally on port 27017
  - Or use a free [MongoDB Atlas](https://www.mongodb.com/atlas) cluster

---

## 🚀 Running Locally

### 1. Start MongoDB
Make sure MongoDB is running:
```bash
# Windows (if installed as a service)
net start MongoDB

# Or start manually
mongod
```

### 2. Start the Backend
```bash
cd backend
npm install
npm run dev        # uses nodemon for hot-reload
# Server runs on http://localhost:5000
```

### 3. Start the Frontend
Open a **new terminal**:
```bash
cd frontend
npm install        # already done if you followed setup
npm start
# App opens at http://localhost:3000
```

---

## 🔐 Environment Variables (`backend/.env`)

| Variable        | Default Value                              | Description              |
|-----------------|--------------------------------------------|--------------------------|
| `PORT`          | `5000`                                     | Backend server port      |
| `MONGO_URI`     | `mongodb://localhost:27017/velora`         | MongoDB connection string |
| `JWT_SECRET`    | `velora_super_secret_jwt_key_2024`         | JWT signing secret       |
| `JWT_EXPIRES_IN`| `7d`                                       | Token expiry duration    |

> ⚠️ Change `JWT_SECRET` to a strong random string in production.

---

## 🌐 API Endpoints

### Auth
| Method | Endpoint              | Description              | Auth Required |
|--------|-----------------------|--------------------------|---------------|
| POST   | `/api/auth/register`  | Register new user        | No            |
| POST   | `/api/auth/login`     | Login & get JWT          | No            |
| GET    | `/api/auth/me`        | Get current user info    | Yes           |

### Notes
| Method | Endpoint              | Description              | Auth Required |
|--------|-----------------------|--------------------------|---------------|
| GET    | `/api/notes`          | Get all user notes       | Yes           |
| POST   | `/api/notes`          | Create a note            | Yes           |
| PUT    | `/api/notes/:id`      | Update a note            | Yes           |
| DELETE | `/api/notes/:id`      | Delete a note            | Yes           |

---

## ☁️ Deploy on AWS EC2

1. Launch an EC2 instance (Ubuntu 22.04, t2.micro for free tier)
2. Install Node.js and MongoDB on the instance
3. Clone/upload your project files
4. Set up environment variables in `backend/.env`
5. Use **PM2** to keep the backend running:
   ```bash
   npm install -g pm2
   cd backend && pm2 start server.js --name velora-api
   ```
6. Build the React frontend and serve with Nginx:
   ```bash
   cd frontend && npm run build
   # Copy build/ to Nginx web root
   ```
7. Configure Nginx to proxy `/api` requests to `localhost:5000`

---

## ✨ Features

- ✅ User registration with hashed passwords (bcrypt)
- ✅ JWT-based login with persistent sessions
- ✅ Protected dashboard route
- ✅ Create, edit, delete, and pin notes
- ✅ Search notes in real-time
- ✅ Responsive dark-themed UI
- ✅ Form validation with error messages
