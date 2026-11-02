# SkyWatch — Real-Time Weather App

A cross-platform Android/iOS weather app built with **React Native, Expo and TypeScript** for the Code A Nova Internship Project (2026).

## Features

- Current weather by device GPS location.
- Search cities worldwide with location suggestions.
- Current temperature, feels-like temperature, condition, humidity, wind, pressure, visibility, sunrise and sunset.
- Five-day forecast and available 3-hour forecast intervals.
- Save and remove favourite cities.
- Dark and light themes.
- Local persistence with AsyncStorage. The last successful weather response remains available when a refresh fails or the device is offline.
- Loading, missing-key, invalid-city, network and location-permission error states.
- Pull-to-refresh and bottom-tab navigation.

## Tech stack

| Area | Technology |
|---|---|
| Framework | React Native + Expo (TypeScript) |
| Weather data | OpenWeatherMap Current Weather + 5 Day / 3 Hour Forecast + Geocoding APIs |
| Location | expo-location |
| HTTP | Axios |
| State | Zustand |
| Local persistence | AsyncStorage |
| Icons | Expo Vector Icons |

## Requirements

- Node.js LTS
- npm
- Expo Go on an Android phone, or Android Studio emulator
- A free OpenWeatherMap API key: https://openweathermap.org/api

## Setup

1. Download or clone this repository.
2. Open a terminal in the project folder.
3. Install dependencies:

   ```bash
   npm install
   ```

4. Create a file named `.env` in the project root. Copy the contents of `.env.example` and replace the placeholder with your own OpenWeatherMap API key:

   ```env
   EXPO_PUBLIC_OPENWEATHER_API_KEY=your_real_api_key
   ```

   Do not commit your real API key to a public GitHub repository. `.env` is ignored by Git.

5. Start the app:

   ```bash
   npx expo start
   ```

6. Scan the QR code using Expo Go, or press `a` to launch an Android emulator.

> OpenWeatherMap may take a little time to activate a newly created API key. If the app reports an API error immediately after creating a key, wait for activation and try again.

## Android APK build

The repository is configured for Expo. To create an installable APK using Expo Application Services (EAS):

1. Install EAS CLI and sign in:

   ```bash
   npm install -g eas-cli
   eas login
   ```

2. Configure the project:

   ```bash
   eas build:configure
   ```

3. Add an APK build profile to `eas.json` (or use the included profile):

   ```json
   {
     "build": {
       "preview": {
         "distribution": "internal",
         "android": { "buildType": "apk" }
       }
     }
   }
   ```

4. Build:

   ```bash
   eas build -p android --profile preview
   ```

EAS build requires an Expo account and internet access. The APK is produced by EAS; it is not included in this source ZIP.

## Project structure

```text
skywatch-github/
├── App.tsx                    # Main screens, navigation and UI
├── app.json                   # Expo and native permissions config
├── package.json
├── tsconfig.json
├── .env.example               # API-key template (no secret included)
├── src/
│   ├── services/weather.ts    # OpenWeatherMap API and data mapping
│   ├── store/useWeatherStore.ts # Zustand state + AsyncStorage persistence
│   └── utils/theme.ts         # Dark/light theme tokens
└── README.md
```

## Test checklist

| Test | Expected result |
|---|---|
| Launch with location permission granted | Current location weather loads |
| Launch with location permission denied | App stays usable and suggests city search |
| Search for a valid city | City suggestions appear and selected weather loads |
| Search for an invalid city | Helpful error appears; app does not crash |
| Save a city | City appears in Saved places |
| Remove a saved city | City disappears from Saved places |
| Open Forecast | Five forecast days and hourly intervals appear |
| Toggle theme | App switches between dark and light appearance |
| Pull to refresh | Current weather is requested again |
| Disable network after a successful fetch | Last saved weather remains visible; refresh error is shown |
| Start without an API key | Setup guidance is displayed instead of a crash |

## API usage

The app uses OpenWeatherMap endpoints:

- Current weather: `/data/2.5/weather`
- Five-day forecast: `/data/2.5/forecast`
- City geocoding: `/geo/1.0/direct`

All requests use metric units. Keep API usage within the limits of your OpenWeatherMap plan.

## Notes

- Android is the primary required platform; iOS is supported by the Expo project configuration.
- UV index is not displayed because the selected free-tier current-weather and forecast endpoints do not reliably provide it. The core requested weather metrics are included.
- Weather condition icons are loaded from OpenWeatherMap's icon service.
- This repository contains source code and setup instructions. Device testing, screen recordings, and the final APK must be completed after adding a personal API key and running/building the app.

## Credits

Built for **Code A Nova — Internship Program 2026**. Weather data by [OpenWeatherMap](https://openweathermap.org/).
