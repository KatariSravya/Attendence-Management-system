# Employee Attendance Management System

A comprehensive attendance tracking system built with React, Node.js, Express, and MongoDB. The system supports two user roles: Employees and Managers, each with their own set of features and dashboards.

## Tech Stack

- **Frontend**: React 18 + TypeScript + Zustand + Tailwind CSS
- **Backend**: Node.js + Express
- **Database**: MongoDB
- **State Management**: Zustand
- **Routing**: React Router DOM
- **Charts**: Recharts
- **Calendar**: React Calendar

## Features

### Employee Features
- ✅ Register/Login
- ✅ Mark attendance (Check In / Check Out)
- ✅ View attendance history (calendar or table view)
- ✅ View monthly summary (Present/Absent/Late days)
- ✅ Dashboard with stats and recent attendance
- ✅ Profile page

### Manager Features
- ✅ Login
- ✅ View all employees attendance
- ✅ Filter by employee, date, status
- ✅ View team attendance summary
- ✅ Export attendance reports (CSV)
- ✅ Dashboard with team stats and charts
- ✅ Calendar view for team attendance
- ✅ Reports page with date range filtering

## Project Structure

```
attendance-management/
├── backend/
│   ├── models/
│   │   ├── User.js
│   │   └── Attendance.js
│   ├── routes/
│   │   ├── auth.js
│   │   ├── attendance.js
│   │   └── dashboard.js
│   ├── middleware/
│   │   └── auth.js
│   ├── scripts/
│   │   └── seed.js
│   ├── server.js
│   └── package.json
├── frontend/
│   ├── src/
│   │   ├── api/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── store/
│   │   ├── App.tsx
│   │   └── index.tsx
│   └── package.json
└── README.md
```

## Setup Instructions

### Prerequisites
- Node.js (v14 or higher)
- MongoDB (local installation or MongoDB Atlas)
- npm or yarn

### Backend Setup

1. Navigate to the backend directory:
```bash
cd backend
```

2. Install dependencies:
```bash
npm install
```

3. Create a `.env` file in the backend directory:
```env
PORT=5000
MONGODB_URI=mongodb://localhost:27017/attendance_db
JWT_SECRET=your_super_secret_jwt_key_change_this_in_production
NODE_ENV=development
```

4. Start MongoDB (if running locally):
```bash
# On Windows
net start MongoDB

# On macOS/Linux
sudo systemctl start mongod
```

5. Seed the database with sample data:
```bash
npm run seed
```

6. Start the backend server:
```bash
npm run dev
```

The backend server will run on `http://localhost:5000`

### Frontend Setup

1. Navigate to the frontend directory:
```bash
cd frontend
```

2. Install dependencies:
```bash
npm install
```

3. Create a `.env` file in the frontend directory:
```env
REACT_APP_API_URL=http://localhost:5000/api
```

4. Start the development server:
```bash
npm start
```

The frontend will run on `http://localhost:3000`

### Running Both Together

From the root directory, you can install all dependencies and run both servers:

```bash
# Install all dependencies
npm run install-all

# Run both backend and frontend
npm run dev
```

## Default Login Credentials

After running the seed script, you can use these credentials:

### Manager
- Email: `manager@company.com`
- Password: `manager123`

### Employee
- Email: `alice@company.com`
- Password: `employee123`

Additional employees are also created by the seed script.

## API Endpoints

### Auth
- `POST /api/auth/register` - Register a new user
- `POST /api/auth/login` - Login user
- `GET /api/auth/me` - Get current user

### Attendance (Employee)
- `POST /api/attendance/checkin` - Check in
- `POST /api/attendance/checkout` - Check out
- `GET /api/attendance/my-history` - Get attendance history
- `GET /api/attendance/my-summary` - Get monthly summary
- `GET /api/attendance/today` - Get today's status

### Attendance (Manager)
- `GET /api/attendance/all` - Get all employees attendance
- `GET /api/attendance/employee/:id` - Get specific employee attendance
- `GET /api/attendance/summary` - Get team summary
- `GET /api/attendance/export` - Export CSV
- `GET /api/attendance/today-status` - Get today's status for all

### Dashboard
- `GET /api/dashboard/employee` - Employee dashboard data
- `GET /api/dashboard/manager` - Manager dashboard data

## Database Schema

### Users Collection
```javascript
{
  name: String,
  email: String (unique),
  password: String (hashed),
  role: 'employee' | 'manager',
  employeeId: String (unique),
  department: String,
  createdAt: Date
}
```

### Attendance Collection
```javascript
{
  userId: ObjectId (ref: User),
  date: Date,
  checkInTime: Date,
  checkOutTime: Date,
  status: 'present' | 'absent' | 'late' | 'half-day',
  totalHours: Number,
  createdAt: Date
}
```

## Features in Detail

### Attendance Status Logic
- **Present**: Checked in before 9:30 AM
- **Late**: Checked in after 9:30 AM
- **Absent**: No check-in recorded
- **Half-day**: Total hours worked less than 4 hours

### Calendar View
- Color-coded calendar showing attendance status
- Green: Present
- Yellow: Late
- Red: Absent
- Orange: Half-day

### Reports Export
- Filter by date range and employee
- Export to CSV format
- Includes all attendance details

## Environment Variables

### Backend (.env)
- `PORT` - Server port (default: 5000)
- `MONGODB_URI` - MongoDB connection string
- `JWT_SECRET` - Secret key for JWT tokens
- `NODE_ENV` - Environment (development/production)

### Frontend (.env)
- `REACT_APP_API_URL` - Backend API URL

## Screenshots

The application includes:
- Modern, responsive UI with Tailwind CSS
- Interactive dashboards with charts
- Calendar view for attendance tracking
- Comprehensive filtering and search
- CSV export functionality

## Development

### Backend Development
- Uses nodemon for auto-restart
- MongoDB connection with Mongoose
- JWT authentication
- RESTful API design

### Frontend Development
- TypeScript for type safety
- Zustand for state management
- React Router for navigation
- Tailwind CSS for styling
- Responsive design

## License

This project is open source and available for educational purposes.

## Support

For issues or questions, please check the code comments or create an issue in the repository.

