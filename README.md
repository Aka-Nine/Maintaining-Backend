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

| Technology             | Purpose                                                                  |
| ---------------------- | ------------------------------------------------------------------------ |
| **FastAPI**            | Backend web framework for building high-performance RESTful APIs         |
| **MongoDB (Atlas)**    | NoSQL database for storing users, attendance logs, and encodings         |
| **Motor**              | Asynchronous MongoDB driver for FastAPI integration                      |
| **face\_recognition**  | Facial encoding, comparison, and detection powered by dlib and ResNet-34 |
| **dlib**               | Core machine learning library used for facial feature extraction         |
| **ResNet-34**          | Deep CNN model used to compute 128-d face encodings                      |
| **OpenCV (cv2)**       | Webcam access and image preprocessing during face capture                |
| **Pillow (PIL)**       | Image processing (for uploaded images)                                   |
| **NumPy**              | Numerical computing used for encoding comparisons                        |
| **PyJWT**              | JSON Web Token creation and decoding for secure login sessions           |
| **bcrypt**             | Secure password hashing for email/password authentication                |
| **Pydantic**           | Data validation for request bodies and responses                         |
| **Uvicorn**            | ASGI server to serve the FastAPI application                             |
| **email-validator**    | Ensures email format is valid before account creation                    |
| **python-dotenv**      | Manages environment variables from `.env` file                           |
| **python-multipart**   | Enables file/image uploads via `multipart/form-data`                     |
| **requests**           | Used in local testing scripts to send API requests                       |
| **certifi**            | CA bundle for SSL certificate validation                                 |
| **idna**               | Internationalized domain name handling for URLs                          |
| **urllib3**            | Reliable HTTP client for Python (used internally by requests)            |
| **charset-normalizer** | Handles string encoding normalization in HTTP responses                  |
| **setuptools**         | Python packaging and installation utility                                |
| **typing-extensions**  | Compatibility for newer typing features in older Python versions         |


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
Public API: https://presensync-api.onrender.com

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



## 🚀 Deployment & DevOps
This project is production-ready with a complete DevOps pipeline:

### 🔁 CI/CD (GitHub Actions)
Trigger: On every push to master

Steps:

Build Docker image

Push to DockerHub (akanine2602/attendance-api)

Trigger deployment on Render via webhook

### 🐳 Dockerized Infrastructure
Full support via Dockerfile

Local development or containerized deployment

Image is memory-optimized to avoid build failures

### ☁️ Live Deployment (Render)
Hosted on: Render

Public API: https://presensync-api.onrender.com

Build strategy: Prebuilt Docker image (no source compile on server)

Trigger: Render deploy hook called by GitHub Action

### ✅ Developer Workflow
Make code changes

Run:

```bash

git add .
git commit -m "Update feature"
git push

```
***GitHub Actions:***

Builds the Docker image

Pushes to DockerHub

Notifies Render → new live deploy

### 📈 Future Improvements
Add test coverage with pytest

Connect with full Grafix frontend

Add HR tools like leave approvals and shift planning

Implement admin-level analytics and controls

Integrate email notifications (absences, daily logs)

Add ML-based fraud detection (duplicate face, spoofing)

### 💬 Contact
For queries, feedback, or contributions:

Author: Aka-Nine

Email: Nine.digitalServices@gmail.com
