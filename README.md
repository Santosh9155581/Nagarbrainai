# NagarBrain AI
### Smart City Traffic Intelligence & Emergency Response Orchestration

NagarBrain AI is an advanced, AI-driven urban orchestration platform designed to improve city operations, optimize traffic flow, and automate emergency vehicle response. By combining real-time computer vision, LLM-based incident verification, and interactive map routing, NagarBrain AI empowers citizens and municipal administrators to manage urban infrastructure dynamically.

---

##  Key Features

###  1. Adaptive Traffic Control & Signal Preemption
* **YOLOv8 Object Detection**: Uses computer vision to analyze video streams from traffic lanes in real-time, detecting cars, trucks, buses, motorcycles, and bicycles.
* **Dynamic Signal Timing**: Automatically calculates vehicle density (Low, Medium, High) and adjusts green light durations accordingly.
* **Emergency Vehicle Preemption**: Instantly identifies incoming ambulances using a specialized classification model, preempting the active signal cycle to give the ambulance immediate green light priority.

###  2. Emergency dispatch & Routing
* **Ambulance Booking**: Citizens can request an ambulance directly from their location on an interactive map.
* **Admin Dispatch Center**: Administrators can view real-time ambulance requests, locate the nearest active emergency station, and dispatch vehicles.
* **Route Optimization**: Uses Google Maps API to chart optimal navigation paths for dispatched emergency vehicles.

###  3. Citizen Incident Reporting
* **Interactive Map Reports**: Citizens can report infrastructure anomalies (e.g., garbage dumps, accidents, potholes, water logging) directly onto the map.
* **Gemini AI Verification**: Integrates Google Gemini API to analyze citizen descriptions, categorize reports, and verify the validity of reports.
* **Moderation Panel**: Admins can review active reports, coordinate field teams, and mark incidents as resolved.

---

##  System Architecture

NagarBrain AI is structured as a microservices application:

1. **Frontend (`/frontend`)**:
   * built with: React (Vite), Tailwind CSS, Lucide icons, and `@react-google-maps/api`.
   * Port: `5173` (Vite Default)

2. **Core Backend (`/backend`)**:
   * Built with: Node.js, Express, MongoDB (Mongoose).
   * **In-Memory Fallback**: If a local MongoDB instance is not detected, the backend automatically falls back to an in-memory data store, allowing instant testing without database setup!
   * Port: `5000`

3. **YOLO Computer Vision Backend (`/yolo_backend`)**:
   * Built with: Python, FastAPI, Uvicorn, Ultralytics YOLOv8, and OpenCV.
   * Port: `8000`

---

##  Environment Variables Setup

Configure the following files before running the application:

### Node.js Backend (`backend/.env`)
Create a `.env` file inside the `backend/` directory:
```env
PORT=5000
MONGO_URI=mongodb://127.0.0.1:27017/nagarbrain_traffic
HF_API_TOKEN=your_hugging_face_token_here
```

### React Frontend (`frontend/.env`)
Create a `.env` file inside the `frontend/` directory (or edit the pre-created template):
```env
VITE_GOOGLE_MAPS_API_KEY=your_google_maps_api_key_here
VITE_GEMINI_API_KEY=your_gemini_api_key_here
```

---

##  Installation & Getting Started

Open three separate terminals at the root of the project:

### 1. Start Python YOLO Backend
Navigate to the computer vision backend:
```bash
cd yolo_backend
```
* **For Python 3.14+ (New versions)**: Since older pinned packages might fail to compile, install the latest binary wheels:
  ```bash
  pip install numpy ultralytics fastapi uvicorn opencv-python-headless python-multipart requests --only-binary :all:
  ```
* **For Python 3.10 / 3.11 / 3.12**: You can run the automated script directly:
  ```bash
  .\start.bat
  ```
Once installed, start the server:
```bash
uvicorn main:app --host 0.0.0.0 --port 8000 --reload
```
Check health on: `http://localhost:8000/health`

### 2. Start Core Node.js Backend
Navigate to the Node.js API server:
```bash
cd backend
npm install
npm start
```
*Starts on: `http://localhost:5000`*

### 3. Start React Frontend
Navigate to the frontend client:
```bash
cd frontend
npm install
npm run dev
```
*Starts on: `http://localhost:5173` (Open this in your web browser)*

---

##  Repository Structure

```
nagarbrain/
├── backend/               # Node.js Express server, MongoDB models & controllers
├── frontend/              # Vite + React client & dashboard pages
├── yolo_backend/          # FastAPI server, YOLO weights & detection scripts
└── README.md              # Project documentation
```
