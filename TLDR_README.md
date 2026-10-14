## TL;DR

**Macro Tracker** is a free, customizable iPhone application for tracking calories, macronutrients, and body weight.

Built using JavaScript and [Scriptable](https://scriptable.app/), it runs directly on your iPhone without subscriptions, external servers, or paid APIs.

### What Can It Do?

- **Track Food:** Log calories, protein, carbs, and fat.
- **Save Favorites:** Quickly log foods you eat frequently.
- **View History:** Review, edit, and delete previous meals.
- **Analyze Nutrition:** See weekly averages and daily breakdowns.
- **Track Weight:** Record weigh-ins and view your weight trends.
- **Get Notifications:** Receive a daily summary of your macros.
- **Home Screen Widget:** Check your progress without opening the app.
- **iCloud Storage:** Automatically save your data between sessions.

**Requirements:** An iPhone, the free Scriptable app, and iCloud Drive.

**Setup Time:** Approximately 5–10 minutes.

---

# Installation Guide (Beginner Friendly)

You do not need any programming experience to install Macro Tracker.

Just follow these steps.

## Step 1: Download Scriptable

Scriptable is a free iPhone application that allows you to run JavaScript programs.

1. Open the **App Store** on your iPhone.
2. Search for **Scriptable**.
3. Download and install the application.
4. Open Scriptable once to complete its initial setup.

Official website: https://scriptable.app/

**Important:** Make sure iCloud Drive is enabled on your iPhone.

You can check this under:

**Settings → Your Name → iCloud → Drive**

Enable **Sync this iPhone** if it is disabled.

---

## Step 2: Download the Macro Tracker Scripts

This repository contains two JavaScript files:

| File | Purpose |
|------|---------|
| `Macro Tracker - Add Food.js` | Main application for food logging, weight tracking, and analytics |
| `Macro Tracker - Dashboard.js` | Home Screen widget displaying daily macro progress |

You will install both scripts into Scriptable.

### Download the Files

1. Open this GitHub repository.
2. Navigate to the `scripts` folder.
3. Open `Macro Tracker - Add Food.js`.
4. Copy the entire JavaScript code.
5. Keep the GitHub page open for the next step.

You will repeat this process for the dashboard script.

---

## Step 3: Install the Main Application

1. Open **Scriptable** on your iPhone.
2. Tap the **+** button to create a new script.
3. Delete any existing placeholder code.
4. Paste the JavaScript code from `Macro Tracker - Add Food.js`.
5. Rename the script to:

   `Macro Tracker - Add Food`

6. Save the script.

### Test the Application

Tap the script to run it.

You should see the Macro Tracker interface with four tabs:

- **Log Food:** Add meals and manage saved foods.
- **History:** View previous meals.
- **Analytics:** Review weekly nutrition statistics.
- **Weight:** Record and monitor body weight.

**Congratulations! The main application is installed.**

---

## Step 4: Configure Your Daily Macro Goals

Macro Tracker allows you to customize your daily nutritional targets.

Open the `Macro Tracker - Add Food` script in Scriptable.

Near the beginning of the code, locate:

```javascript
const GOALS = {
  calories: 2400,
  protein: 200,
  carbs: 250,
  fat: 65
};
```

Change these numbers to your desired daily goals.

For example, if you want to consume 2,000 calories, 180g of protein, 200g of carbohydrates, and 60g of fat:

```javascript
const GOALS = {
  calories: 2000,
  protein: 180,
  carbs: 200,
  fat: 60
};
```

Save your changes.

**Important:** If you use the Home Screen widget, update the goals in the dashboard script as well so both displays match.

---

## Step 5: Install the Home Screen Widget

The dashboard widget displays your daily nutrition progress directly on your iPhone Home Screen.

### Create the Dashboard Script

1. Return to this GitHub repository.
2. Open `Macro Tracker - Dashboard.js`.
3. Copy the entire JavaScript code.
4. Open Scriptable.
5. Create another script using the **+** button.
6. Paste the dashboard code.
7. Name the script:

   `Macro Tracker - Dashboard`

8. Save it.

### Add the Widget to Your Home Screen

1. Go to your iPhone Home Screen.
2. Press and hold an empty area until the icons begin moving.
3. Tap **Edit → Add Widget**.
4. Search for **Scriptable**.
5. Select the **Medium** widget size.
6. Tap **Add Widget**.
7. Tap **Done**.

### Connect the Widget to Your Script

1. Press and hold the new Scriptable widget.
2. Select **Edit Widget**.
3. Tap the **Script** option.
4. Select `Macro Tracker - Dashboard`.
5. Close the widget settings.

Your widget should now display your daily macro information.

**Note:** iOS controls how frequently widgets refresh. Your dashboard may not update immediately after logging food.

---

## Step 6: Enable Daily Notifications

Macro Tracker can send a daily summary showing your calorie and macronutrient totals.

The default notification time is **8:00 PM**.

### Enable Notification Permissions

1. Open your iPhone's **Settings**.
2. Navigate to **Notifications**.
3. Find **Scriptable**.
4. Enable **Allow Notifications**.

### Change the Notification Time (Optional)

Open `Macro Tracker - Add Food` in Scriptable.

Find:

```javascript
const NOTIFICATION_HOUR = 20;
const NOTIFICATION_MINUTE = 0;
```

The application uses 24-hour time.

| Desired Time | Hour | Minute |
|--------------|------|--------|
| 6:00 PM | 18 | 0 |
| 7:00 PM | 19 | 0 |
| 8:00 PM | 20 | 0 |
| 9:00 PM | 21 | 0 |
| 10:30 PM | 22 | 30 |

For example, to receive notifications at 9:30 PM:

```javascript
const NOTIFICATION_HOUR = 21;
const NOTIFICATION_MINUTE = 30;
```

Save your changes.

### How Notifications Work

When you log food and save your changes, Macro Tracker schedules a notification containing your current daily totals.

If you log additional food before the notification time, the pending notification is updated the next time you save.

**You do not need to open Scriptable when the notification arrives.**

However, notifications reflect your most recently saved data. They are not automatically recalculated in the background.

---

## Step 7: Start Tracking Your Food

Now that everything is configured, you can begin logging meals.

### Add Your First Meal

1. Open Scriptable.
2. Run `Macro Tracker - Add Food`.
3. Select the **Log Food** tab.
4. Enter a food name.
5. Enter its calories, protein, carbohydrates, and fat.
6. Tap **Add Food**.
7. Tap **Done** at the top of the screen to save.

Your food will now appear in your daily totals.

### Save Frequently Eaten Foods

If you regularly eat the same meals:

1. Enter the food's nutritional information.
2. Tap **Save as Favorite**.
3. Tap **Done** to save your changes.

The next time you open Macro Tracker, you can use **Quick Add** to log that food immediately.

---

## Step 8: Track Your Body Weight

Macro Tracker also includes a built-in weight tracking system.

1. Open the main application.
2. Select the **Weight** tab.
3. Choose the date.
4. Enter your weight in pounds.
5. Tap **Save Weight**.
6. Tap **Done** to save your changes.

The application automatically calculates:

- Latest recorded weight
- Seven-day average weight
- Starting weight
- Total weight change
- Thirty-day weight trend

You can also edit or delete previous weigh-ins.

**Tip:** For more consistent results, weigh yourself at approximately the same time each morning.

---

## Step 9: Understand Where Your Data Is Stored

Macro Tracker automatically creates a folder in iCloud Drive.

Your data is stored here:

```text
iCloud Drive
└── Scriptable
    └── MacroTracker
        ├── food_log.json
        ├── saved_foods.json
        └── weight_log.json
```

Each file has a specific purpose:

| File | Stored Information |
|------|-------------------|
| `food_log.json` | All logged meals and nutritional information |
| `saved_foods.json` | Your favorite and frequently eaten foods |
| `weight_log.json` | Your recorded body weight measurements |

These files are automatically created as needed.

You do not need to manually create or edit them.

### Important

**Do not delete these files unless you want to remove your tracking history.**

Consider periodically backing up the `MacroTracker` folder.

---

# Troubleshooting

### The App Doesn't Open

Make sure you copied the entire JavaScript file into Scriptable.

Check that no lines were accidentally deleted or modified.

### My Food Isn't Saving

After adding food, you must tap **Done** at the top of the application window.

This closes the interface and allows Scriptable to save your changes.

### My Widget Isn't Updating

First, verify that your dashboard script is configured to use the same storage folder as the main application.

The correct folder name is:

`MacroTracker`

Also remember that iOS determines when widgets refresh.

### I'm Not Receiving Notifications

Check the following:

1. Scriptable notifications are enabled in iOS Settings.
2. You logged food before the scheduled notification time.
3. You tapped Done to save your changes.
4. Your device's Focus settings are not silencing Scriptable notifications.

### My Weight History Disappeared

Check whether the following file exists:

`iCloud Drive/Scriptable/MacroTracker/weight_log.json`

If the file was deleted, you will need to restore it from a backup.

---

# You're All Set!

You now have a fully functional nutrition and weight tracking application running directly on your iPhone.

No subscription, external server, or paid nutrition tracking service is required.

## License

This project is licensed under the MIT License.

Copyright (c) 2026 Troy Volpe.