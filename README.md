# TALQS Bot - Legal Technology Platform

A comprehensive, full-stack legal technology platform that combines AI-powered question-answering, document generation, and legal information management. Built with React, Vite, Flask, and MongoDB, TALQS Bot provides legal professionals and enthusiasts with intelligent tools for legal research, NDA generation, legal summarization, and case law reference materials.

**Repository**: [bhaavyaram/talqs_bot](https://github.com/bhaavyaram/talqs_bot)  
**Status**: Active Development  
**License**: Open Source

---

## Table of Contents

- [Overview](#overview)
- [Technology Stack](#technology-stack)
- [Project Structure](#project-structure)
- [Architecture](#architecture)
- [Installation & Setup](#installation--setup)
- [Configuration](#configuration)
- [Running the Application](#running-the-application)
- [API Reference](#api-reference)
- [Frontend Features](#frontend-features)
- [Backend Services](#backend-services)
- [Database](#database)
- [Authentication](#authentication)
- [Development Workflow](#development-workflow)
- [Key Components](#key-components)
- [Troubleshooting](#troubleshooting)

---

## Overview

TALQS Bot is a full-stack web application designed to democratize access to legal technology. The platform integrates:

- **AI-Powered Legal Q&A**: Using DistilBERT-based question-answering models for legal context understanding
- **Document Generation**: Automated NDA (Non-Disclosure Agreement) PDF generation with customizable fields
- **Legal Dictionary**: Searchable database of legal terminology and definitions
- **Case Law Simulation**: Interactive legal case scenario exploration
- **Legal Summarization**: Automated summarization of legal documents and context
- **IPC Sections Reference**: Indian Penal Code section lookup and reference
- **User Authentication**: JWT-based secure authentication with MongoDB persistence

The application separates concerns into a modern frontend (React + Vite) and a robust backend (Flask + MongoDB), communicating via REST APIs with CORS support.

---

## Technology Stack

### Frontend
| Layer | Technology | Version | Purpose |
|-------|-----------|---------|---------|
| **Framework** | React | ^18.3.1 | UI library |
| **Build Tool** | Vite | ^6.2.0 | Fast bundling & dev server |
| **Styling** | Tailwind CSS | ^4.1.2 | Utility-first CSS framework |
| **Routing** | React Router DOM | ^7.4.1 | Client-side navigation |
| **Animation** | Framer Motion | ^12.6.3 | Smooth UI animations |
| **UI Libraries** | Heroicons, Lucide React, React Icons | Latest | Icon sets |
| **State & Effects** | React Hooks | - | State management |
| **HTTP Client** | Axios | ^1.8.4 | API requests |
| **Rich Text** | React Quill | ^2.0.0 | Rich text editing |
| **Charts & Flow** | XYFlow React | ^12.5.4 | Interactive flow diagrams |
| **Canvas** | html2canvas | ^1.4.1 | DOM to canvas conversion |

### Backend
| Layer | Technology | Version | Purpose |
|-------|-----------|---------|---------|
| **Framework** | Flask | Latest | Web framework |
| **Middleware** | Flask-CORS | Latest | Cross-origin resource sharing |
| **ML Pipeline** | Transformers | Latest | NLP models (DistilBERT) |
| **ML Engine** | Torch/TensorFlow | Latest | Deep learning backend |
| **PDF Generation** | ReportLab | Latest | PDF document creation |
| **Database** | MongoDB | Cloud | NoSQL document store |
| **DB Driver** | PyMongo | Latest | MongoDB Python client |
| **Authentication** | JWT, bcrypt | Latest | Token & password management |
| **Security** | Python-dotenv | Latest | Environment variable loading |

### DevOps & Tools
- **Version Control**: Git
- **Package Management**: npm (frontend), pip (backend)
- **Environment**: Node.js, Python 3.8+
- **Database Hosting**: MongoDB Atlas (Cloud)

---

## Project Structure

```
talqs_bot/
│
├── Root Level (Frontend)
│   ├── index.html                 # Entry HTML template
│   ├── package.json               # Frontend dependencies & scripts
│   ├── vite.config.js             # Vite bundler configuration
│   ├── eslint.config.js           # Linting rules
│   ├── .gitignore                 # Git ignore rules
│   └── README.md                  # This file
│
├── src/                           # React frontend source code
│   ├── main.jsx                   # React app entry point with BrowserRouter
│   ├── App.jsx                    # Main app router & layout
│   ├── index.css                  # Global styles with Tailwind imports
│   ├── App.css                    # App-specific styles
│   │
│   ├── assets/                    # Reusable UI components & content sections
│   │   ├── WelcomePage.jsx        # Hero welcome section
│   │   ├── herosection.jsx        # Landing page hero
│   │   ├── qasumm.jsx             # QA & summarization feature showcase
│   │   ├── contents.jsx           # Content exploration flow
│   │   └── Neonflow.jsx           # Neon-styled flow animations
│   │
│   ├── pages/                     # Full-page components (routes)
│   │   ├── login.jsx              # User login page with auth
│   │   ├── signup.jsx             # User registration page
│   │   ├── Navbar.jsx             # Navigation bar component
│   │   ├── NotePage.jsx           # Note-taking interface
│   │   ├── qachatbot.jsx          # Legal Q&A chatbot interface
│   │   ├── summarization.jsx      # Document summarization page
│   │   ├── LegalDictionary.jsx    # Legal terminology lookup
│   │   ├── Ndatemplate.jsx        # NDA template editor
│   │   ├── ipcsecs.jsx            # IPC sections reference
│   │   ├── nextpage.jsx           # Legal case simulation
│   │   ├── features.jsx           # Feature showcase
│   │   ├── footer.jsx             # Site footer
│   │   ├── global.css             # Page-level styles
│   │   ├── image.png              # Reference images
│   │   └── legal-note-*.png       # Legal documentation images
│   │
│   └── components/                # Reusable UI components
│       ├── Sidebar.jsx            # Sidebar navigation
│       ├── Navbar.jsx             # (Empty, used in pages/)
│       └── DictionaryResultCard.jsx # Dictionary result display
│
├── public/                        # Static assets served as-is
│   └── (Icons, favicon, etc.)
│
├── backend/                       # Flask backend API server
│   ├── package.json               # Node dependencies (express stack)
│   ├── vite.config.js             # Vite config (if serving frontend)
│   ├── .env                       # Environment variables (MongoDB URI, SECRET_KEY)
│   ├── README.md                  # Backend documentation
│   ├── .gitignore                 # Git ignore rules
│   │
│   └── backend/                   # Python Flask application
│       ├── app.py                 # Main Flask application (7,479 bytes)
│       ├── database.py            # MongoDB connection setup
│       ├── requirements.txt       # Python dependencies
│       ├── package.json           # Node dependencies for PDF generation
│       │
│       ├── venv/                  # Python virtual environment (not versioned)
│       ├── __pycache__/           # Python bytecode cache (not versioned)
│       ├── templates/             # HTML templates (if applicable)
│       └── package-lock.json      # Locked Node dependencies
│
└── .github/                       # GitHub configuration (if present)
    └── workflows/                 # CI/CD pipelines (if configured)
```

---

## Architecture

### High-Level Architecture Flow

```
┌─────────────────────────────────────────────────────────────────┐
│                        CLIENT BROWSER                            │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                  React + Vite SPA                       │   │
│  │  (Pages: Login, QA Bot, Dictionary, NDA, etc.)    │   │
│  └─────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
                          ↓ (HTTP/REST/JSON)
┌─────────────────────────────────────────────────────────────────┐
│                    BACKEND API SERVER                            │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │           Flask Application (app.py)                    │   │
│  │  ┌─────────────────────────────────────────────────┐   │   │
│  │  │ Endpoints:                                       │   │   │
│  │  │ • POST /signup - User registration             │   │   │
│  │  │ • POST /login - User authentication (JWT)      │   │   │
│  │  │ • POST /verify-token - Token validation        │   │   │
│  │  │ • POST /ask - Legal Q&A (DistilBERT pipeline) │   │   │
│  │  │ • POST /generate_nda_pdf - PDF generation     │   │   │
│  │  │ • GET /test-db - Database connectivity check  │   │   │
│  │  └─────────────────────────────────────────────────┘   │   │
│  └─────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
                          ↓ (PyMongo Driver)
┌─────────────────────────────────────────────────────────────────┐
│              MongoDB Atlas Cloud Database                        │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ Database: "talqs"                                       │   │
│  │ Collections:                                            │   │
│  │ • users - Stores user credentials (email, hash_pwd)   │   │
│  └─────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
                          ↓ (HuggingFace API)
┌─────────────────────────────────────────────────────────────────┐
│         Machine Learning Models & Transformers                  │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ • distilbert-base-cased-distilled-squad               │   │
│  │   (Question-Answering on legal context)                │   │
│  └─────────────────────────────────────────────────────────┘   │
└───────────────────────────────────────��─────────────────────────┘
```

### Request/Response Flow

1. **User Requests** (Browser) → **React Router** (URL routing)
2. **React Components** → **Axios HTTP Client** → **Flask Endpoints**
3. **Flask** processes request → queries **MongoDB** or **NLP Pipeline**
4. **Response** returned as JSON → **React State Updates** → **Component Re-render**

### Authentication Flow

```
User Input (email, password)
           ↓
     Flask /login
           ↓
  MongoDB users_collection lookup
           ↓
  bcrypt password validation
           ↓
  JWT token generation (exp: 1 hour)
           ↓
  Token stored in localStorage (client)
           ↓
  Token sent with subsequent API requests
           ↓
  /verify-token endpoint validates JWT
           ↓
  ✓ Access granted or ✗ token expired
```

---

## Installation & Setup

### Prerequisites

- **Node.js** (v16+) & npm
- **Python** (v3.8+) & pip
- **MongoDB Atlas account** (Cloud database)
- **Git**

### Frontend Setup

1. **Clone the repository**:
   ```bash
   git clone https://github.com/bhaavyaram/talqs_bot.git
   cd talqs_bot
   ```

2. **Install frontend dependencies**:
   ```bash
   npm install
   ```

3. **Verify installations**:
   ```bash
   npm list | head -20  # Check key dependencies
   ```

### Backend Setup

1. **Navigate to backend directory**:
   ```bash
   cd backend/backend
   ```

2. **Create Python virtual environment**:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install Python dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

   **Dependencies installed**:
   - `flask` - Web framework
   - `flask-cors` - CORS support
   - `transformers` - NLP models
   - `torch` or `tensorflow` - ML backends
   - `bcrypt` - Password hashing
   - `pyjwt` - JWT token generation
   - `pymongo` - MongoDB driver
   - `python-dotenv` - Environment variables
   - `reportlab` - PDF generation

4. **Verify Python installation**:
   ```bash
   pip list | grep -E "flask|transformers|pymongo|bcrypt"
   ```

---

## Configuration

### Environment Variables

Create a `.env` file in the `backend/` directory:

```bash
# MongoDB Connection (from MongoDB Atlas)
MONGO_URI="mongodb+srv://username:password@cluster.mongodb.net/?retryWrites=true&w=majority&appName=cluster"

# JWT Secret Key (use a strong, random string)
SECRET_KEY="your-secret-key-here-min-32-chars"
```

**⚠️ Security Note**: Never commit `.env` to version control. Add it to `.gitignore`.

### MongoDB Setup

1. **Create MongoDB Atlas Account**: [https://www.mongodb.com/cloud/atlas](https://www.mongodb.com/cloud/atlas)
2. **Create a Cluster**: Choose a region close to your deployment
3. **Create Database**: Name it `talqs`
4. **Create Collection**: Name it `users`
5. **Generate Connection String**: Copy the URI with credentials
6. **Add to `.env`**: Paste the URI in `MONGO_URI`

### Vite Configuration

The `vite.config.js` includes:
- React plugin via `@vitejs/plugin-react`
- Tailwind CSS plugin via `@tailwindcss/vite`
- Base path set to `/`

Modify if deploying to a subdirectory:
```javascript
export default defineConfig({
  base: "/your-subdirectory/",  // Change this
  plugins: [tailwindcss(), react()],
})
```

---

## Running the Application

### Development Mode

#### Terminal 1 - Frontend (React Dev Server)

```bash
cd talqs_bot
npm run dev
```

Output:
```
  VITE v6.2.0  ready in XXX ms

  ➜  Local:   http://localhost:5173/
  ➜  Press h to show help
```

**Frontend available at**: `http://localhost:5173`

#### Terminal 2 - Backend (Flask API Server)

```bash
cd backend/backend
source venv/bin/activate  # Activate virtual environment
python app.py
```

Output:
```
 * Serving Flask app 'app'
 * Debug mode: on
 * Running on http://127.0.0.1:5000
```

**Backend API available at**: `http://localhost:5000`

### Production Mode

#### Build Frontend

```bash
npm run build
```

Generates optimized files in `dist/` directory.

```bash
npm run preview  # Preview production build locally
```

#### Deploy Backend

```bash
# Remove debug mode, set environment to production
# Recommended: Use Gunicorn or similar WSGI server
pip install gunicorn
gunicorn -w 4 -b 0.0.0.0:5000 app:app
```

---

## API Reference

### Authentication Endpoints

#### `POST /signup`
Register a new user.

**Request**:
```json
{
  "email": "user@example.com",
  "password": "securePassword123"
}
```

**Response (201)**:
```json
{
  "message": "signup successful"
}
```

**Error (400)**:
```json
{
  "message": "user already exists"
}
```

---

#### `POST /login`
Authenticate user and return JWT token.

**Request**:
```json
{
  "email": "user@example.com",
  "password": "securePassword123"
}
```

**Response (200)**:
```json
{
  "message": "Login successful",
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "user": "user@example.com"
}
```

**Error (401)**:
```json
{
  "message": "Invalid credentials"
}
```

---

#### `POST /verify-token`
Validate JWT token expiration and signature.

**Request**:
```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

**Response (200)**:
```json
{
  "valid": true,
  "email": "user@example.com"
}
```

**Error (401)**:
```json
{
  "valid": false,
  "error": "Token expired"
}
```

---

### Legal AI Endpoints

#### `POST /ask`
Answer legal questions using DistilBERT QA pipeline.

**Request**:
```json
{
  "question": "What is the difference between copyright and trademark?"
}
```

**Response (200)**:
```json
{
  "answer": "Copyright protects original works of authorship... [answer extracted from LEGAL_CONTEXT]"
}
```

**Error (400)**:
```json
{
  "answer": "⚠️ Please provide a question."
}
```

---

#### `POST /generate_nda_pdf`
Generate customized NDA PDF document.

**Request**:
```json
{
  "disclosingParty": "Company A Inc.",
  "receivingParty": "Company B LLC",
  "date": "2025-06-24",
  "purpose": "Business Discussion"
}
```

**Response (200)**:
- Returns PDF file as attachment: `NDA_Document.pdf`

**Error (500)**:
```json
{
  "answer": "❌ Error: [error message]"
}
```

---

### Database Endpoints

#### `GET /test-db`
Test MongoDB connection and list all users.

**Response (200)**:
```json
{
  "success": true,
  "users": ["user1@example.com", "user2@example.com"]
}
```

---

## Frontend Features

### Pages & Components

#### 1. **Login Page** (`src/pages/login.jsx`)
- Email/password authentication
- Forgot password link
- Sign-up redirect
- Animated backdrop with gradient
- Responsive design (mobile-first)
- Features: Framer Motion animations, backdrop blur

#### 2. **Signup Page** (`src/pages/signup.jsx`)
- User registration form
- Email validation
- Password strength indication
- Link to login page
- Error handling

#### 3. **Home Page** (`src/App.jsx`)
- Welcome section with username personalization
- Feature showcase sections
- Navigation bar
- Feature cards
- Legal case simulation
- Footer

#### 4. **QA Chatbot** (`src/pages/qachatbot.jsx`)
- Real-time legal Q&A interface
- Sidebar chat history
- Message timestamps
- Copy & regenerate buttons for bot responses
- Typing indicator
- User/bot message differentiation with icons
- Scroll-to-latest message behavior

#### 5. **Legal Dictionary** (`src/pages/LegalDictionary.jsx`)
- Search legal terminology
- Result cards with definitions
- Browse by category
- Responsive layout

#### 6. **NDA Template Editor** (`src/pages/Ndatemplate.jsx`)
- Customizable NDA form fields
- PDF download functionality
- Disclosing party, receiving party inputs
- Date & purpose fields
- Live preview

#### 7. **IPC Sections Reference** (`src/pages/ipcsecs.jsx`)
- Indian Penal Code sections lookup
- Section descriptions & punishments
- Category filtering
- Search functionality

#### 8. **Legal Case Simulation** (`src/pages/nextpage.jsx`)
- Interactive case scenario exploration
- Legal outcome predictions
- Educational purpose

#### 9. **Note-Taking** (`src/pages/NotePage.jsx`)
- Rich text editor (React Quill)
- Save & retrieve notes
- Export to PDF or text
- Syntax highlighting

#### 10. **Summarization** (`src/pages/summarization.jsx`)
- Document upload/paste
- Automatic summarization
- Adjustable summary length

### Navigation & Layout

**Navbar** (`src/pages/Navbar.jsx`):
- Links to all major pages
- User authentication status display
- Logo & branding
- Responsive mobile menu

**Footer** (`src/pages/footer.jsx`):
- Company information
- Quick links
- Social media links

### Styling

- **Tailwind CSS** for utility-first styling
- **Custom CSS** with animations:
  - `waveAnimation` - Background wave effect
  - `float` - Floating element animation
  - `blurPulse` - Pulse blur effect
- **Framer Motion** for complex animations
- **Dark theme** with gradient backgrounds (indigo-900 to purple-800)
- **Responsive breakpoints** for mobile, tablet, desktop

---

## Backend Services

### Flask Application (`backend/backend/app.py`)

#### Core Functionality

1. **Initialization**
   - Load environment variables from `.env`
   - Initialize Flask app with CORS support
   - Load DistilBERT QA pipeline on startup

2. **Middleware**
   - CORS headers enabled for all routes
   - JSON request/response handling
   - Error handling with appropriate HTTP status codes

#### Key Features

**NLP Processing**:
```python
qa_pipeline = pipeline("question-answering", 
                      model="distilbert-base-cased-distilled-squad")
```
- Uses DistilBERT (distilled version of BERT) for efficient QA
- Accepts legal context + question
- Returns extracted answer from context

**PDF Generation**:
- Uses ReportLab for document creation
- Generates formatted NDA with sections
- Includes borders, headers, bullet points
- Returns as downloadable attachment

**Password Security**:
```python
# Registration: Hash password with bcrypt
hashed_password = bcrypt.hashpw(password.encode('utf-8'), bcrypt.gensalt())

# Login: Compare provided password with stored hash
bcrypt.checkpw(password.encode("utf-8"), stored_hash)
```

**JWT Token Management**:
- Token expires after 1 hour
- Contains user email in payload
- Uses `SECRET_KEY` from environment
- Algorithm: HS256

### Database Connection (`backend/backend/database.py`)

```python
from pymongo import MongoClient

MONGODB_URI = os.getenv("MONGODB_URI")
client = MongoClient(MONGODB_URI)
db = client["talqs"]
users_collection = db["users"]
```

**Collections**:
- `users` - Stores user records with schema:
  ```json
  {
    "_id": ObjectId,
    "email": "user@example.com",
    "password": "bcrypt_hashed_password"
  }
  ```

---

## Database

### MongoDB Schema

**Database**: `talqs`

**Collection**: `users`

```javascript
{
  "_id": ObjectId("507f1f77bcf86cd799439011"),
  "email": {
    "type": "String",
    "required": true,
    "unique": true
  },
  "password": {
    "type": "BinData",  // bcrypt hash
    "required": true
  },
  "created_at": {
    "type": "Date",
    "default": "Date.now()"
  }
}
```

### Database Indexes

Recommended indexes for performance:

```javascript
db.users.createIndex({ "email": 1 }, { unique: true })
```

### Connection Pool

- **Default pool size**: 10 connections
- **Configurable via**: `maxPoolSize` parameter in connection URI
- **Recommended**: 20-50 for production

---

## Authentication

### JWT Token Structure

**Header**:
```json
{
  "alg": "HS256",
  "typ": "JWT"
}
```

**Payload**:
```json
{
  "email": "user@example.com",
  "exp": 1719338400,  // Unix timestamp (1 hour from issue)
  "iat": 1719334800
}
```

**Signature**: HMAC-SHA256(`header.payload`, `SECRET_KEY`)

### Token Lifecycle

1. **Creation**: User logs in, token generated with 1-hour expiration
2. **Storage**: Stored in browser's `localStorage` as `token`
3. **Transmission**: Sent in request body for API calls
4. **Validation**: `/verify-token` validates signature and expiration
5. **Refresh**: User must log in again after 1 hour

### Password Hashing

**Algorithm**: bcrypt (cost factor: 10)

**Process**:
1. Generate salt: `bcrypt.gensalt()`
2. Hash password: `bcrypt.hashpw(password, salt)`
3. Storage: Save full hash (salt + hash)
4. Verification: `bcrypt.checkpw(input, stored_hash)` - returns boolean

---

## Development Workflow

### Local Development

1. **Start virtual environment** (Backend):
   ```bash
   cd backend/backend
   source venv/bin/activate
   ```

2. **Run Flask development server** (Terminal 1):
   ```bash
   python app.py
   # Server: http://localhost:5000 (debug mode enabled)
   ```

3. **Run Vite dev server** (Terminal 2):
   ```bash
   npm run dev
   # Client: http://localhost:5173 (HMR enabled)
   ```

4. **Make changes** → Auto-reload on both client & server

### Debugging

**Flask Debugging**:
- Debug mode enabled in `app.py`
- Debugger runs on port 5001 when enabled
- Use print statements or debugger breakpoints

**React Debugging**:
- React DevTools browser extension
- Vite provides source maps for debugging
- Network tab shows API calls to `localhost:5000`

### Testing

**Test MongoDB Connection**:
```bash
curl http://localhost:5000/test-db
```

**Test Login Flow**:
```bash
curl -X POST http://localhost:5000/login \
  -H "Content-Type: application/json" \
  -d '{"email":"user@example.com","password":"password123"}'
```

**Test QA Endpoint**:
```bash
curl -X POST http://localhost:5000/ask \
  -H "Content-Type: application/json" \
  -d '{"question":"What is a contract?"}'
```

---

## Key Components

### Frontend Components

| Component | Purpose | Key Props | File |
|-----------|---------|-----------|------|
| `App` | Main router & layout | - | `src/App.jsx` |
| `Login` | Authentication form | - | `src/pages/login.jsx` |
| `Signup` | Registration form | - | `src/pages/signup.jsx` |
| `Navbar` | Navigation menu | - | `src/pages/Navbar.jsx` |
| `QABotChat` | Q&A interface | - | `src/pages/qachatbot.jsx` |
| `LegalDictionary` | Terminology search | - | `src/pages/LegalDictionary.jsx` |
| `Ndatemplate` | NDA editor | - | `src/pages/Ndatemplate.jsx` |
| `IPCSections` | IPC lookup | - | `src/pages/ipcsecs.jsx` |
| `NotePage` | Note editor | - | `src/pages/NotePage.jsx` |
| `Summarization` | Doc summarizer | - | `src/pages/summarization.jsx` |
| `WelcomePage` | Hero section | `username` | `src/assets/WelcomePage.jsx` |

### Backend Modules

| Module | Purpose | Key Functions |
|--------|---------|---------------|
| `app.py` | Flask application | `signup()`, `login()`, `ask_question()`, `generate_nda_pdf()`, `verify_token()` |
| `database.py` | MongoDB connection | `users_collection` |
| `transformers` | NLP pipeline | `pipeline("question-answering", model="distilbert...")` |

---

## Troubleshooting

### Common Issues

#### **1. MongoDB Connection Error**

**Error**: `pymongo.errors.ServerSelectionTimeoutError`

**Solutions**:
- Verify `MONGO_URI` in `.env` is correct
- Check MongoDB Atlas IP whitelist includes your IP
- Ensure cluster is running in MongoDB Atlas
- Test connection: `curl http://localhost:5000/test-db`

#### **2. CORS Error (Frontend)**

**Error**: `Access to XMLHttpRequest blocked by CORS policy`

**Solutions**:
- Ensure Flask app has `CORS(app)` initialized
- Verify API URL is `http://localhost:5000` (not HTTPS locally)
- Clear browser cache & hard refresh (Ctrl+Shift+R)
- Check browser console for actual error

#### **3. JWT Token Expired**

**Error**: `{"valid": false, "error": "Token expired"}`

**Solutions**:
- User must log in again
- Token expiration is 1 hour by default
- Modify in code: `datetime.timedelta(hours=1)` → change hours value

#### **4. Model Download Timeout**

**Error**: `transformers` module downloads model on first run

**Solutions**:
```bash
# Pre-download model before running app
python -c "from transformers import pipeline; pipeline('question-answering', model='distilbert-base-cased-distilled-squad')"
```

#### **5. Vite Port Already in Use**

**Error**: `EADDRINUSE: address already in use :::5173`

**Solutions**:
```bash
# Kill process on port 5173
lsof -ti:5173 | xargs kill -9

# Or specify different port
npm run dev -- --port 3000
```

#### **6. Flask Port Already in Use**

**Error**: `Address already in use`

**Solutions**:
```bash
# Kill process on port 5000
lsof -ti:5000 | xargs kill -9

# Or specify different port in app.py
app.run(debug=True, port=5001)
```

#### **7. Python Virtual Environment Issues**

**Error**: `Command 'python' not found` or permission denied

**Solutions**:
```bash
# Ensure Python 3 is installed
python3 --version

# Use python3 explicitly
python3 -m venv venv
source venv/bin/activate

# On Windows
python -m venv venv
venv\Scripts\activate
```

#### **8. Missing Dependencies**

**Error**: `ModuleNotFoundError: No module named 'flask'`

**Solutions**:
```bash
# Ensure virtual environment is activated
source venv/bin/activate

# Reinstall requirements
pip install -r requirements.txt --force-reinstall
```

### Performance Optimization

**Frontend**:
- Use React DevTools Profiler to identify slow components
- Implement code splitting with `React.lazy()` & `Suspense`
- Monitor bundle size: `npm run build` → check `dist/`

**Backend**:
- Cache model after first load (avoid re-downloading)
- Use connection pooling for MongoDB
- Consider async/await for non-blocking operations

### Logging & Monitoring

**Flask Logging**:
```python
import logging
logging.basicConfig(level=logging.DEBUG)
logger = logging.getLogger(__name__)
logger.info("Message")
```

**React Logging**:
```javascript
console.log("Debug message");
console.error("Error:", error);
```

---

## Additional Resources

- **React Documentation**: [react.dev](https://react.dev)
- **Vite Guide**: [vitejs.dev](https://vitejs.dev)
- **Tailwind CSS**: [tailwindcss.com](https://tailwindcss.com)
- **Flask Documentation**: [flask.palletsprojects.com](https://flask.palletsprojects.com)
- **MongoDB**: [docs.mongodb.com](https://docs.mongodb.com)
- **Transformers Library**: [huggingface.co/transformers](https://huggingface.co/transformers)
- **Framer Motion**: [framer.com/motion](https://www.framer.com/motion/)
- **ReportLab**: [reportlab.com](https://www.reportlab.com/)

---

## Contributing

Contributions are welcome! Please follow these guidelines:

1. **Fork** the repository
2. **Create a feature branch**: `git checkout -b feature/your-feature`
3. **Commit changes**: `git commit -m "Add your feature"`
4. **Push to branch**: `git push origin feature/your-feature`
5. **Open Pull Request**: Describe changes & reference issues

---

## License

This project is open source and available under the MIT License.

---

## Contact & Support

For questions or issues:
- **GitHub Issues**: [Create an issue](https://github.com/bhaavyaram/talqs_bot/issues)
- **Email**: [Contact via GitHub profile](https://github.com/bhaavyaram)

---

**Last Updated**: June 24, 2025  
**Repository**: [bhaavyaram/talqs_bot](https://github.com/bhaavyaram/talqs_bot)  
**Status**: Active Development
