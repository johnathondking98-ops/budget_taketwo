# budget-v4-1 · Family Finance App

A React Native / Expo app for tracking bi-weekly pay, bills, groceries, and fuel — with real-time cloud sync via Firebase.

---

## Prerequisites

Install these **once** on your Chromebook Linux environment before doing anything else.

### 1 · Node.js (v18 or newer)

```bash
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt-get install -y nodejs
node -v   # should print v18.x.x or higher
```

### 2 · Expo CLI

```bash
npm install -g expo-cli
```

### 3 · Expo Go on your Android phone

Install **Expo Go** from the Google Play Store on the phone you want to preview on.  
Make sure your phone and your Chromebook are on the **same Wi-Fi network**.

---

## Running the app (every time)

```bash
# 1. Navigate to the project folder
#    (Linux files > android > budget-v4-1 is the default location)
cd ~/android/budget-v4-1

# 2. Install dependencies (first run only, or after any package.json change)
npm install

# 3. Start the Expo development server
npx expo start
```

The terminal will display a **QR code**.  
Open **Expo Go** on your Android phone and tap **"Scan QR code"** to load the app.

> **Tip:** If the QR code doesn't scan, press `a` in the terminal to open directly on a connected Android device, or `w` to open in a web browser for a quick sanity check.

---

## Project structure

```
budget-v4-1/
├── App.js                  Main entry — state, Firebase sync, layout
├── firebase.js             Firebase init & realtime DB export
├── index.js                Expo root component registration
├── app.json                Expo config (slug: budget-v4)
├── package.json            Dependencies (Firebase ^10, Expo ~54)
│
├── Pages/
│   ├── DashboardPage.js    Pay period overview
│   ├── CalendarPage.js     Shift & bill calendar
│   ├── GroceryPage.js      Grocery tracker with tax
│   └── SettingsPage.js     Pay rates, tax, cycle dates
│
├── components/             Modals (shift log, calendar entry, fuel, archive, report…)
├── hooks/                  usePayroll, useGroceries, useCalendar, useStorage
├── styles/GlobalStyles.js  Shared style tokens
└── constants/Colors.js     Theme color palette
```

---

## Cloud sync

All data is stored in **Firebase Realtime Database** under the path `family_vault`.  
No data is saved to the device — every change syncs in real time across all phones on the same account.

To initialize a fresh cloud vault (wipe & reload from current device state):  
Open the app → **Settings** → tap **INITIALIZE FAMILY CLOUD**.

---

## Troubleshooting

| Problem | Fix |
|---|---|
| `Cannot find module 'firebase/compat/app'` | Run `npm install` — the `node_modules` folder is missing |
| QR code shows but app won't load | Phone and Chromebook must be on the **same Wi-Fi network** |
| `Metro bundler` error on start | Delete `.expo/` folder and re-run `npx expo start` |
| App loads but shows no data | Tap **INITIALIZE FAMILY CLOUD** in Settings to push data to Firebase for the first time |
| Camera / barcode scanner doesn't work | Grant camera permission when Expo Go asks, or go to Android Settings → Apps → Expo Go → Permissions |