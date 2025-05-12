# G-SPA Database

A comprehensive database system for the G-SPA (Gamma-ray Spectroscopy with Public Access) project, featuring a modern web interface for accessing astronomical data.

## Project Overview

The G-SPA Database provides a unified platform for accessing, querying, and managing astronomical data. The system consists of:

- **Frontend**: Landing page and admin dashboard built with React
- **Backend**: Authentication and data fetching service (Flask) and a specialized query service (Node.js)
- **Infrastructure**: MongoDB database and Nginx reverse proxy

## Implemented Features

### Frontend
- Landing page with public access to browse astronomical data
- Admin dashboard for data management and user administration
- Shared authentication components between applications
- Responsive design for desktop and mobile access

### Backend
- Authentication system with session management
- Data fetching service for CRUD operations on astronomical data
- Specialized query service for complex data analysis
- API for both public and authenticated access

### DevOps
- Docker containerization of all services
- Nginx reverse proxy configuration
- MongoDB database integration

## Deployment Requirements

The following updates are needed for production deployment:

### Frontend
- Environment variable configuration for production endpoints
- Implementation of token expiration handling
- Enhanced error handling and user feedback

### Backend
- Replace hardcoded paths with environment variables
- Implement secure password storage with proper hashing
- Add token expiration settings
- Enforce HTTPS for all connections

### DevOps
- Set up data backup and restore procedures
- Configure monitoring and logging
- Implement CI/CD pipeline
- Set up SSL certificates for HTTPS

## Installation and Setup

### Prerequisites
- Docker and Docker Compose
- Node.js (for local development)
- Python 3.8+ (for local development)

### Running with Docker
```bash
# Clone the repository
git clone https://github.com/GSPA-Studios/G-SPA_DB
cd G-SPA_DB

# Build and start the containers
docker-compose up -d

# The application will be available at:
# - Landing page: http://localhost:80
# - Admin dashboard: http://localhost:80/admin
# - API: http://localhost:80/api
```

### Local Development Setup
```bash
# Backend: Fetching Service
cd backend/fetching_n_auth/backend
pip install -r requirements.txt

# Backend: Query Service
cd backend/queries
pnpm install

# Frontend: Landing Page
cd frontend/landingPage
npm install

# Frontend: Admin Dashboard
cd frontend/adminDashboard
npm install
```

## Architecture

```
G-SPA_DB/
├── frontend/
│   ├── landingPage/       # Public access interface
│   └── adminDashboard/    # Administrator interface
├── backend/
│   ├── fetching_n_auth/   # Authentication and data management (Flask)
│   └── queries/           # Specialized query service (Node.js)
├── nginx/                 # Reverse proxy configuration
└── docker-compose.yml     # Container orchestration
```

## Endpoint Configuration

### API Endpoints

The G-SPA Database system uses a reverse proxy architecture to route requests to the appropriate services:

* **Landing Page:** `http://localhost/` 
* **Admin Dashboard:** `http://localhost/admin/`
* **Authentication API:** `http://localhost/api/fetch/auth/*`
* **Data Fetching API:** `http://localhost/api/fetch/*`
* **Query Service API:** `http://localhost/api/query/*`

### Endpoint Modifications & Security

#### Local Development Endpoints
- **Landing Page:** `http://localhost:3000`
- **Admin Dashboard:** `http://localhost:3001`
- **Fetch Service API:** `http://localhost:5000`
- **Query Service API:** `http://localhost:4000`

#### Cross-Origin Resource Sharing (CORS)
- Frontend services are configured to communicate with backend services using proper CORS headers
- Admin Dashboard uses a proxy configuration in `vite.config.js` to route `/api` requests to the backend
- Landing Page uses environment variables for API configuration in `config.js`

#### Authentication Endpoints
- **Shared Authentication:** Both applications use the same token-based authentication system
- **Admin Login:** `/admin/login` requiring credentials for each session
- **Token Validation:** `/api/auth/validate` for verifying token validity
- **Session Management:** Admin sessions stored in `sessionStorage` for enhanced security

#### Production Configuration
For production deployment, modify the following files:
1. Update `.env` files in both frontend applications with production API URLs
2. Configure `docker-compose.yml` with appropriate environment variables
3. Update `nginx.conf` to include SSL/TLS settings for HTTPS
4. Set secure cookie attributes with `SameSite=Strict` and `HttpOnly=true`

#### Endpoint Security Enhancements
- **Token Expiration:** Tokens expire after a configurable time period
- **Session Validation:** Regular checks for valid sessions (every 3 minutes)
- **Automatic Redirection:** Expired sessions redirect to login page
- **HTTPS Enforcement:** All endpoints should use HTTPS in production

## Contributing

Contributions are welcome! Please see the [CONTRIBUTING.md](CONTRIBUTING.md) file for details.

## License

This project is licensed under the MIT License - see the LICENSE file for details.

