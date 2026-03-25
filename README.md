# 🚀 User Management Backend API

A RESTful backend API built with **Node.js**, **Express**, and **MongoDB** (Mongoose) for managing users. It supports creating and fetching user records with auto-generated avatar images.

---

## 📁 Project Structure

```
backend/
├── config/
│   └── database.js          # MongoDB connection setup
├── controller/
│   ├── createUser.js         # Controller to create a new user
│   └── getUsers.js           # Controller to fetch all users
├── models/
│   └── User.js               # Mongoose User schema/model
├── routes/
│   └── user.js               # API route definitions
├── .env.example              # Example environment variables
├── .gitignore                # Git ignore rules
├── index.js                  # App entry point
├── package.json              # Project metadata & dependencies
└── package-lock.json         # Dependency lock file
```

---

## 🛠️ Tech Stack

| Technology | Purpose              |
| ---------- | -------------------- |
| Node.js    | Runtime environment  |
| Express.js | Web framework        |
| MongoDB    | NoSQL database       |
| Mongoose   | MongoDB ODM          |
| dotenv     | Environment config   |
| CORS       | Cross-origin support |
| Nodemon    | Dev auto-restart     |

---

## ⚙️ Installation & Setup

### 1. Clone the repository

```bash
git clone <your-repo-url>
cd backend
```

### 2. Install dependencies

```bash
npm install
```

### 3. Configure environment variables

Create a `.env` file in the project root based on `.env.example`:

```env
PORT=4000
DATABASE_URL=<your-mongodb-connection-string>
```

### 4. Start the server

**Development** (with auto-reload):

```bash
npm run dev
```

**Production**:

```bash
npm start
```

The server will start on `http://localhost:4000` (or the port specified in `.env`).

---

## 📡 API Endpoints

Base URL: `/api/v1`

### `GET /`

Health check — confirms the server is running.

**Response:**

```html
<h1>Backend is Running and this is '/' Route</h1>
```

---

### `POST /api/v1/createUser`

Create a new user.

**Request Body** (`application/json`):

```json
{
  "name": "John Doe",
  "email": "john@example.com",
  "title": "Software Engineer",
  "department": "Engineering",
  "role": "Developer"
}
```

> **Note:** The `image` field is auto-generated using the [DiceBear Initials API](https://www.dicebear.com/) based on the user's name.

**Success Response** (`201`):

```json
{
  "status": 201,
  "message": "User created successfully",
  "data": {
    "_id": "...",
    "name": "John Doe",
    "email": "john@example.com",
    "title": "Software Engineer",
    "department": "Engineering",
    "role": "Developer",
    "image": "https://api.dicebear.com/5.x/initials/svg?seed=John Doe"
  }
}
```

**Error Response** (`400` — missing fields):

```json
{
  "status": 400,
  "message": "Please fill all fields"
}
```

---

### `GET /api/v1/getallUsers`

Fetch all users.

**Success Response** (`200`):

```json
{
  "success": true,
  "data": [
    {
      "_id": "...",
      "name": "John Doe",
      "email": "john@example.com",
      "title": "Software Engineer",
      "department": "Engineering",
      "role": "Developer",
      "image": "https://api.dicebear.com/5.x/initials/svg?seed=John Doe"
    }
  ]
}
```

---

## 📦 User Model Schema

| Field        | Type     | Required | Constraints       |
| ------------ | -------- | -------- | ----------------- |
| `name`       | `String` | ✅       | —                 |
| `email`      | `String` | ✅       | Must be unique    |
| `title`      | `String` | ✅       | —                 |
| `department` | `String` | ✅       | Max 20 characters |
| `role`       | `String` | ✅       | —                 |
| `image`      | `String` | ✅       | Auto-generated    |

---

## 🔧 Scripts

| Command         | Description                            |
| --------------- | -------------------------------------- |
| `npm start`     | Start the server with Node.js          |
| `npm run dev`   | Start the server with Nodemon (dev)    |

---

## 🌐 CORS Configuration

CORS is enabled for all origins (`*`), allowing any frontend to communicate with this API.

---

## 📄 License

ISC
