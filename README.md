✈️ AI Travel Itinerary Builder

An AI-powered web application that generates weather-aware, day-wise travel itineraries based on a destination and travel date using the Groq LLaMA model and RapidAPI weather forecast API.
📦 Project Structure

    travel_backend/        # Django backend
    ├── config/              # Django settings
    ├── itinerary/           # App with views, serializers, weather, groq logic
    ├── manage.py
    
    travel-frontend/         # React frontend (Vite or CRA)
    ├── src/
    │   ├── components/
    │   ├── App.jsx
    │   └── main.jsx

⚙️ Setup Instructions
🔁 Backend (Django)

    Clone the repo and install dependencies:

cd travel_itinerary
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate
pip install -r requirements.txt

    Run the Django server:

python manage.py runserver

🌐 Frontend (React)

cd travel-frontend
npm install
npm run dev   # or npm start for CRA

    Make sure the Django server is running on http://127.0.0.1:8000.

🔑 API Keys Required

Create a .env file (or set directly in code if testing).
1️⃣ Groq API

    API Key: Get it from https://console.groq.com

    Usage: Used to generate an AI itinerary based on weather and location.

    Example endpoint:
    https://api.groq.com/openai/v1/chat/completions

2️⃣ Weather Forecast API (via RapidAPI)

    API Key: Get from RapidAPI Weather API

    Chosen API: weather-api167
    Endpoint:
    https://weather-api167.p.rapidapi.com/api/weather/forecast

    Example Usage:

curl --request GET \
  --url 'https://weather-api167.p.rapidapi.com/api/weather/forecast?place=London%2CGB&cnt=3&type=three_hour' \
  --header 'x-rapidapi-host: weather-api167.p.rapidapi.com' \
  --header 'x-rapidapi-key: YOUR_API_KEY'

    Weather Fields Used:

        temprature (converted from Kelvin to Celsius)

        description

        dt_txt for date filtering

📤 API Endpoint
POST /api/itinerary/

Request Body:

{
  "destination": "Paris",
  "date": "2025-07-01"
}

Response Example:

{
  "destination": "Paris",
  "date": "2025-07-01",
  "weather": {
    "temp": 27.5,
    "description": "few clouds"
  },
  "itinerary": "8 AM - Breakfast...\n10 AM - Eiffel Tower visit..."
}

📌 Assumptions & Notes

    The weather API provides 3-hour forecasts for the next 3 days only.

    The backend matches the requested date from the closest available dt_txt value.

    Weather temperature is converted from Kelvin → Celsius.

    Groq’s llama-4-scout-17b model is used for generation.

    Error handling is added for invalid input, missing forecast, and API failures.

    CORS is configured using django-cors-headers to allow frontend requests.

    The frontend is responsive and uses Tailwind CSS for styling.

🧠 Built With

    Django + Django REST Framework

    React.js (Vite or CRA)

    Groq LLM API

    RapidAPI Weather API

    Tailwind CSS
