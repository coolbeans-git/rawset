# RAWSET_

Open-source workout logger for Android. Dot-matrix, grid-based generative UI (beige + maroon), ticker header, offline-first, no account, no tracking.
Independent clone of the *feature set* of popular gym loggers. No third-party code, assets or trademarks are used.

## Features (v0.1 — Workout Logging)
- Start empty workout, live stopwatch
- Per-exercise custom notes (persist between workouts)
- Automatic rest timer (−15/+15/skip, per-exercise override, skipped before drop sets and mid-superset)
- Add / remove sets
- Set types: Normal, Warm up, Failure, Drop
- Previous workout values (tap to copy)
- Warm-up set calculator (editable % × reps formula, rounding)
- Weight plate calculator (per side, bar weight configurable)
- RPE column (toggle in settings)
- Supersets / circuits (colour-coded)
- Save workout + history, repeat, delete, JSON export
- Live PR notification (weight, est. 1RM, volume)
- Live Activity equivalent: ongoing Android notification
- Stats tab: consistency grid + weekly streak, sets per muscle group (7d), per-exercise charts (est. 1RM / max weight / volume), body measurements
- Backup: export via Android share sheet, import as merge or full replace
- Routines with folders (create, edit, duplicate, move, delete)
- Weekly schedule: assign a routine to each weekday; "today" card on the log tab
- Templates: Bro Split (6d), Push/Pull/Legs (6d), Arnold Split (6d), Upper/Lower (4d)

## Build the APK
**Easiest:** push to GitHub; Actions builds `rawset.apk` (Actions tab → latest run → Artifacts).
**Locally:** Node 20, JDK 17, Android SDK.
```
npm install
npx cap add android
npx cap sync android
cd android && ./gradlew assembleDebug
# APK: android/app/build/outputs/apk/debug/app-debug.apk
```
Edit `www/index.html`, run `npx cap sync android`, rebuild.

## Roadmap
Exercise library with media, progress photos, monthly report, Health Connect.

MIT licensed.

## Testing on a phone
See TESTING.md.
