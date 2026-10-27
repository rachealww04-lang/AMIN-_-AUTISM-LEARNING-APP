# ANIM — Android Studio project aligned to the project report

This Kotlin + Jetpack Compose prototype follows the core user-facing modules described in `amin_folder_corrected.docx`: child profile setup, an uncluttered home dashboard, skill-area activities, picture-led instructions, text-to-speech, AAC-style communication board, visual schedule, positive reinforcement, progress summary, and sensory/audio preferences. It also includes a separate static caregiver/teacher dashboard mock-up in `web-dashboard/index.html`.

## Open the Android app
1. Extract the ZIP.
2. Open Android Studio and choose **Open**.
3. Select the `ANIM_Android_Studio` folder (the folder containing `settings.gradle.kts`).
4. Use JDK 17 and install Android SDK Platform 35 if prompted.
5. Allow Gradle to sync, then run the `app` configuration on an emulator or Android device.

## Included in this prototype
- Kotlin, Android Studio, Jetpack Compose and Material 3 UI.
- Child nickname/profile saved locally.
- Communication, social skills, early learning and daily living practice activities.
- Picture choices, spoken prompts using Android Text-to-Speech, immediate feedback and star rewards.
- AAC-style board that speaks common phrases.
- Visual activity schedule.
- Progress counts saved locally on the device using Android SharedPreferences.
- Audio and gentle-visual preferences.
- Static web dashboard mock-up with sample progress data.

## Important implementation limits
This is a working prototype, not the full production system described in the report. To match all of Chapter Six, the next engineering steps are to replace the lightweight local preferences with a Room/SQLite database, integrate Lottie lesson assets, implement Firebase Authentication/Cloud Firestore/Cloud Storage with security rules and parental consent, implement role-based access, and connect a real web dashboard to cloud data. The dashboard in this ZIP is a visual mock-up only and does not read data from the Android app. The language setting is saved, but complete Kiswahili translations and verified Kiswahili TTS are not included. The Android Text-to-Speech voice depends on the device.

No Firebase credentials or child data are included. Do not enter sensitive identifying information into the prototype. Obtain guardian consent before any real child data is collected. No flashing visuals or sudden loud sounds are used in the sample screens.


## Additional implementation foundations
- Room / SQLite dependency and `data/AnimDatabase.kt` for local learner profiles and learning-session records. The database layer is added but must still be wired into the Compose screens.
- Lottie Compose dependency for animation playback. Add your own licensed JSON assets under `app/src/main/assets/`.
- `FIREBASE_SETUP.md` explains the steps that require your own Firebase project and real configuration file. No fake credentials are included.

**Honest implementation status:** The app's current screens use SharedPreferences for profile/settings/counters. Room is present as a database layer but is not yet the source of truth for the screens. The web dashboard is a standalone prototype and is not yet connected to the mobile app. Firebase sync is not active until a real Firebase project is configured and the authentication/security rules are implemented.

## Fixes in this corrected ZIP

The previous ZIP could not be opened and synced by Android Studio as delivered. Changed here:

1. **Missing Gradle wrapper (the reason the project would not sync).** `gradlew`, `gradlew.bat` and the `gradle/wrapper/` files were absent. They are now included, pinned to Gradle 8.11.1 — Android Gradle Plugin 8.7.3 needs Gradle 8.9 or newer.
2. **Gradle configuration cache switched off.** `org.gradle.configuration-cache=true` conflicted with the kapt annotation-processing step that Room uses. It is now `false`.
3. **Text-to-Speech could not start on Android 11 or newer.** The app targets API 35, and from API 30 the manifest must declare the TTS engine query. Without it, "Hear instruction" and the talk-board cards silently did nothing on modern phones. The `<queries>` block for `android.intent.action.TTS_SERVICE` is now present.
4. **Voice locale fallback.** The voice was locked to `Locale.UK`; on a device without British English voice data the app stayed silent. It now falls back to the device default language.
5. **Added `.gitignore`** so build output and your private `app/google-services.json` are never committed.

Nothing else was altered: screens, activities, counters, the Room database layer and the web dashboard mock-up are unchanged.

### Tooling required
- Android Studio Ladybug (2024.2) or newer — Android Gradle Plugin 8.7.3 and `compileSdk = 35` need it.
- JDK 17 (the version bundled with Android Studio).
- Android SDK Platform 35 (Android Studio will offer to download it).
