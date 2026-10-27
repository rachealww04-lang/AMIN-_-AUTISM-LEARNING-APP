# Firebase setup for ANIM (adult accounts and cloud sync)

Firebase cannot be connected completely until you create/select a Firebase project. Do not use a made-up `google-services.json`.

1. Open Firebase Console and create a project for ANIM.
2. Add an Android app using package name `com.example.anim` (must match `applicationId` in `app/build.gradle.kts`).
3. Download the real `google-services.json` and place it in `ANIM_Android_Studio/app/google-services.json`. Do not share it publicly.
4. Enable Firebase Authentication > Email/Password for adult accounts.
5. Create Cloud Firestore and Cloud Storage only after configuring rules that restrict each parent/teacher to authorised records. Never leave production rules open.
6. Add the Google Services Gradle plugin using the version recommended by Firebase's current Android setup guide, then add Firebase BoM, Authentication, Firestore and Storage dependencies.
7. Implement adult sign-in and role-based security rules before syncing any child data. Collect guardian consent and minimise identifiable information.

## Current local data layer
`app/src/main/java/com/example/anim/data/AnimDatabase.kt` defines Room entities and queries for learner profiles and learning sessions. It supports offline records and identifies sessions waiting for sync. It is a foundation for integration; the existing screens still use SharedPreferences for their current counters until the next wiring step.

## Lottie animations
The Lottie Compose dependency is included. Place licensed JSON animation files in `app/src/main/assets/` and reference them with `LottieCompositionSpec.Asset("your_animation.json")`. Use slow, low-motion animations and provide a reduced-motion alternative.
