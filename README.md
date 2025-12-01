# 🚆 RailGuard + Rail360 Backend

Smart train assistant that shows **live train status + weather** for Indian Railways and powers the **RailGuard Zoho Cliq bot**.

- 🔁 Live train status from IRCTC (via RapidAPI)
- 🌦 Real-time weather from OpenWeatherMap
- 🤖 Zoho Cliq bot commands for students / travellers
- 🌐 Deployed backend on Railway.app (`rail360-backend-production.up.railway.app`)

---

## 📌 1. Project Overview

This project has **two main parts**:

1. **Rail360 Backend (FastAPI)**
   - Python FastAPI server
   - Exposes simple APIs for:
     - train + weather status
     - dual weather (current + destination)
     - normal city weather

2. **RailGuard Bot (Zoho Cliq)**
   - Deluge message handler
   - Calls the FastAPI backend
   - Provides easy slash commands like `/rail360`, `/alert`, `/weather` etc.

The idea:  
> Type a command in Zoho Cliq → Bot calls backend → backend calls IRCTC + OpenWeather → nicely formatted reply in chat.

---

## 🏗 2. Architecture

**External APIs**

- IRCTC Live Train Status – via **RapidAPI**  
- OpenWeatherMap – Current weather by **city name**

**Backend**

- Python 3
- FastAPI
- Hosted on **Railway.app**

**Bot**

- Zoho Cliq Bot
- Deluge (Zoho’s scripting language)
- Message Handler → calls FastAPI 

---

## ⚙️ 3. Tech Stack

- **Language**: Python (FastAPI), Deluge (Zoho)
- **Framework**: FastAPI
- **Hosting**: Railway.app
- **External APIs**:
  - `indian-railway-irctc` (RapidAPI)
  - `api.openweathermap.org`
- **Others**:
  - `requests` for HTTP
  - `uvicorn` as ASGI server

---

## 🔑 4. Configuration & Environment Variables

> ⚠️ Never hard-code real API keys in public repos.  
> Always store them inside *Railway.app → Variables* section.

Required environment variables:

```bash
OPENWEATHER_API_KEY=<your_openweather_api_key>
RAPID_RAIL_KEY=<your_rapidapi_irctc_key>

🧪 5. API Endpoints
1️⃣ Train + 3-Weather (origin, current, destination)
GET /api/rail-360?train_no=<train>&station_code=<code>&departure_date=<YYYYMMDD>

Example:

/api/rail-360?train_no=20683&station_code=MS&departure_date=20251130

2️⃣ Dual Weather (current + destination)
GET /api/rail-360-two-weather?train_no=<train>&departure_date=<YYYYMMDD>

Example:

/api/rail-360-two-weather?train_no=20683&departure_date=20251130

3️⃣ City Weather
GET /api/weather?city=Chennai

🤖 6. Zoho Cliq Bot Commands
Command	Purpose
/rail360 <train_no> <YYYYMMDD>	Live status + origin/current/destination weather
/rail360two <train_no> <YYYYMMDD>	Live status + current & destination weather
/checktrain <train_no> <YYYYMMDD>	Alias of /rail360two
/livestatus <train_no> <YYYYMMDD>	Alias of /rail360two
/alert <train_no> <YYYYMMDD> <station_code>	Station distance alert (near / next / far)
/weather <city>	Current weather for any city
/help	Show all supported commands
/ping	Check if the bot is active

📦 7. Folder Structure
.
├── main.py              # FastAPI backend code
├── requirements.txt     # Python dependencies
└── README.md            # Documentation (this file)

🚀 8. Deployment (Railway.app)

Create a new project on Railway.app

Connect your GitHub repository

Set environment variables:

OPENWEATHER_API_KEY=<your_openweather_api_key>
RAPID_RAIL_KEY=<your_rapidapi_irctc_key>


Deploy the service

Note the public URL
https://rail360-backend-production.up.railway.app

Use this URL inside your Zoho Cliq Deluge code (base_url).

🧠 9. Why This Project?

This project solves a real problem for Indian train passengers:

Combines live train status + live weather

Simple chat commands inside Zoho Cliq

Useful for students and daily travellers who want “all info in one place”.

✨ 10. Author

👤 Subanesh Selvam
Electronics and Communication Engineering (ECE) Student
Backend & API Integrations • India
