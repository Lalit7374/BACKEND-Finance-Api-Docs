# 💰 Finance Dashboard API

**Live Docs:** https://backend-finance-dashboard-7dyj.onrender.com/
**Version:** v1.0

A role-based financial records backend built with **Node.js, Express, and MongoDB**.
Supports authentication, access control, financial tracking, and analytics.

---

# 🚀 Features

* 🔐 JWT Authentication (8-hour expiry)
* 👥 Role-Based Access Control (Viewer, Analyst, Admin)
* 📊 Financial Records Management
* 📈 Dashboard Analytics
* 🧾 Category & Trend Insights
* ♻️ Soft Deletes
* ⚡ RESTful API Design

---

# 🛠 Tech Stack

* Node.js + Express
* MongoDB + Mongoose
* JSON Web Tokens (JWT)

---

# ⚡ Quick Start

### 1. Start MongoDB

```bash
# macOS
brew services start mongodb-community

# Linux
sudo systemctl start mongod
```

---

### 2. Install dependencies & seed data

```bash
npm install
npm run seed
```

---

### 3. Start the server

```bash
npm start
```


* Docs: https://backend-finance-dashboard-7dyj.onrender.com/

---

# 🔐 Authentication Flow

All routes **except login** require a Bearer token:

```http
Authorization: Bearer <your_jwt_token>
```

* Tokens expire after **8 hours**
* Re-login to get a new token

---

# 👥 Roles & Permissions

| Action              | Viewer | Analyst | Admin |
| ------------------- | ------ | ------- | ----- |
| Login / Profile     | ✅      | ✅       | ✅     |
| View Records        | ✅      | ✅       | ✅     |
| Dashboard Analytics | ✅      | ✅       | ✅     |
| Create Records      | ❌      | ✅       | ✅     |
| Edit Own Records    | ❌      | ✅       | ✅     |
| Edit Any Record     | ❌      | ❌       | ✅     |
| Delete Records      | ❌      | ❌       | ✅     |
| Manage Users        | ❌      | ❌       | ✅     |

---

# 👤 Demo Users

| Name         | Email                                   | Password   | Role    |
| ------------ | --------------------------------------- | ---------- | ------- |
| Alice Admin  | [alice@demo.com](mailto:alice@demo.com) | admin123   | admin   |
| Bob Analyst  | [bob@demo.com](mailto:bob@demo.com)     | analyst123 | analyst |
| Carol Viewer | [carol@demo.com](mailto:carol@demo.com) | viewer123  | viewer  |

---

# 📬 Postman Testing Guide

### 1. Login

**POST** `/api/auth/login`

```json
{
  "email": "alice@demo.com",
  "password": "admin123"
}
```

➡️ Copy the JWT token from response

---

### 2. Create Environment

Variables:

```
base_url = http://localhost:3000
token = <your_token>
```

---

### 3. Set Authorization

* Type: Bearer Token
* Token: `{{token}}`

OR header:

```
Authorization: Bearer {{token}}
```

---

### 4. Set Headers (POST/PATCH)

```
Content-Type: application/json
```

---

# 🎯 Key Test Scenarios

| # | Request                       | Expected     |
| - | ----------------------------- | ------------ |
| 1 | POST /api/auth/login          | 200 + JWT    |
| 2 | GET /api/dashboard/summary    | 200 + totals |
| 3 | POST /api/records             | 201 created  |
| 4 | GET /api/records?type=expense | 200 filtered |
| 5 | POST /api/records (viewer)    | 403 denied   |

---

# 📌 API Endpoints

## 🔐 Auth

* `POST /api/auth/login`
* `GET /api/auth/me`

---

## 👥 Users (Admin only)

* `GET /api/users`
* `POST /api/users`
* `PATCH /api/users/:id`
* `DELETE /api/users/:id`

---

## 💸 Financial Records

* `GET /api/records`
* `POST /api/records`
* `PATCH /api/records/:id`
* `DELETE /api/records/:id`

---

### Request Body Example

```json
{
  "amount": 25000,
  "type": "income",
  "category": "consulting",
  "date": "2025-04-10",
  "notes": "Q2 project payment"
}
```

---

### Rules

* Analysts → can edit **their own records only**
* Admin → can edit **all records**

---

## 📊 Dashboard Analytics

* `GET /api/dashboard/summary`
* `GET /api/dashboard/category`
* `GET /api/dashboard/trend`
* `GET /api/dashboard/recent`

---

# ⚠️ Error Handling

### Standard Format

```json
{
  "error": "Short description",
  "details": ["field-level messages"]
}
```

---

### Status Codes

| Code | Meaning          |
| ---- | ---------------- |
| 200  | OK               |
| 201  | Created          |
| 400  | Validation error |
| 401  | Unauthorized     |
| 403  | Forbidden        |
| 404  | Not found        |
| 409  | Conflict         |
| 500  | Server error     |

---

# 🌐 Deployment

Live API Docs:
👉 https://backend-finance-dashboard-7dyj.onrender.com/

---

# 📌 Notes

* Ensure MongoDB is running before starting
* Use seeded users for quick testing
* All protected routes require JWT

---

# ⭐ Contribution

Feel free to fork, improve, and submit PRs 🚀

---

# 📄 License

MIT License
