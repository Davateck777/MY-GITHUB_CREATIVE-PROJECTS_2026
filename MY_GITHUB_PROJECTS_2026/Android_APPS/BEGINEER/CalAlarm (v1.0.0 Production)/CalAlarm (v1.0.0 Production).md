
> [!important]
> Add the following Features 
> 
> 1. A General Setting for the App
> 2. Alarm ringtone selector
> 3. Minimalist + Organized in-app Layout 
> 
> Note : REMOVE MVP TRAINING WHEELS AND SHIP TO VER 1.0 PRODUCTION 
> 
> Add the following functions:
> 
> 
> 4. Alarm_Ringtone_Duration
> 5. Ability to Display over screen



> **Minimalist Calendar Time Alarm for Android**

  

CalAlarm is a minimalist, event-specific calendar alarm application for Android built with Kotlin and Jetpack Compose. Unlike traditional daily repeating alarm clocks, CalAlarm anchors alerts directly to calendar dates, meetings, appointments, deadlines, and flights with customizable reminder offsets, exact system alarm scheduling, ringtone audio selection, and display-over-screen capabilities.

  

---

  

## 📱 Key Features

  

### 1. Calendar-Anchored Exact Alarms

* **Context-Aware Event Alarms**: Schedule alerts tied to specific dates and times rather than daily repetitive alarm schedules.

* **Reminder Offsets**: Choose when you want the alarm to ring:

  * *At time of event* (0m)

  * *5 minutes before*

  * *10 minutes before*

  * *15 minutes before*

  * *30 minutes before*

  * *1 hour before*

  * *2 hours before*

  * *1 day before*

* **Real-time Live Countdowns**: Displays live remaining time (e.g. `In 2h 45m`, `Tomorrow`, `Completed`).

* **Hardware AlarmClock Integration**: Uses Android's `AlarmManager.setAlarmClock(...)` to wake the device from Doze mode and show the system alarm clock icon on lock screens.

  

### 2. Alarm Ringtone Selector & Duration (`Alarm_Ringtone_Duration`)

* **Audio Tone Selector**: Choose between system alarm ringtones, notification chimes, and standard phone ringers. Includes live **Play / Pause preview** before applying.

* **Per-Alarm & Global Default**: Assign a distinct tone to a specific event or configure a global default in Settings.

* **Auto-Silence Duration Timeout**: Automatically silences ringing and vibration after a customizable interval (*1 min, 2 mins, 5 mins, 10 mins, or Continuous*) to prevent battery drain. Displays a live countdown (`Auto-silencing in mm:ss`) during active alarms.

* **Custom Vibration Patterns**: Choose between *Standard*, *Gentle*, and *Urgent* haptic feedback patterns.

  

### 3. Display Over Screen (`SYSTEM_ALERT_WINDOW`)

* **Screen Takeover (`AlarmRingActivity`)**: Pops up full-screen alerts directly over running apps, games, or videos when the alarm fires.

* **Lock Screen Bypass**: Uses `showWhenLocked`, `turnScreenOn`, and `USE_FULL_SCREEN_INTENT` to turn on the screen and show alarms without requiring device unlocking first.

* **Permission Management**: Built-in 1-click status checker and direct link to Android's "Display over other apps" system settings screen.

  

### 4. Minimalist & Organized 3-Tab Layout

* **Alarms**: Chronological timeline, live countdown badges, search bar, 14-day date scrubber strip, category filter pills (*Meeting, Deadline, Flight, Task, Personal, Reminder*), and hero card for next upcoming alarm.

* **Calendar**: Interactive monthly agenda view displaying day matrix, alarm count indicators, and selected day agenda cards.

* **Settings**: General settings hub for ringtone selection, auto-silence duration, overlay permissions, snooze defaults, and theme management.

  

### 5. Single-Stream Audio Engine & Notification Sync

* **Isolated Audio Authority**: All ringtone playback and looping is strictly handled by `AlarmRingtonePlayer` with synchronized lifecycle management (`MediaPlayer` primary with `Ringtone` fallback).

* **Silent High-Priority Channel**: The Android notification channel is configured with `setSound(null, null)` and `enableVibration(false)` to prevent duplicate concurrent audio playback between the notification manager and alarm engine.

* **Accurate Ringtone Resolution**: Queries device ringtone titles cleanly through `Ringtone.getTitle()` to prevent numeric index fallbacks.

  

### 6. Production Reliability & Offline Storage

* **Local Room Database (SQLite)**: 100% offline-first, private on-device data persistence using Room and KSP.

* **Reboot Resilience (`BootReceiver`)**: Automatically reschedules all active upcoming alarms when the device reboots.

  

---

  

## 🛠️ Architecture & Tech Stack

  

* **Language**: Kotlin 2.0+

* **UI Framework**: Jetpack Compose (Material Design 3)

* **Architecture**: Clean MVVM (Model-View-ViewModel) + Repository Pattern

* **Local Persistence**: AndroidX Room + KSP (Kotlin Symbol Processing)

* **Asynchronous Concurrency**: Kotlin Coroutines & Reactive `StateFlow`

* **System Services**:

  * `AlarmManager` (Exact AlarmClock API)

  * `NotificationManager` (High-priority heads-up notifications with action buttons)

  * `RingtoneManager` & `MediaPlayer` (Audio playback)

  * `Vibrator` & `VibratorManager` (Haptic waveform patterns)

  * `WindowManager` (Lock screen and overlay flags)

  

---

  

## 📋 Required Permissions

  

The app declares least-privilege permissions in `AndroidManifest.xml`:

* `android.permission.POST_NOTIFICATIONS`: For Android 13+ heads-up alerts.

* `android.permission.SCHEDULE_EXACT_ALARM` & `USE_EXACT_ALARM`: For exact alarm triggers.

* `android.permission.SYSTEM_ALERT_WINDOW`: For display over other applications.

* `android.permission.USE_FULL_SCREEN_INTENT`: For lock-screen alarm takeover.

* `android.permission.WAKE_LOCK`: To wake CPU during alarm ringing.

* `android.permission.VIBRATE`: For haptic vibration patterns.

* `android.permission.RECEIVE_BOOT_COMPLETED`: To reschedule pending alarms on system reboot.

  

---

  

## 🚀 Building & Testing

  

### Assemble Debug APK

```bash

gradle assembleDebug

```

  

### Run Unit Tests

```bash

gradle :app:testDebugUnitTest

```

  

---

  

## 📄 License

Released under the MIT License. Copyright © 2026 CalAlarm.