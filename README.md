# Digital-Will-Vault
Secure digital legacy vault with Dead Man's Switch, multi-party crypto key sharding, AI personalized video/audio messages, auto subscription cancellation, and funeral wish lists.
Here is the **"Read Me"** text—written as if this app is ready to ship on the App Store. 

I've written it in three formats depending on where you need it:

---

## Option 1: The App Store / Product Landing Page (Marketing Copy)

---

# Tempest – Hyper-Local Micro-Weather

**"Your city says 10% chance of rain. Your street says 'get inside.'"**

Stop trusting weather stations 20 miles away. Tempest turns the barometers in thousands of nearby phones into a crowdsourced pressure map—predicting rain on your *exact block* within 15 minutes.

**How it works:**
- 50 phones in your neighborhood suddenly drop in pressure? 
- Tempest alerts you before the first drop hits your rooftop.
- Rain two blocks away? You stay dry. Rain on your head? We warned you.

**Earn Forecast Points.** Report what you see. Train our AI to weigh the most accurate phone sensors. The more you contribute, the sharper your alerts become.

**Battery-friendly.** Smart polling adapts to your movement—desk, walk, or drive.

**Perfect for:** Commuters, outdoor events, urban farmers, and anyone tired of carrying an umbrella "just in case."

**Download Tempest. Outsmart the sky.**

---

## Option 2: The Developer / GitHub Repository "README.md" (Technical)

---

# Tempest – Crowdsourced Micro-Weather v1.0

### Overview
Tempest is an iOS/Android application that uses MEMS barometer data from user devices to generate hyper-local (100m x 100m) rainfall predictions with a 15-minute lead time. 

Unlike traditional radar-based forecasting, Tempest detects the *pressure precursor* of microbursts and thunderstorms by aggregating relative pressure changes (ΔP/Δt) across densely populated grid cells.

### Core Architecture
- **Sensor Fusion:** Barometer (Bosch BMP390 / equivalent) + Accelerometer + GPS.
- **Noise Filtering:** Altitude changes (stairs/elevators) are subtracted using GPS elevation and motion context.
- **Crowd Consensus:** A grid cell requires a minimum of 20 active devices within a 5-minute rolling window to trigger an alert. 
- **Weighted Voting:** Each device model has a "Sensor Reliability Score" (0–100) based on historical drift accuracy.

### Gamification Logic
- **+10 Points** for confirming a correct forecast ("Yes, it's raining").
- **-50 Points** for false reporting (detected via pressure map divergence).
- **Leaderboards** by neighborhood. Top forecasters earn "Storm Chaser" badges.

### Battery Optimization
- **Stationary mode:** Poll barometer every 60 seconds.
- **Motion mode:** Poll every 5 minutes + apply altitude correction.
- Background processing uses the `CMSensorRecorder` (iOS) / `SensorManager` (Android) with wake locks minimized.

### API Endpoints (Backend)
- `POST /api/v1/pressure` – Submit device pressure + GPS + timestamp.
- `GET /api/v1/forecast/{lat}/{lon}` – Retrieve 15-min micro-forecast for grid cell.
- `GET /api/v1/leaderboard` – Return top 100 users by Forecast Points.

### Dependencies
- Python 3.10 (FastAPI backend)
- PostgreSQL + PostGIS (spatial grid indexing)
- Redis (real-time pressure stream aggregation)
- TensorFlow Lite (on-device sensor calibration)

### Known Limitations
- **Stadium Mode:** Grid cells with >500 devices in synchronized motion (e.g., sports crowds) are automatically excluded to prevent HVAC/crowd-wave false positives.
- **Rural Areas:** Requires minimum device density. Forecasts fall back to national radar API when <20 devices are active in a 5km radius.

### Installation (Dev)
```bash
git clone https://github.com/yourrepo/tempest.git
cd tempest/backend
pip install -r requirements.txt
uvicorn main:app --reload
```

### Contributing
Submit PRs for sensor calibration models or new gamification mechanics. All contributions must pass battery-drain tests (<3% per hour).

---

## Option 3: The In-App "First-Time User" Walkthrough (Friendly & Short)

---

**Welcome to Tempest.**

You just joined a neighborhood weather network powered by *your phone's pressure sensor*.

**Here's the deal:**
1. Keep the app running in the background.
2. When the pressure drops around you, we'll send a **15-minute rain alert** for your exact block.
3. When it starts raining, tap **"Confirm"** to earn Forecast Points.
4. The more points you earn, the more accurate your alerts become—because we learn which sensors to trust.

**No typing. No widgets. Just open, forget, and get alerted.**

One rule: Don't fake a report. Our pressure map knows if you're lying. 😉

**Ready? Let's predict the sky.**

