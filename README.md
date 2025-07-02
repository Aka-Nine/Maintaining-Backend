# Attendance Management System (Backend)

This is the backend API for an Attendance Management System built using **FastAPI**. It features login and registration using both **email/password** and **facial recognition**, powered by the **ResNet-34** model for face encoding.

## 🚀 Features

- **User Management**
  - Employer and employee registration with face capture
  - Dual login methods (email/password and facial recognition)
  - Role-based access control

- **Attendance Tracking**
  - Face-based check-in and check-out
  - Hours worked calculation
  - Automatic earnings computation

- **Employer Dashboard**
  - Employee management
  - Real-time working status monitoring
  - Payment processing functionality

- **Technical**
  - RESTful API design with FastAPI
  - Asynchronous MongoDB integration using Motor
  - JWT-based authentication

## 🧠 Face Recognition Technology

This system leverages advanced facial recognition capabilities:

- **Model**: ResNet-34 (deep residual neural network)
- **Library**: [face_recognition](https://github.com/ageitgey/face_recognition)
- **Processing**: PIL, OpenCV, NumPy
- **Storage**: 128-dimension face encodings stored in MongoDB

### Precision & Accuracy Parameters

| Setting | Tolerance | Use Case |
|---------|-----------|----------|
| Login | 0.6 | Balanced security approach |
| Check-in/out | 0.65 | Slightly more lenient for daily use |

*Lower tolerance increases precision but may reject valid users; higher tolerance improves recall but may reduce security.*

## 🛠 Technologies Used

| Technology | Purpose |
|------------|---------|
| **FastAPI** | Backend web framework |
| **MongoDB** | NoSQL database (Atlas recommended) |
| **Motor** | Async MongoDB driver |
| **face_recognition** | Face encoding & comparison |
| **ResNet-34** | Face detection model |
| **bcrypt** | Password hashing |
| **JWT (PyJWT)** | Token-based authentication |
| **Pydantic** | Data validation |
| **Uvicorn** | ASGI server |
| **dotenv** | Environment configuration |

## 📁 Project Structure

```
.
├── main.py        # App entrypoint
├── auth.py        # Auth & JWT logic
├── database.py    # MongoDB setup
├── utils.py       # Utility functions (face encoding, hashing)
├── models.py      # Pydantic models
├── employee.py    # Employee APIs
├── employer.py    # Employer APIs
└── attendance.py  # Attendance APIs
```

> Frontend and testing files are separate and not included in this repository.

## 📦 Installation

1. **Clone the repo:**
   ```bash
   git clone https://github.com/your-username/attendance-system-backend.git
   cd attendance-system-backend
   ```

2. **Create .env file:**
   ```
   MONGO_URI=your_mongo_uri_here
   DATABASE_NAME=attendance_system
   SECRET_KEY=your_jwt_secret
   ```

3. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```
   *Ensure packages include: fastapi, uvicorn, python-multipart, motor, face_recognition, pillow, bcrypt, python-dotenv*

4. **Run the server:**
   ```bash
   uvicorn main:app --reload
   ```
   API will be available at: http://127.0.0.1:8000

## 🧪 API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/employer/register` | Register new employer account |
| POST | `/employee/register` | Register new employee account |
| POST | `/login/password` | Login with email/password |
| POST | `/login/face` | Login with facial recognition |
| POST | `/attendance/checkin` | Employee check-in with face |
| POST | `/attendance/checkout` | Employee check-out with face |
| GET | `/employee/attendance/summary` | Get employee's attendance history |
| POST | `/employer/pay_employee/{employee_id}` | Mark employee as paid |

## 📸 Image Upload Notes

- All face-related routes accept image uploads via `multipart/form-data`
- Images are resized and encoded internally before being matched using ResNet34-based face encodings
- Best results achieved with clear frontal face images in good lighting conditions

## 🖼 Grafix Integration

This backend is designed to work seamlessly with the Grafix dashboard UI that visualizes:
- Real-time employee status
- Attendance summaries
- Payments and earnings analytics

## 🔬 Technical Implementation Details

### Backend Architecture
- **Roles**: Employer & Employee models with distinct permissions
- **Authentication**:
  - Email/Password (JWT-secured)
  - Face login (powered by ResNet34 embeddings)
- **Database**:
  - Stores encoded face vectors (128D)
  - Tracks work sessions: check-in, check-out, total hours, and earnings
- **API Design**: Routes are modularly separated and validated using Pydantic and dependency injection

### Face Matching Logic
```python
# Example face comparison
face_recognition.compare_faces([stored_encoding], new_encoding, tolerance=0.6)
```

## ✅ Future Improvements

- Add comprehensive test suite
- Implement logging and exception handling middleware
- Connect with production-grade Grafix frontend
- Enhance security with rate limiting and additional authentication factors

---

🚀 Deployment & DevOps
This backend now includes a fully automated CI/CD pipeline using GitHub Actions, Docker, and Render:

🔁 CI/CD Workflow
Every push to master:

Builds a Docker image using GitHub Actions

Pushes to DockerHub: akanine2602/attendance-api

Triggers automatic deployment to Render via Deploy Hook

🐳 Dockerized Architecture
All services are containerized with a single Dockerfile

Environment variables are managed securely via .env and Render Dashboard

Face recognition dependencies like dlib and face_recognition are prebuilt to optimize deployment time and avoid build memory issues

🌐 Live API
Hosted on Render

Public endpoint: https://presensync-api.onrender.com

🛠 DevOps Tools Used
Tool	Purpose
Docker	Containerization of FastAPI backend
DockerHub	Hosting prebuilt image
GitHub Actions	CI/CD pipeline to automate Docker builds and deploys
Render	Cloud hosting with deploy hook support
Uvicorn	ASGI server within Docker container

✅ Developer Workflow
Push changes to master

GitHub Actions automatically:

Builds Docker image

Pushes to DockerHub

Notifies Render to redeploy

Live API is updated instantly



