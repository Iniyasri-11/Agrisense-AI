# AgriSense AI: Smart Farming Platform

AgriSense AI is a modern, responsive, and user-friendly web application designed for farmers. The platform integrates **FastAPI (Backend)**, **React.js + Tailwind CSS v4 (Frontend)**, and **MongoDB** to collect and monitor real-time agricultural telemetry from simulated Wokwi ESP32 nodes, generate AI predictions, and offer bilingual voice assistance.

---

## 🌟 Key Features

*   **Bilingual Localization:** Full support for **English** and **தமிழ் (Tamil)** across login forms and dashboard cards, switchable on-the-fly.
*   **Secure Authentication:** Secure Login and Signup forms built with `react-hook-form` and input validation.
*   **Google Single Sign-On:** Fully connected *Continue with Google* login flow, which automatically registers Google user accounts on the backend.
*   **Real-time Sensor Dashboard:** Sleek cards displaying:
    *   Soil Moisture (%)
    *   Temperature (°C)
    *   Humidity (%)
    *   Rainfall (mm)
    *   Water Tank Level (%)
*   **Historical Trends:** Graphical analysis of weekly soil moisture trends and water pump usage powered by Recharts.
*   **Crop Simulation Controller:** Adjust sliding inputs to mock telemetry changes in real time and watch predictive warnings react instantly.
*   **AI Prediction Cards:**
    *   **Smart Irrigation:** Warns if moisture drops below threshold guidelines.
    *   **Disease Detection:** Diagnoses crop molds or leaf rot pathogens.
    *   **Yield Predictor:** Estimates expected output tonnage using pH, rainfall, and climate data.
*   **Floating Voice Assistant:** Persistent microphone widget supporting bilingual speech recognition, transcription text, waveform animations, and audio speech synthesis.

---

## 🛠️ Technology Stack

### Frontend
*   **Core:** React.js, Vite
*   **Styling:** Tailwind CSS v4, Lucide Icons
*   **Form Management:** React Hook Form
*   **Charts:** Recharts
*   **Multilingual Support:** i18next, react-i18next
*   **API Client:** Axios

### Backend
*   **Framework:** FastAPI (Python)
*   **Server:** Uvicorn
*   **Audio Transcription:** Whisper AI integration
*   **Speech Synthesis:** Edge-TTS audio generator
*   **Validation:** Pydantic

### Database
*   **Engine:** MongoDB (with dynamic in-memory fallback for offline development)

---

## 🔌 Wokwi Simulator & Cloud Integration

The platform is designed to receive cloud telemetry from physical ESP32 boards simulated inside **Wokwi**.

### How Wokwi Updates the Database:
Your Wokwi C++ sketch can submit HTTP `POST` requests to update the IoT database in real time.

*   **API Endpoint:** `POST http://<your-backend-ip>:8000/api/sensor-data`
*   **Wokwi Client JSON Payload:**
```json
{
  "crop_type": "Paddy",
  "growth_stage": "Flowering",
  "soil_moisture": 28,
  "temperature": 32,
  "humidity": 65,
  "rainfall": 27.5,
  "soil_ph": 6.4,
  "water_tank_level": 80,
  "disease_detected": "None",
  "yield_prediction": "12 tons/acre",
  "weather_forecast": "Partly Cloudy"
}
```

---

## 📂 MongoDB Schema Reference

The database `agrisense_ai` stores data in three main collections:

1.  **`users`:** Holds farmer credentials and profiles:
    ```json
    {
      "fullName": "Iniyasri",
      "email": "iniyasrisv11@gmail.com",
      "mobileNumber": "9791578864",
      "preferredLanguage": "en",
      "cropType": "Paddy"
    }
    ```
2.  **`sensor_data`:** Stores the active IoT telemetry mapping (`_id: "current_sensor_data"`):
    ```json
    {
      "_id": "current_sensor_data",
      "soil_moisture": 25,
      "temperature": 31,
      "humidity": 65
    }
    ```
3.  **`history`:** Records queries processed by the AI voice assistant:
    ```json
    {
      "query": "When should I irrigate my crop?",
      "response": "Your soil moisture is low at 25%. Irrigation is recommended.",
      "language": "en",
      "audio_filename": "response_abc123.mp3"
    }
    ```

---

## 🚀 Getting Started

### Prerequisites
*   Node.js (v18+)
*   Python (v3.10+)
*   MongoDB (Installed locally on port `27017`)

### 1. Setup Backend
Activate the pre-configured virtual environment and start the FastAPI service:
```bash
# Activate virtual environment
.venv\Scripts\activate

# Start the uvicorn API server
python -m uvicorn backend.main:app --port 8000
```
*The API documentation will be available at `http://localhost:8000/docs`.*

### 2. Setup Frontend
Install client-side dependencies and launch the Vite compiler:
```bash
# Navigate to frontend folder
cd frontend

# Install packages
npm install

# Run Vite dev server
npm run dev
```
*Open your browser and visit `http://localhost:5173/` to interact with the platform.*
