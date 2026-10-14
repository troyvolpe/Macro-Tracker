# Macro Tracker

A lightweight, customizable nutrition and body weight tracking application built entirely with JavaScript using Scriptable for iOS.

Macro Tracker provides a simple way to monitor daily macronutrient intake, log meals, track body weight, analyze nutritional trends, and receive automated daily notifications.

The application runs locally on an iPhone and stores data in iCloud Drive without requiring a subscription, external database, or dedicated backend server.

## Features

### Food Logging
- Log meals with calories, protein, carbohydrates, and fat.
- Automatically calculate daily macronutrient totals.
- View progress toward customizable daily nutrition goals.
- Edit or delete previously logged meals.
- Preserve historical food entries across sessions.

### Saved Foods
- Save frequently consumed foods for future use.
- Quickly add saved foods without reentering nutritional information.
- Automatically populate the food entry form using saved foods.
- Update or remove saved foods.

### Food History
- Browse food entries by date.
- View historical daily macronutrient totals.
- Edit or delete historical entries.
- Maintain a persistent food log using JSON storage.

### Weekly Analytics
- Calculate seven-day averages for:
  - Calories
  - Protein
  - Carbohydrates
  - Fat
- Track how frequently daily protein goals are achieved.
- Monitor the number of days with recorded food entries.
- View a daily breakdown of calorie and protein consumption.

### Body Weight Tracking
- Record body weight in pounds.
- Associate weigh-ins with specific dates.
- Edit or delete previous weight entries.
- Display the most recently recorded weight.
- Calculate average weight over the previous seven days.
- Monitor total weight change from the first recorded weigh-in.
- Visualize weight fluctuations using a 30-day line graph.

### Automated Daily Notifications
- Schedule a daily macronutrient summary notification.
- Display consumed calories, protein, carbohydrates, and fat.
- Calculate remaining macronutrients relative to daily goals.
- Automatically update the pending notification when tracker changes are saved.
- Deliver notifications without opening the application at the scheduled time.

Notifications are scheduled locally through iOS.

**Note:** Notification content reflects the most recently saved food data. A notification is scheduled only when the tracker is saved before the configured notification time and food has been logged for that day.

### Home Screen Widget
A separate Scriptable widget provides quick access to daily macronutrient information directly from the iPhone Home Screen.

The widget reads the same food history used by the main application.

Widget refresh timing is managed by iOS.

---

## Technology Stack

| Technology | Purpose |
|------------|---------|
| JavaScript | Application logic |
| HTML5 | User interface |
| CSS3 | Interface styling |
| Scriptable | iOS JavaScript runtime |
| WebView | Interactive application interface |
| iCloud Drive | Persistent data storage |
| JSON | Food, favorites, and weight records |
| iOS Notifications | Scheduled daily macro summaries |
| SVG | Body weight visualization |

The application does not require a traditional web server, database server, or external API.

---

## Application Architecture

Macro Tracker uses a lightweight architecture consisting of a Scriptable application, an embedded WebView interface, and persistent JSON files.

```text
iPhone
│
├── Scriptable
│   │
│   ├── Macro Tracker - Add Food
│   │   │
│   │   ├── Food Logging
│   │   ├── Saved Foods
│   │   ├── Food History
│   │   ├── Weekly Analytics
│   │   ├── Weight Tracking
│   │   └── Notification Scheduling
│   │
│   └── Macro Tracker - Dashboard
│       │
│       └── Home Screen Widget
│
└── iCloud Drive
    │
    └── Scriptable
        │
        └── MacroTracker
            │
            ├── food_log.json
            ├── saved_foods.json
            └── weight_log.json
```

### Data Flow

1. The user launches the food tracking script.
2. Scriptable loads existing JSON data from iCloud Drive.
3. An embedded WebView renders the application interface.
4. The user logs food, manages saved foods, or records body weight.
5. JavaScript updates the application's in-memory data.
6. When the WebView is closed using Done, Scriptable retrieves pending changes.
7. Updated data is written to the corresponding JSON files.
8. Scriptable updates the scheduled daily macro notification.
9. The Home Screen widget reads food history independently.

This architecture separates the user interface from persistent storage while keeping the application entirely within the iOS ecosystem.

---

## Installation

### Requirements

- iPhone running a compatible version of iOS
- Scriptable for iOS
- iCloud Drive enabled
- Notification permissions for Scriptable
- Optional: Home Screen widget support

### Step 1: Install Scriptable

Install Scriptable from the Apple App Store.

Scriptable allows JavaScript applications to interact with supported iOS functionality, including file storage, notifications, and Home Screen widgets.

### Step 2: Create the Main Script

1. Open Scriptable.
2. Create a new script.
3. Name it `Macro Tracker - Add Food`.
4. Copy the main application JavaScript into the script.
5. Save the script.

### Step 3: Configure Nutrition Goals

Daily nutrition goals are defined near the beginning of the main script.

```javascript
const GOALS = {
  calories: 2400,
  protein: 200,
  carbs: 250,
  fat: 65
};
```

Modify these values to match your nutritional targets.

### Step 4: Configure Notifications

The notification time is configurable.

```javascript
const NOTIFICATION_HOUR = 20;
const NOTIFICATION_MINUTE = 0;

const NOTIFICATION_ID = "macro-summary";
```

The default configuration schedules notifications for 8:00 PM.

Notification permissions must be enabled for Scriptable in iOS Settings.

### Step 5: Run the Application

1. Open `Macro Tracker - Add Food`.
2. Run the script.
3. The application interface will open.
4. Begin logging meals or recording body weight.
5. Tap Done to save changes.

The application automatically creates its storage directory if it does not already exist.

### Step 6: Configure the Home Screen Widget

1. Create a separate Scriptable script for the dashboard.
2. Add the dashboard JavaScript.
3. Long-press the iPhone Home Screen.
4. Add a Scriptable widget.
5. Select the desired widget size.
6. Configure the widget to run the dashboard script.

The dashboard script must reference the same iCloud storage directory as the main application.

---

## Data Storage

Application data is stored in the following directory:

```text
iCloud Drive/
└── Scriptable/
    └── MacroTracker/
        ├── food_log.json
        ├── saved_foods.json
        └── weight_log.json
```

### Food Entries

Food entries are stored in `food_log.json`.

Example:

```json
[
  {
    "food": "Chicken and Rice",
    "calories": 650,
    "protein": 55,
    "carbs": 75,
    "fat": 12,
    "timestamp": "2026-10-14T17:30:00.000Z"
  }
]
```

### Saved Foods

Frequently consumed foods are stored in `saved_foods.json`.

Example:

```json
[
  {
    "food": "Protein Shake",
    "calories": 160,
    "protein": 30,
    "carbs": 5,
    "fat": 2
  }
]
```

### Weight Entries

Body weight measurements are stored in `weight_log.json`.

Example:

```json
[
  {
    "date": "2026-10-14",
    "weight": 185.5
  },
  {
    "date": "2026-10-15",
    "weight": 185.2
  }
]
```

Weight entries are associated with calendar dates rather than timestamps.

The application prevents duplicate weight entries for the same date through its interface.

---

## User Interface

The application contains four main tabs.

| Tab | Functionality |
|-----|---------------|
| Log Food | Add meals, manage favorites, view daily progress |
| History | Browse, edit, and delete previous food entries |
| Analytics | View seven-day nutrition averages and daily breakdowns |
| Weight | Log weigh-ins, review weight history, and visualize trends |

The interface uses a dark theme with green accents and is designed for mobile devices.

---

## Notifications

The application uses Scriptable's native notification functionality.

When food data is saved before the configured notification time:

1. The application removes the previously pending macro summary notification.
2. It calculates the current day's nutritional totals.
3. It generates a notification containing consumed and remaining macronutrients.
4. It schedules the updated notification for the configured time.

Example notification:

```text
Daily Macro Summary

Calories: 2100 / 2400
Protein: 175 / 200g
Carbs: 220 / 250g
Fat: 55 / 65g

Remaining:
Calories: 300 left
Protein: 25g left
Carbs: 30g left
Fat: 10g left
```

Because the notification is scheduled in advance, iOS can deliver it without launching Scriptable at the notification time.

### Notification Limitations

- Notifications are not generated automatically on days when the tracker is never saved.
- Changes made after the scheduled notification time are not included in that day's summary.
- Notification content reflects the most recent successful save.
- Notification delivery depends on iOS notification permissions and device settings.

---

## Weight Analytics

The weight tracking component calculates several useful metrics.

### Latest Weight

Displays the most recent recorded weight based on the measurement date.

### Seven-Day Average

Calculates the average of all recorded weigh-ins within the previous seven calendar days.

Days without measurements are excluded from the calculation.

### Total Weight Change

Calculates the difference between the earliest and latest recorded weights.

```text
Total Change = Latest Weight - Starting Weight
```

### 30-Day Trend

Displays recorded weights from the previous 30 calendar days using an SVG line graph.

The graph automatically adjusts its vertical scale based on the recorded measurements.

Missing days are not interpreted as zero-weight measurements.

---

## Privacy and Security

Macro Tracker is designed to operate without external application servers.

- Food and weight records are stored in the user's iCloud Drive.
- No third-party analytics service is integrated.
- No external database is required.
- No application account or subscription is necessary.
- No external API requests are required for core functionality.

Data security depends on the security of the user's device, Apple account, and iCloud configuration.

Users should avoid committing personal food logs or weight records to public repositories.

---

## Limitations

The current version has several limitations:

- Food information must be entered manually.
- No barcode scanning or nutrition database integration.
- No automatic Apple Health synchronization.
- Weight measurements are recorded in pounds.
- Nutrition goals are configured directly in JavaScript.
- The application requires Scriptable on iOS.
- Data is saved when the WebView is closed using Done.
- Scheduled notifications are based on the most recently saved data.

---

## Future Improvements

Potential future enhancements include:

- Apple Health integration for body weight measurements.
- Barcode scanning and nutritional database lookup.
- Configurable goals directly within the application.
- Weekly and monthly weight averages.
- Calorie intake versus weight change analysis.
- CSV export for nutrition and weight history.
- Additional Home Screen widgets.
- Improved visualization of long-term nutrition trends.
- Meal templates and reusable meal combinations.
- Weight goal tracking and progress projections.

---

## Project Motivation

Macro Tracker was developed as a personal project to create a simple, customizable alternative to subscription-based nutrition tracking applications.

The project demonstrates how JavaScript, Scriptable, iCloud storage, and native iOS functionality can be combined to build a practical mobile application without a traditional backend.

It also provides hands-on experience with:

- JavaScript application development
- HTML and CSS interface design
- JSON-based data persistence
- Asynchronous file operations
- iOS automation and notifications
- Data aggregation and visualization
- Mobile application architecture

---

## Disclaimer

Macro Tracker is a personal nutrition and weight tracking tool.

It is not intended to provide medical advice, diagnose health conditions, or replace guidance from qualified healthcare professionals.

---

## License

MIT License

Copyright (c) 2026 Troy Volpe

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

---

## Author

**Troy Volpe**

Personal iOS development project built using JavaScript and Scriptable.