# GreenCode

GreenCode is a full-stack system designed to support environmental, sustainability, and community-impact projects under Bos-Com.  
It consists of a **Spring Boot backend API** and a **React frontend** (new addition), with future integrations planned.

---

## 🚀 Features

### Backend (Spring Boot)
- RESTful API
- JWT/OAuth authentication
- PostgreSQL database support
- Centralised configuration (`config/`, `.env`)
- Dockerized for easy deployment
- Swagger/OpenAPI documentation

### Frontend (React)
- Modern React with Vite (recommended over deprecated Create React App)
- React Router for navigation
- Axios for API communication
- Authentication UI (login, password reset flow)
- Tailwind CSS configured and ready to use
- Ready to connect to backend reset API

---

## 🚧 Frontend Setup (Vite + Tailwind CSS)

### Prerequisites
- Node.js 18+
- npm or yarn

### Installation

```bash
# Navigate to frontend directory (if separate) or use root
# For Vite setup:
npm create vite@latest greencode-frontend -- --template react
cd greencode-frontend
npm install

# Install Tailwind CSS
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

### Configure Tailwind

Update `tailwind.config.js`:
```javascript
module.exports = {
  content: [
    "./index.html",
    "./src/**/*.{js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

Add to `src/index.css`:
```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

### Running the Frontend

```bash
npm run dev
```

The frontend will be available at `http://localhost:5173`

---

## 📁 Project Structure
GreenCode/
├── src/                 # Spring Boot source code
├── config/              # external configuration & scripts
├── docs/                # architecture, API docs
├── greencode-frontend/  # React frontend (new)
├── pom.xml              # Maven build file
└── docker-compose.yml   # Docker orchestration

## 🧪 Testing the API

### Running the Backend

```bash
# Using Maven
./mvnw spring-boot:run

# Or build and run with Docker
docker-compose up -d
```

The backend will be available at `http://localhost:8080`

### API Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/api/auth/login` | POST | User authentication |
| `/api/auth/register` | POST | User registration |
| `/api/projects` | GET | List all projects |
| `/api/projects` | POST | Create new project |
| `/api/projects/{id}` | GET | Get project details |
| `/api/projects/{id}` | PUT | Update project |
| `/api/projects/{id}` | DELETE | Delete project |
| `/api/users` | GET | List all users |

### Testing with curl

```bash
# Test health endpoint
curl http://localhost:8080/actuator/health

# Register a new user
curl -X POST http://localhost:8080/api/auth/register \
  -H "Content-Type: application/json" \
  -d '{
    "username": "testuser",
    "email": "test@example.com",
    "password": "password123"
  }'

# Login
curl -X POST http://localhost:8080/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{
    "username": "testuser",
    "password": "password123"
  }'

# Get all projects (after authentication)
curl http://localhost:8080/api/projects \
  -H "Authorization: Bearer YOUR_JWT_TOKEN"

# Create a new project
curl -X POST http://localhost:8080/api/projects \
  -H "Authorization: Bearer YOUR_JWT_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Tree Planting Initiative",
    "description": "Community tree planting campaign",
    "status": "active",
    "category": "environment"
  }'
```

### Swagger Documentation

Once the application is running, access the Swagger UI at:
- http://localhost:8080/swagger-ui.html
- http://localhost:8080/v3/api-docs

### Running Tests

```bash
# Run all tests
./mvnw test

# Run specific test class
./mvnw test -Dtest=ProjectServiceTest

# Run with coverage
./mvnw test jacoco:report
```

### Frontend Testing

```bash
# Navigate to frontend directory
cd greencode-frontend

# Install dependencies
npm install

# Start development server
npm run dev

# Run tests
npm test

# Build for production
npm run build
```
