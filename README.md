# DiagnosX
DiagnosX — Full-Stack AI Symptom Checker & amp; Doctor Recommendation System

DiagnosX — Full-Stack AI Symptom Checker & Doctor Recommendation SystemAn enterprise-grade, full-stack Single Page Application (SPA) designed to evaluate patient symptoms using Machine Learning, determine triage urgency levels, and match patients with specialized healthcare providers for seamless appointment booking.Built on a hybrid MERN Stack + Python FastAPI Microservice architecture, DiagnosX demonstrates modern full-stack web development, token-based authentication, real-time AI processing, NoSQL data modeling, and Docker container orchestration.📸 System Architecture & Overview                          

                          ┌───────────────────────────┐
                          │    React + Vite SPA       │
                          │   (Tailwind, Redux)       │
                          └─────────────┬─────────────┘
                                        │ (REST / JWT)
                                        ▼
                          ┌───────────────────────────┐
                          │   Express.js API Gateway  │
                          │  (Auth, Routing, Mongo)   │
                          └──────┬─────────────┬──────┘
                                 │             │
                   (Internal API)│             │(Mongoose)
                                 ▼             ▼
          ┌───────────────────────────┐   ┌───────────────────────────┐
          │   Python FastAPI Engine   │   │     MongoDB Database      │
          │  (Symptom Triage / ML)    │   │  (Users, Triage, Appts)   │
          └───────────────────────────┘   └───────────────────────────┘

Key Features
AI-Powered Symptom Triage: Interactive multi-step form capturing body region, duration, severity index (1-10), and custom symptom vectors routed to a Python ML microservice. Doctor Match Engine: Dynamic search and filtering system matching triage outcome specialties (Cardiology, Neurology, Pulmonology, etc.) with available specialist doctor profiles. Instant Consultation Booking: Interactive slot selection modal connected with live appointment state persistence.Patient Dashboard: Patient history tracking with full assessment log exports (JSON format) and active WebRTC consultation links. Doctor Triage Portal: Specialized portal allowing doctors to review incoming patient referrals, examine AI confidence scores, and accept cases. Embedded Architecture Viewer: Interactive code and diagram viewer directly in the application UI demonstrating production backend, microservice, schema, and configuration source codes. 

Technology Stack

Layer                      Technologies Used
Frontend                   React 18, Vite, Tailwind CSS, Redux Toolkit React Router v6, Lucide Icons
Backend API Gateway        Node.js, Express.js, JSON Web Tokens (JWT), Bcrypt.js, Axios
AI Microservice            Python 3.10+, FastAPI, Pydantic, Uvicorn
Database                   MongoDB, Mongoose ODM
DevOps & Containerization  Docker, Docker Compose 

Repository Layout

diagnosx/
├── client/                 # React + Vite Frontend
│   ├── src/
│   │   ├── components/     # UI Components (Checker, Doctors, Portals)
│   │   ├── features/       # Redux Slices (Auth, Symptoms, Doctors)
│   │   └── services/       # Axios API Client Interceptors
│   └── package.json
│
├── server/                 # Express.js Backend Service
│   ├── src/
│   │   ├── controllers/    # API Controllers
│   │   ├── models/         # Mongoose Schemas (User, Assessment, Appointment)
│   │   └── middleware/     # JWT Auth Verification
│   └── package.json
│
├── ai-service/             # Python FastAPI ML Microservice
│   ├── app/
│   │   ├── main.py         # FastAPI Entrypoint & Routes
│   │   └── ml_engine/      # Symptom Triage Matrix Logic
│   └── requirements.txt
│
└── docker-compose.yml      # Multi-container orchestration config

Quick Start & Local SetupOption 1: Docker Compose (Recommended)Run the entire full-stack application environment (MongoDB, FastAPI, Express, React) with a single command:# Clone repository
git clone https://github.com/your-username/diagnosx.git
cd diagnosx

# Boot up all services in containerized environment
docker-compose up --build
Access the components:Frontend SPA: http://localhost:80Express Backend: http://localhost:5000FastAPI Microservice Docs: http://localhost:8000/docsOption 2: Local Manual Setup1. MongoDBEnsure MongoDB is running locally on port 27017 or obtain a Mongo Atlas connection string.2. Python FastAPI Microservicecd ai-service
python -m venv venv
source venv/bin/activate # On Windows: venv\Scripts\activate
pip install -r requirements.txt
uvicorn app.main:app --reload --port 8000
3. Express Backend Servercd server
npm install
# Create .env file based on .env.example
npm run dev
4. React Vite Clientcd client
npm install
npm run dev

Environment Variables Configurationserver/.envPORT=5000
MONGO_URI=mongodb://localhost:27017/diagnosx_db
FASTAPI_SERVICE_URL=http://localhost:8000
JWT_SECRET=super_secret_jwt_token_key_2026
ai-service/.envHOST=0.0.0.0
PORT=8000
MODEL_VERSION=v2.1.0-biobert

API Endpoints OverviewMethodEndpointDescriptionAuth RequiredPOST/api/auth/registerRegister a new userNoPOST/api/auth/loginAuthenticate & retrieve JWT tokenNoPOST/api/symptoms/analyzeSubmit symptoms -> FastAPI proxy -> Save AssessmentYes (JWT)GET/api/doctorsRetrieve matched doctor directoryYes (JWT)POST/api/appointmentsBook consultation appointment slotYes (JWT)POST/predict (FastAPI)ML Symptom Triage Inference EndpointInternal API Key📄 LicenseDistributed under the MIT License.
