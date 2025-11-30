# Quick Setup Guide

## Prerequisites
- Node.js (v14+)
- MongoDB (local or Atlas)

## Installation Steps

### 1. Install Dependencies

```bash
# Install root dependencies
npm install

# Install backend dependencies
cd backend
npm install

# Install frontend dependencies
cd ../frontend
npm install
```

### 2. Backend Setup

```bash
cd backend

# Create .env file (copy from env.example)
# Windows: copy env.example .env
# Linux/Mac: cp env.example .env

# Edit .env with your MongoDB URI
# For local MongoDB: mongodb://localhost:27017/attendance_db
# For MongoDB Atlas: mongodb+srv://username:password@cluster.mongodb.net/attendance_db

# Seed the database
npm run seed

# Start the server
npm run dev
```

### 3. Frontend Setup

```bash
cd frontend

# Create .env file
# Windows: echo REACT_APP_API_URL=http://localhost:5000/api > .env
# Linux/Mac: echo "REACT_APP_API_URL=http://localhost:5000/api" > .env

# Start the development server
npm start
```

### 4. Access the Application

- Frontend: http://localhost:3000
- Backend API: http://localhost:5000

## Default Login Credentials

**Manager:**
- Email: manager@company.com
- Password: manager123

**Employee:**
- Email: alice@company.com
- Password: employee123

## Troubleshooting

### MongoDB Connection Issues
- Ensure MongoDB is running locally, or
- Update MONGODB_URI in backend/.env with your Atlas connection string

### Port Already in Use
- Change PORT in backend/.env
- Update REACT_APP_API_URL in frontend/.env accordingly

### CORS Errors
- Ensure backend is running on port 5000
- Check REACT_APP_API_URL matches backend URL


