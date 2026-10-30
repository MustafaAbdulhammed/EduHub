# EduHub

EduHub is a role-based educational platform for managing students, mentors, courses, materials, uploads, and academic activity. The project combines a React frontend with an Express backend and uses Firebase for authentication plus MongoDB for application data.

## Overview

EduHub is designed for a learning environment where different user roles have different responsibilities:

- Students can view courses, upload materials, review activity, and receive notifications
- Mentors can manage assigned courses, monitor enrollments, and review submissions
- Admins can manage users, programs, faculties, requests, settings, and platform activity

The application supports:

- Multi-role dashboards and navigation
- Course and enrollment management
- Material uploads and download access
- Notification and activity log flows
- Google Drive-backed file storage integration
- Firebase-based user authentication

## Tech Stack

Frontend
- React 18
- React Router
- Tailwind CSS
- Framer Motion
- React Query
- Zustand
- Firebase client SDK

Backend
- Node.js
- Express
- MongoDB with Mongoose
- Firebase Admin SDK
- Google Drive API integration
- JWT-based auth middleware

Dev tooling
- Concurrently for running client and server together
- Nodemon for backend development
- Docker Compose for local infrastructure support

## Project Structure

```text
EduHub/
├── client/                  # React frontend app
│   ├── public/              # Static assets
│   ├── src/
│   │   ├── components/      # Reusable UI and sections
│   │   ├── context/         # App contexts
│   │   ├── features/        # Role-based feature modules
│   │   ├── hooks/           # Custom hooks
│   │   ├── lib/             # Firebase, API, utilities
│   │   ├── pages/           # Route-level screens
│   │   ├── router/          # Routing + guards
│   │   ├── services/        # API clients
│   │   └── styles/          # Global styles and tokens
│   └── package.json
├── server/                  # Express API server
│   ├── src/
│   │   ├── config/          # DB, Firebase, and app config
│   │   ├── middleware/      # Auth, validation, errors
│   │   ├── modules/         # Domain modules (users, courses, uploads, etc.)
│   │   └── shared/          # Shared helpers
│   ├── server.js
│   └── package.json
├── scripts/                 # Utility scripts
├── uploads/                 # Local uploaded material storage
├── docker-compose.yml       # Local service setup
├── CORS.json                # CORS config for Firebase/Google resources
├── DEPLOYMENT_GUIDE.md      # Deployment notes
├── GOOGLE_DRIVE_SETUP.md    # Google Drive setup guide
├── package.json             # Root scripts
├── test-google-drive.js     # Drive integration smoke test
└── README.md                # Project documentation
```

## Core Features

### Student experience
- Dashboard and personalized academic overview
- Course browsing and enrollment management
- Material access and uploads
- Activity logs and review flows
- Notifications and profile routines

### Mentor experience
- Assigned course oversight
- Enrollment tracking
- Review queue and reporting
- Analytics and activity observations

### Admin experience
- User management
- Faculty, program, and course administration
- Moderation workflows
- Log and audit tracking
- Settings and notifications

### Platform infrastructure
- Secure Express API with CORS and rate limiting
- Firebase authentication integration
- Google Drive integration for file storage
- Upload serving through the backend and local `uploads/` folder
- Health-check endpoint for deployment monitoring

## Local Development

### Prerequisites

Before running the project locally, make sure you have:

- Node.js 18+
- npm
- MongoDB running locally or available via MongoDB Atlas
- Firebase project credentials
- Google Drive service account credentials (optional but recommended for drive-backed uploads)

### Install dependencies

From the project root:

```bash
npm install
npm run install-all
```

This installs dependencies for:
- the root workspace
- the React client
- the Express server

### Environment setup

Create environment files before starting the app.

Client environment (`client/.env`):

```env
REACT_APP_FIREBASE_API_KEY=your_api_key
REACT_APP_FIREBASE_AUTH_DOMAIN=your_project.firebaseapp.com
REACT_APP_FIREBASE_PROJECT_ID=your_project_id
REACT_APP_FIREBASE_STORAGE_BUCKET=your_project.appspot.com
REACT_APP_FIREBASE_MESSAGING_SENDER_ID=your_messaging_sender_id
REACT_APP_FIREBASE_APP_ID=your_app_id
```

Server environment (`server/.env`):

```env
NODE_ENV=development
PORT=5000
MONGO_URI=mongodb://localhost:27017/eduhub
JWT_SECRET=your_super_secret_key
CLIENT_URLS=http://localhost:3000
FIREBASE_PROJECT_ID=your_project_id
FIREBASE_CLIENT_EMAIL=your_service_account_email
FIREBASE_PRIVATE_KEY="-----BEGIN PRIVATE KEY-----\n...\n-----END PRIVATE KEY-----\n"
GOOGLE_SERVICE_ACCOUNT_KEY_PATH=./credentials/service-account-key.json
GOOGLE_DRIVE_FOLDER_ID=your_google_drive_folder_id
```

> Note: The Firebase private key must contain escaped newline characters in `.env` format, as shown above.

### Run the app

From the root directory:

```bash
npm run dev
```

This starts:
- the Express backend from `server/`
- the React frontend from `client/`

You can also run each side separately:

```bash
npm run server
npm run client
```

## API and backend notes

The backend is organized by feature module under `server/src/modules`. Common route groups include:

- `/api/auth` for authentication and authorization
- `/api/users` for user management
- `/api/courses` for course data
- `/api/enrollments` for enrollments and student-course tracking
- `/api/materials` for learning materials
- `/api/uploads` for file upload flows
- `/api/notifications` for notifications
- `/api/logs` for activity logs
- `/api/google-drive` for Google Drive-specific storage flows

The server also exposes a health endpoint:

```bash
GET /health
```

## Deployment

The repository includes operational guidance for deployment and Google Drive integration:

- [DEPLOYMENT_GUIDE.md](./DEPLOYMENT_GUIDE.md)
- [GOOGLE_DRIVE_SETUP.md](./GOOGLE_DRIVE_SETUP.md)

These documents explain environment variable setup, deployment targets, and cloud file-storage configuration.

## Recommended workflow

1. Start MongoDB and ensure services are accessible
2. Add Firebase and Google Drive credentials in `.env` files
3. Run `npm run dev`
4. Open the frontend in your browser at the local React dev server
5. Use the backend API on the configured Express port

## Troubleshooting

Common issues:

- Missing Firebase variables: verify the client and server environment files are populated
- MongoDB connection failures: confirm `MONGO_URI` is valid and the database is running
- Google Drive upload errors: verify the service account key, folder ID, and API permissions
- CORS issues: confirm `CLIENT_URLS` matches the frontend origin in development or deployment

## Contributing

If you are contributing to this project:

- keep feature work organized by module
- update environment documentation when adding new configuration values
- keep secrets out of source control
- validate both frontend and backend behavior before merging changes

## Notes

This project appears to be a full-stack educational management platform with role-based access and cloud file support. The repository is structured for local development and deployment across separate frontend and backend applications.
