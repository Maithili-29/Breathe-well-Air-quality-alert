# Breathe-Well: Air Quality Alert

## Project Description
**Breathe-Well** is a student-developed app that monitors air quality in real-time and provides alerts when pollution levels rise. The app fetches data from public AQI APIs, analyzes local air quality, and notifies users with tips to reduce exposure. The goal is to help users make informed decisions about outdoor activities and health.

**Key Features:**
- Real-time AQI monitoring based on user location
- Color-coded air quality levels: Green (Good), Yellow (Moderate), Red (Unhealthy)
- Alerts for high pollution levels
- Tips to improve indoor air quality
- Historical AQI data stored locally

---

## Technologies Used
| Technology      | Purpose |
|-----------------|---------|
| Python          | Core app logic and AQI data processing |
| Tkinter / Kivy  | GUI development for demo |
| SQLite          | Local database for storing AQI history |
| Requests / JSON | Fetch AQI data from API |
| Matplotlib      | Plotting AQI trends |
| Flask           | Optional REST API integration |

---
## How the Software Works

The Breathe-Well app works in the following steps:

1. **User Launches the App**
   - User opens the Breathe-Well application (Tkinter/Kivy GUI).
   - Dashboard loads with last recorded AQI or “--” if no data exists.

2. **User Requests AQI Update**
   - User clicks the **Refresh AQI** button.
   - This triggers the `update_dashboard()` function in `main.py`.

3. **Fetching Real-Time Air Quality Data**
   - `update_dashboard()` calls `get_aqi_data(location)` from `api_handler.py`.
   - The app requests current AQI data from a public API.
   - Example API response:
     ```json
     {
       "location": "Delhi",
       "aqi": 178
     }
     ```
   - The AQI value is interpreted into a status:
     - 0–50 → Good
     - 51–150 → Moderate
     - 151+ → Unhealthy

4. **Displaying the Dashboard**
   - The GUI updates to show:
     - Current AQI value (e.g., 178)
     - Status indicator (e.g., Unhealthy)
     - Color-coded display (Green, Yellow, Red)
   - Optional: Historical AQI trend plotted using Matplotlib.

5. **Triggering Alerts**
   - If AQI exceeds safe limits (>150), `send_alert(aqi, status)` in `notifications.py` is called.
   - Popup alert example:
     ```
     "AQI is 178 (Unhealthy). Limit outdoor activity!"
     ```
   - Provides tips to reduce outdoor exposure and improve indoor air quality.

6. **Storing Data Locally**
   - The AQI reading is saved in SQLite via `save_data(location, aqi)` in `database.py`.
   - Each record includes:
     - Location
     - AQI value
     - Timestamp
   - Historical data can be fetched using `fetch_history()` for trend analysis.

7. **Optional Backend/API**
   - Flask REST API can be integrated for multi-device access.
   - Other apps or devices can fetch AQI data from the server in real-time.

8. **User Interaction & Feedback**
   - Users can refresh AQI anytime.
   - Historical trends allow users to see if air quality is improving or worsening.
   - The app runs as a lightweight dashboard and alert system.



