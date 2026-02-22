# 🌿 AnnaData — Intelligent Farming Companion

AnnaData is a full-stack smart agriculture management platform that gives farmers real-time data, AI-powered insights, and actionable tools to optimise crop yields, monitor field conditions, and manage day-to-day farm operations.

---

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Backend Setup](#backend-setup)
  - [Frontend Setup](#frontend-setup)
- [Environment Variables](#environment-variables)
- [API Reference](#api-reference)
- [Pages & Routes](#pages--routes)
- [Internationalisation](#internationalisation)
- [Contributing](#contributing)

---

## Overview

AnnaData (repository name: **AITD**) is designed to be *your intelligent farming companion for data-driven agriculture management and crop optimisation*. It brings together weather forecasting, soil monitoring, pest detection, commodity market prices, inventory tracking, financial analysis, and WhatsApp alert notifications into a single, easy-to-use web application.

---

## Features

### 🏠 Home Dashboard
A comprehensive at-a-glance overview of your farm:
- **Welcome Section** — Quick platform introduction.
- **Technology Section** — Overview of the three core pillars: Weather Monitoring, Soil Analysis, and Crop Management.
- **Soil Monitoring** — Real-time metrics for soil moisture, temperature, and nitrogen levels with progress indicators and actionable recommendations.
- **Commodity Market Prices** — Live price tracking (Wheat, Corn, Soybeans, Cotton) with trend indicators.
- **Crop Alerts** — Colour-coded alert cards highlighting fields that need attention.
- **Farm Weather Widget** — Current temperature, humidity, wind speed, and a 3-day forecast.
- **Agricultural Pest Monitor** — Field scan results with pest-risk indicators (Aphid Activity, Corn Borer Risk) and a "Run field scan" action button.
- **Agriculture News** — Latest news headlines relevant to farming.
- **Farm Management Quick Links** — Shortcuts to Crop Reports, Yield Analytics, and Farm Settings.

### 🌦️ Weather Dashboard (`/Weather`)
- Scrolling critical-update ticker banner.
- **Weekly Forecast Carousel** — Interactive card carousel sourced from the OpenWeatherMap API, defaulting to the user's geolocation or Mapusa (Goa, India) as a fallback.
- **Weather Details Grid** — Detailed breakdown for the selected forecast day.
- Informational text section explaining the data sources and methodology.

### 🌱 Farm Management (`/resources`)
A full suite of farm-operations tools:

| Module | Description |
|---|---|
| **Crop Management** | Track crop varieties, planting dates, growth stages, and growth-progress bars with pest-risk alerts. |
| **Yield Predictions** | AI-powered yield predictions (bu/acre) compared against current yields with percentage-change indicators. |
| **Inventory Management** | Four-category inventory (Seeds, Fertilizers, Equipment, Harvested Crops) with a recent-transactions table. |
| **Financial Overview** | Annual revenue, expenses, and predicted profit with an expense-breakdown chart (Seeds, Equipment, Labour, Fuel). |
| **Resource Consumption** | Usage tracking for Diesel Fuel, Water, and Electricity with an AI-generated optimisation suggestion. |
| **Product Shelf Life** | Tracks harvested produce expiry dates and raises alerts when stock is nearing end-of-shelf-life. |
| **Market Operations** | Buy/sell transaction log with selling, buying, and net revenue summaries. |
| **Task Scheduler** | Prioritised farm-task list (High / Medium / Low) with date and time scheduling and completion tracking. |

### 📲 WhatsApp Alerts (Twilio)
The backend exposes a `/notify-farmer` endpoint that sends WhatsApp messages via the Twilio Sandbox to a farmer's phone number. Three alert types are supported:
- `weather` — Rain forecast notification.
- `drought` — Prolonged dry-period warning.
- `fertilizer` — Fertiliser application reminder.

### 🌐 Internationalisation
The UI supports **English** and **Hindi** via `i18next` with automatic browser-language detection.

---

## Tech Stack

### Frontend
| Technology | Version | Purpose |
|---|---|---|
| [React](https://react.dev/) | 19 | UI library |
| [Vite](https://vitejs.dev/) | 6 | Dev server and build tool |
| [Tailwind CSS](https://tailwindcss.com/) | 4 | Utility-first CSS |
| [React Router](https://reactrouter.com/) | 7 | Client-side routing |
| [Lucide React](https://lucide.dev/) | 0.487 | Icon library |
| [i18next](https://www.i18next.com/) | 24 | Internationalisation |
| [Radix UI](https://www.radix-ui.com/) | latest | Accessible UI primitives |
| [class-variance-authority](https://cva.style/) | 0.7 | Component variant management |

### Backend
| Technology | Version | Purpose |
|---|---|---|
| [Node.js](https://nodejs.org/) | 18+ | Runtime |
| [Express](https://expressjs.com/) | 5 | HTTP server |
| [node-fetch](https://github.com/node-fetch/node-fetch) | 3 | Server-side HTTP requests |
| [Twilio](https://www.twilio.com/) | 5 | WhatsApp alert messaging |
| [dotenv](https://github.com/motdotla/dotenv) | 16 | Environment variable management |
| [cors](https://github.com/expressjs/cors) | 2 | Cross-origin resource sharing |

### External APIs
- **[OpenWeatherMap](https://openweathermap.org/api)** — Current weather and 5-day forecast data.
- **[Twilio WhatsApp Sandbox](https://www.twilio.com/docs/whatsapp/sandbox)** — WhatsApp message delivery.

---

## Project Structure

```
AITD/
├── Backend/
│   ├── package.json
│   └── src/
│       ├── server.js        # Express server, Weather API proxy, Twilio alerts
│       └── test.rest        # Manual API test file
└── Frontend/
    ├── index.html
    ├── vite.config.js
    ├── package.json
    └── src/
        ├── main.jsx         # React entry point
        ├── App.jsx          # Root layout (Navbar + Outlet + Footer)
        ├── i18.js           # i18next configuration
        ├── routers/
        │   └── router.jsx   # Application routes
        ├── pages/
        │   ├── Home.jsx         # Home dashboard
        │   ├── Weather.jsx      # Weather dashboard
        │   ├── FarmManagement.jsx  # /resources page
        │   ├── Detect.jsx       # Detect page (in development)
        │   ├── Manage.jsx       # Manage page (in development)
        │   └── Login.jsx        # Login page
        ├── components/
        │   ├── Navbar.jsx
        │   ├── Footer.jsx
        │   ├── WelcomeSection.jsx
        │   ├── TechnologySection.jsx
        │   ├── FeatureCards.jsx
        │   ├── SoilMonitoring.jsx
        │   ├── CommodityPrices.jsx
        │   ├── CropAlerts.jsx
        │   ├── FarmWeather.jsx
        │   ├── PestMonitor.jsx
        │   ├── AgricultureNews.jsx
        │   ├── FarmManagement.jsx
        │   ├── CardCarousel.jsx
        │   ├── GridSection.jsx
        │   ├── ScrollingText.jsx
        │   ├── Separator.jsx
        │   ├── TextSection.jsx
        │   ├── PageHeader.jsx
        │   └── farm-management/
        │       ├── CropManagement.jsx
        │       ├── YieldPredictions.jsx
        │       ├── InventoryManagement.jsx
        │       ├── FinancialOverview.jsx
        │       ├── ResourceConsumption.jsx
        │       ├── ProductShelfLife.jsx
        │       ├── MarketOperations.jsx
        │       └── TaskScheduler.jsx
        ├── locales/
        │   ├── en/translation.json   # English strings
        │   └── hn/translation.json   # Hindi strings
        └── lib/
            └── utils.js
```

---

## Getting Started

### Prerequisites

- **Node.js** ≥ 18 (includes npm)
- A free [OpenWeatherMap API key](https://home.openweathermap.org/users/sign_up)
- A [Twilio account](https://www.twilio.com/try-twilio) with WhatsApp Sandbox enabled (for alert notifications)

---

### Backend Setup

```bash
# 1. Navigate to the backend directory
cd AITD/Backend

# 2. Install dependencies
npm install

# 3. Create the environment file
cp .env.example .env   # or create .env manually (see Environment Variables below)

# 4. Start the development server (auto-restarts on file changes)
npm run dev
```

The backend server starts at **http://localhost:3000**.

---

### Frontend Setup

```bash
# 1. Navigate to the frontend directory
cd AITD/Frontend

# 2. Install dependencies
npm install

# 3. Start the Vite dev server
npm run dev
```

The frontend dev server starts at **http://localhost:5173**.

> **Note:** The frontend proxies weather data through the backend at `http://localhost:3000/api/weather`. Make sure the backend is running before using the Weather Dashboard.

#### Other Frontend Scripts

| Command | Description |
|---|---|
| `npm run dev` | Start development server |
| `npm run build` | Production build (outputs to `dist/`) |
| `npm run preview` | Preview the production build locally |
| `npm run lint` | Run ESLint |

---

## Environment Variables

Create a `.env` file inside the `Backend/` directory with the following keys:

```env
# OpenWeatherMap API key
WEATHER_API_KEY=your_openweathermap_api_key

# Twilio credentials (for WhatsApp alerts)
TWILIO_ACCOUNT_SID=your_twilio_account_sid
TWILIO_AUTH_TOKEN=your_twilio_auth_token
```

| Variable | Required | Description |
|---|---|---|
| `WEATHER_API_KEY` | ✅ Yes | API key from [openweathermap.org](https://openweathermap.org/api) |
| `TWILIO_ACCOUNT_SID` | ✅ Yes (for alerts) | Found in your Twilio Console Dashboard |
| `TWILIO_AUTH_TOKEN` | ✅ Yes (for alerts) | Found in your Twilio Console Dashboard |

---

## API Reference

All backend endpoints are served from `http://localhost:3000`.

### `GET /api/weather`

Fetches current weather conditions and a 5-day / 3-hour forecast from OpenWeatherMap.

**Query Parameters**

| Parameter | Type | Required | Description |
|---|---|---|---|
| `lat` | `number` | No | Latitude (defaults to Mapusa, Goa) |
| `lon` | `number` | No | Longitude (defaults to Mapusa, Goa) |

**Example Request**
```
GET /api/weather?lat=15.5957&lon=73.8091
```

**Example Response**
```json
{
  "current": { /* OpenWeatherMap current weather object */ },
  "forecast": { /* OpenWeatherMap forecast object with list[] */ }
}
```

---

### `POST /notify-farmer`

Sends a WhatsApp alert message to a farmer via the Twilio Sandbox.

**Request Body**

```json
{
  "phone": "+919876543210",
  "alertType": "weather"
}
```

| Field | Type | Required | Values |
|---|---|---|---|
| `phone` | `string` | ✅ Yes | Recipient phone number in E.164 format (e.g. `+919876543210`) |
| `alertType` | `string` | ✅ Yes | `"weather"`, `"drought"`, or `"fertilizer"` |

**Example Response**
```json
{
  "success": true,
  "sid": "SMxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
}
```

> **Twilio Sandbox Note:** The recipient must first opt-in to the Twilio WhatsApp Sandbox by sending `join <sandbox-keyword>` to `+1 415 523 8886` before they can receive messages.

---

## Pages & Routes

| Route | Page | Description |
|---|---|---|
| `/` | Home | Main dashboard with soil, weather, pest, commodity, and news widgets |
| `/Weather` | Weather Dashboard | Forecast carousel and detailed weather grid |
| `/resources` | Farm Management | Full farm-operations suite (crops, inventory, finance, tasks) |
| `/detect` | Detect | Disease/pest detection (in development) |
| `/manage` | Manage | Additional management tools (in development) |
| `/login` | Login | User authentication (in development) |

---

## Internationalisation

The frontend uses **i18next** with `react-i18next` and automatic browser-language detection.

- **English** translations: `Frontend/src/locales/en/translation.json`
- **Hindi** translations: `Frontend/src/locales/hn/translation.json`

The `fallbackLng` is set to `"en"`, so English strings are used when a translation key is missing in the detected language.

To add a new language:
1. Create a new folder under `Frontend/src/locales/<lang-code>/`.
2. Add a `translation.json` file with the required keys.
3. Import and register it in `Frontend/src/i18.js`.

---

## Contributing

1. Fork the repository and create a new branch: `git checkout -b feature/your-feature-name`
2. Make your changes and ensure the code lints cleanly: `npm run lint` (in `Frontend/`)
3. Commit your changes with a clear message.
4. Open a Pull Request against the `main` branch.
