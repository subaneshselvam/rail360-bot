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
> In production, use environment variables.

Required env vars:

```bash
OPENWEATHER_API_KEY=
'e91c6fd924313ba0b6905b5d69b8a68f"
RAPID_RAIL_KEY="06373a2f1msh54eabd13036fcb8p172ba3jsne82a30f201bf"
