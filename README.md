# FitForm — Native Android Fitness & Pose Detection

A Kotlin + Jetpack Compose Android project with a dark premium UI and lime accent. It includes:

- CameraX camera preview and on-device Google ML Kit Pose Detection (STREAM_MODE).
- Pose landmark points drawn over the camera view.
- Exercise selector with pose tracking for general body poses and heuristic rep counting patterns for common movements: squats, lunges, push-ups, curls, rows, overhead/shoulder presses, lateral/front raises, jumping jacks, sit-ups/crunches, glute bridges, good mornings, bodyweight deadlifts, triceps extensions, and high knees.
- BMI calculator and estimated daily maintenance calories (Mifflin-St Jeor-style equation with activity multipliers).
- Workout library with video-search links and shortcuts to supported AI exercises.
- Local progress charts and workout history persisted in a Room database (`fitform.db`).

## Requirements

- Android Studio Ladybug or newer (or a compatible recent Android Studio)
- JDK 17
- Android SDK 35 installed
- A physical Android phone is recommended for camera testing. An emulator may work if it has a camera source.
- Internet access for Gradle dependency downloads and for opening the workout video links.

## Run it

1. Unzip `FitFormAndroid.zip`.
2. In Android Studio choose **Open** and select the `FitFormAndroid` folder (the one containing `settings.gradle.kts`).
3. Allow Gradle sync to download dependencies. If prompted, install Android SDK 35 and use JDK 17.
4. Connect an Android phone with USB debugging enabled, or start an emulator.
5. Press **Run ▶** for the `app` configuration.
6. Grant camera permission when prompted. Open **Train**, choose Squat or Push-up, tap **Start tracking**, and keep the relevant joints visible in a well-lit frame.
7. Choose a movement from the horizontal exercise selector. Tap **Save session to progress** to store the session in the local Room database. Open **Progress** to see saved sessions and the rep chart.

## Build an APK

From Android Studio: **Build → Build Bundle(s) / APK(s) → Build APK(s)**.

Or from the project folder with a JDK 17 and Android SDK configured:

```bash
./gradlew assembleDebug
```

On Windows:

```bat
gradlew.bat assembleDebug
```

The debug APK is normally written to `app/build/outputs/apk/debug/app-debug.apk`.

## Important implementation notes

- Pose inference runs on-device. The app does not upload camera frames.
- ML Kit detects body landmarks generally, but accurate rep counting for literally every possible exercise is not achievable with one generic algorithm. This project includes configurable angle/phase heuristics for several common movement families, not a trained classifier for every exercise. Some movements (including glute bridges, deadlifts, raises, or movements where equipment hides joints) may count poorly with the current 2D-angle proxies. Static holds such as planks should be timed rather than counted as reps. Camera angle, body visibility, lighting, clothing, and individual movement style affect accuracy. Treat the counter as a prototype and test/tune each exercise on real devices; it is not a certified form checker.
- The displayed calorie numbers are rough estimates derived from reps and are not measured energy expenditure. The calorie calculator is a general estimate and not medical advice. BMI is a screening metric, not a diagnosis.
- The workout library opens YouTube search results rather than embedding copyrighted videos.
- This starter project uses Room local storage, not Firebase/Firestore; progress remains on the device and does not sync across devices.
- No build was run in this environment. Android Studio/Gradle must resolve dependencies and compile the project; fix any SDK or dependency resolution errors shown by your local setup before installation.
