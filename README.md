# Patient Management

A full-stack patient management app with a React frontend and an Express + MongoDB backend.

The system supports:

- Admin and doctor sign-in with JWT authentication
- Doctor registration with profile image upload
- Patient registration
- Patient and doctor search by ID number
- Patient medical record creation by doctors
- Contact info updates for doctors and patients by admins

## Tech Stack

- Frontend: React, Vite, React Router, Redux Toolkit
- Backend: Node.js, Express
- Database: MongoDB
- Auth: JSON Web Tokens
- File upload: Formidable

## Project Structure

```text
patientManagement/
|-- backend/
|   |-- controllers/
|   |-- helpers/
|   |-- middlewares/
|   |-- routes/
|   |-- uploads/
|   `-- index.js
|-- frontend/
|   |-- src/
|   `-- vite.config.js
`-- README.md
```

## Features

### Authentication

- `POST /users/signin` signs in an admin or doctor
- JWTs are required for protected actions
- Tokens expire after 1 hour

### Doctors

- Admins can register doctors
- Doctor registration accepts multipart form data and an image upload
- Anyone can search doctors by ID number
- Admins can update doctor contact details

### Patients

- Admins and doctors can register patients
- Doctors can add medical records
- Anyone can search patients by ID number
- Admins can update patient contact details

## Frontend Routes

The React app currently exposes these pages:

- `/`
- `/about`
- `/signin`
- `/profile`
- `/adminpanel`
- `/registerdoctor`
- `/searchdoctor`
- `/registerpatient`
- `/searchpatient`

## Backend API

### User routes

- `POST /users/signin`
- `GET /users/checkifloggedin`

### Doctor routes

- `POST /doctors/registerdoctor`
- `GET /doctors/search?idnumber=...`
- `POST /doctors/updatecontact`

### Patient routes

- `POST /patients/registerpatient`
- `GET /patients/search?idnumber=...`
- `POST /patients/addnewmedicalrecord`
- `POST /patients/updatecontact`

## Prerequisites

- Node.js 18+
- npm
- MongoDB running locally on `mongodb://localhost:27017`

## Environment Variables

Create `backend/.env` with:

```env
PORT=5000
secret=your_jwt_secret
```

Notes:

- The backend currently uses a hardcoded MongoDB connection string: `mongodb://localhost:27017`
- The database name is hardcoded as `medicalportal`

## Database Setup

The app expects MongoDB collections such as:

- `admin`
- `doctors`
- `patients`

At least one admin account must exist in the `admin` collection before admin-only features can work.

The code expects admin documents to include at least:

- `email`
- `username`
- `password` (bcrypt hash)

Doctor documents include:

- `idnumber`
- `phone`
- `email`
- `username`
- `password`

Patient documents include:

- `idnumber`
- `username`
- `email`
- `address`
- `phone`
- `medicalrecord`

## Installation

### 1. Install frontend dependencies

```bash
cd frontend
npm install
```

### 2. Install backend dependencies

```bash
cd backend
npm install
```

## Running Locally

Open two terminals.

### Terminal 1: start the backend

```bash
cd backend
npm start
```

The backend runs on `http://localhost:5000`.

### Terminal 2: start the frontend

```bash
cd frontend
npm run dev
```

Vite will print the frontend URL, usually `http://localhost:5173`.

## Available Scripts

### Frontend

- `npm run dev` starts the Vite dev server
- `npm run build` builds the production bundle
- `npm run preview` previews the production build
- `npm run lint` runs ESLint

### Backend

- `npm start` starts the backend with Nodemon

## How Auth Works

- After sign-in, the frontend stores the returned JWT in `localStorage`
- Protected requests send the token in the `Authorization` header as `Bearer <token>`
- The backend verifies the token using `process.env.secret`

## File Upload Notes

- Doctor registration uploads an image file
- Uploaded files are stored in `backend/uploads`
- The current upload size limit is 1 MB

## Current Implementation Notes

- Backend URLs in the frontend are hardcoded to `http://localhost:5000`
- MongoDB connection settings are hardcoded in `backend/helpers/connectDB.js`
- There is no automated test suite yet
- The repository currently includes installed dependencies and uploaded files inside `backend/`

## Future Improvements

- Move API base URLs into environment variables
- Move MongoDB configuration into environment variables
- Add database seed scripts for admin creation
- Add tests for controllers and routes
- Add role-based UI guards across all protected pages

## License

This project does not currently declare a project-specific license.
