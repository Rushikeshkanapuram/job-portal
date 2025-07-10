#  Job Portal Application

A full-stack Job Portal platform that connects **job seekers** with **recruiters**. Users can register, log in, create a profile, upload resumes, search and apply for jobs. Recruiters can post jobs, view applicants, and manage application statuses (Accept/Reject).

---

##  Tech Stack

###  Frontend

- React.js (with Hooks)
- Redux Toolkit (global state management)
- React Router DOM
- Tailwind CSS
- ShadCN UI
- Axios

###  Backend

- Node.js
- Express.js
- MongoDB (Mongoose ODM)
- Cloudinary (file storage)
- Multer (handling form-data file uploads)
- JWT (Authentication & Authorization)
- Cookie-based session management
- CORS, dotenv, bcryptjs

---

##  Folder Structure

```
job-portal/
├── frontend/                # React Client
│   ├── components/          # Shared UI components (Navbar, Job, etc.)
│   ├── pages/               # Page components (Home, Profile, Browse, etc.)
│   ├── hooks/               # Custom React hooks (API fetching logic)
│   ├── redux/               # Redux slices (authSlice, jobSlice, etc.)
│   └── utils/               # Constants like API endpoints
│
├── backend/                 # Express Server
│   ├── controllers/         # Logic for users, jobs, companies, applications
│   ├── models/              # MongoDB schemas (User, Job, Company, Application)
│   ├── routes/              # API endpoints
│   ├── middleware/          # Auth middleware, error handlers
│   └── index.js             # App entry point
```

---

##  Features

###  For Job Seekers

- Register and login
- Update profile with bio, photo, skills, and resume
- Browse and search jobs by keyword
- Apply to jobs (with one click)
- Track all applied jobs with application status
- View recruiter decisions (Accepted / Rejected)

###  For Recruiters

- Post jobs with details (title, location, type, etc.)
- View all applicants for each job
- Access applicant profile, resume
- Accept or reject applications
- Manage company profile and setup

###  Authentication

- Role-based (Seeker / Recruiter)
- JWT-based login stored in cookies
- Protected routes for recruiters using middleware

---

##  API Endpoints (Backend)

###  Auth
- `POST /api/auth/register`
- `POST /api/auth/login`
- `GET /api/auth/user`
- `GET /api/auth/logout`

###  Job
- `POST /api/job/create`
- `GET /api/job/get`
- `GET /api/job/:id`
- `PUT /api/job/update/:id`
- `DELETE /api/job/delete/:id`

###  Application
- `POST /api/application/apply/:id`
- `GET /api/application/get` (for seekers)
- `GET /api/application/:id/applicants` (for recruiters)
- `POST /api/application/status/:id/update`

###  Company
- `POST /api/company/create`
- `GET /api/company/get`
- `GET /api/company/:id`
- `PUT /api/company/update/:id`

---

##  State Management (Redux Slices)

- `authSlice`: stores user info, login state
- `jobSlice`: handles all jobs, applied jobs, searched queries
- `applicationSlice`: stores applicants for recruiter
- `companySlice`: manages current company details

---

##  File Uploads

- Resumes and profile photos are uploaded to Cloudinary
- `multer` handles multipart/form-data on the backend
- Resume download link is provided in applicant details

---

##  Smart Features

-  Search: Jobs can be searched by title, description, or location
-  Filtering (planned): FilterCard UI is already scaffolded
-  Animations: `framer-motion` used for job card transitions
-  Responsive UI with Tailwind & ShadCN components
-  Clean UX with popovers, modals, and toasts

---

##  Sample Components

###  Hero Search Component

```jsx
const searchJobHandler = () => {
    dispatch(setSearchedQuery(query));
    navigate("/browse");
}
```

###  Protected Route (Recruiter-only)

```jsx
useEffect(() => {
    if (!user || user.role !== 'recruiter') {
        navigate("/");
    }
}, []);
```

###  Applied Jobs Status

```jsx
<Badge className={
    appliedJob.status === "rejected" ? 'bg-red-400' :
    appliedJob.status === "pending" ? 'bg-gray-400' :
    'bg-green-400'
}>
    {appliedJob.status.toUpperCase()}
</Badge>
```

---

##  Usage

### 1. Install Dependencies

```bash
cd backend
npm install

cd ../frontend
npm install
```

### 2. Set Up Environment Variables

See `.env` examples below.

#### backend/.env
```env
PORT=8000
MONGO_URL=your_mongodb_connection_string
SECRET_KEY=your_jwt_secret
CLOUD_NAME=your_cloudinary_cloud_name
API_KEY=your_cloudinary_api_key
API_SECRET=your_cloudinary_api_secret
```

#### frontend/.env
```env
VITE_API_END_POINT=http://localhost:8000
```

### 3. Run the App

```bash
# Start backend
cd backend
npm run dev

# Start frontend in a new terminal
cd ../frontend
npm run dev
```

Visit `http://localhost:5173` to start using the app.

---

##  Author

- [Rushikesh Kanapuram](https://github.com/Rushikeshkanapuram)

---

##  Notes

- Supports recruiter and job seeker views
- Add `.env` files to root of each folder
- `node_modules` and other logs are ignored via `.gitignore`
