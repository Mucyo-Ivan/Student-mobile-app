# Student Authentication App

A simple mobile application built with React Native (Expo) that allows students to sign up, login, and view their profile. The app uses a Node.js backend with PostgreSQL database for secure data storage.

## Features

- **Student Signup**: Register with name, email, and password
- **Student Login**: Secure authentication with encrypted passwords
- **Profile Display**: View logged-in student's name after authentication
- **Logout**: Simple logout functionality
- **Cross-Platform**: Runs on web, iOS, and Android

## Tech Stack

### Frontend
- **React Native** with Expo
- **Expo Router** for navigation
- **Axios** for API requests

### Backend
- **Node.js** with Express
- **PostgreSQL** database
- **bcryptjs** for password hashing
- **CORS** for cross-origin requests

## Prerequisites

Before running this project, make sure you have:

- **Node.js** (v14 or higher) - [Download here](https://nodejs.org/)
- **PostgreSQL** (v12 or higher) - [Download here](https://www.postgresql.org/download/)
- **npm** or **yarn** package manager
- **Expo CLI** (will be installed globally)

## Project Structure

```
student-authentication-app/
├── student-app-backend/          # Backend API
│   ├── server.js                 # Express server and API routes
│   ├── .env                      # Database configuration
│   └── package.json
│
└── student-app-frontend/         # Frontend app
    ├── app/
    │   └── index.js              # Main app screen
    ├── App.js
    ├── app.json
    └── package.json
```

## Installation & Setup

### 1. Database Setup

**Step 1:** Start PostgreSQL service

**Step 2:** Open PostgreSQL terminal (psql) and create the database:

```sql
CREATE DATABASE student_app;
```

**Step 3:** Connect to the database:

```sql
\c student_app
```

**Step 4:** Create the students table:

```sql
CREATE TABLE students (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### 2. Backend Setup

**Step 1:** Navigate to backend folder:

```bash
cd student-app-backend
```

**Step 2:** Install dependencies:

```bash
npm install
```

**Step 3:** Create `.env` file in the backend folder:

```env
PORT=5000
DB_USER=postgres
DB_HOST=localhost
DB_NAME=student_app
DB_PASSWORD=your_postgres_password
DB_PORT=5432
```

Replace `your_postgres_password` with your actual PostgreSQL password.

**Step 4:** Start the backend server:

```bash
node server.js
```

You should see:
```
Server running on port 5000
Connected to PostgreSQL database
```

### 3. Frontend Setup

**Step 1:** Open a new terminal and navigate to frontend folder:

```bash
cd student-app-frontend
```

**Step 2:** Install dependencies:

```bash
npm install
```

**Step 3:** Install Axios (if not already installed):

```bash
npm install axios
```

**Step 4:** Start the Expo development server:

```bash
npx expo start
```

**Step 5:** Choose how to run the app:
- Press `w` to open in **web browser**
- Press `a` to open in **Android emulator**
- Press `i` to open in **iOS simulator**
- Scan QR code with **Expo Go app** on your phone

## Usage

### Sign Up
1. Open the app - you'll see the "Student Signup" screen
2. Enter your name, email, and password
3. Click "Sign Up"
4. You'll see a success message

### Login
1. After signing up, click "Already have an account? Login"
2. Enter your email and password
3. Click "Login"
4. You'll be taken to the welcome screen

### Welcome Screen
1. After successful login, you'll see "Welcome!" with your name displayed
2. Click "Logout" to return to the login screen

## API Endpoints

### POST /api/signup
Create a new student account

**Request Body:**
```json
{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "password123"
}
```

**Response:**
```json
{
  "message": "Signup successful",
  "student": {
    "id": 1,
    "name": "John Doe",
    "email": "john@example.com"
  }
}
```

### POST /api/login
Authenticate a student

**Request Body:**
```json
{
  "email": "john@example.com",
  "password": "password123"
}
```

**Response:**
```json
{
  "message": "Login successful",
  "student": {
    "id": 1,
    "name": "John Doe",
    "email": "john@example.com"
  }
}
```

## Troubleshooting

### Backend Issues

**Problem:** "Database connection failed"
- **Solution:** Check your `.env` file has correct PostgreSQL credentials
- **Solution:** Ensure PostgreSQL service is running

**Problem:** Port 5000 already in use
- **Solution:** Change the PORT in `.env` to a different number (e.g., 5001)

### Frontend Issues

**Problem:** "Network Error" when signing up/logging in
- **Solution:** Make sure backend server is running on port 5000
- **Solution:** For physical devices, change `localhost` to your computer's IP address in `app/index.js`

**Problem:** Can't see signup page, only welcome screen
- **Solution:** Make sure you edited the file inside `app/` folder, not root `App.js`
- **Solution:** Run `npx expo start -c` to clear cache

**Problem:** Alert doesn't show on web
- **Solution:** The code uses `alert()` for web compatibility instead of `Alert.alert()`

## Running on Different Ports

### Change Frontend Port (default 8081)

```bash
npx expo start --port 9000
```

### Change Backend Port (default 5000)

Edit `.env` file:
```env
PORT=5001
```

Then update `API_URL` in `app/index.js`:
```javascript
const API_URL = 'http://localhost:5001/api';
```

## Security Notes

- Passwords are hashed using bcryptjs before storing in database
- Never commit `.env` file to version control
- In production, use environment variables and secure HTTPS connections
- Consider adding JWT tokens for session management in production

## Future Enhancements

- [ ] Add password strength validation
- [ ] Implement "Forgot Password" functionality
- [ ] Add email verification
- [ ] Include profile editing feature
- [ ] Add JWT token-based authentication
- [ ] Implement refresh tokens
- [ ] Add loading indicators
- [ ] Better error handling and validation

## License

This project is open source and available for educational purposes.

## Contributing

Feel free to fork this project and submit pull requests for any improvements.

## Support

If you encounter any issues:
1. Check the troubleshooting section above
2. Ensure all prerequisites are installed correctly
3. Verify your database connection and credentials
4. Make sure both backend and frontend servers are running

---

**Happy Coding!** 🚀
