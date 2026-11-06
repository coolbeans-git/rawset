# Phase 1: navigation and global workout session (v0.2.0)

## Before you install (protects your logged workouts)
1. In the CURRENT app: Settings > Export backup > save to Files/Drive. Open the saved file once to confirm it is not empty.
2. Optional but recommended, makes this the last forced reinstall: create a stable signing key.
   keytool -genkeypair -v -keystore debug.keystore -storepass android -alias androiddebugkey -keypass android -keyalg RSA -keysize 2048 -validity 10000 -dname "CN=Android Debug,O=Android,C=US"
   Mac: base64 -i debug.keystore | tr -d '\n'   (Linux: base64 -w0 debug.keystore)
   GitHub repo > Settings > Secrets and variables > Actions > New repository secret: name DEBUG_KEYSTORE_B64, value = the base64 text. Keep debug.keystore somewhere safe.
3. Push the new files, wait for Build APK, install. If Android says "App not installed", uninstall the old RAWSET (this erases its data), install the new one, then Settings > Import (merge) with your backup.

## Navigation model
- Tabs: STATS (default on every launch), HISTORY, ROUTINES, WEEK. Tabs are siblings; back from another tab goes to STATS.
- Screens above tabs: active workout (wk) and routine editor (ed). Back pops one screen; it never discards a workout.
- Modals: back closes the top modal; drill-down modals (template preview, weekdays, move to folder, warm-up, plates, superset) go back to their parent menu first.
- Root (STATS, nothing open): first back shows "PRESS BACK AGAIN TO EXIT", second within 2 s exits.
- Routine editor: back with unsaved changes asks SAVE / DISCARD / KEEP EDITING. A draft survives app kill; ROUTINES shows "RESUME EDITING".
- Active workout lives in S.cur, editor draft in S.ed (separate). Starting a second workout while one is active resumes the first.
- Bar at the bottom of every other screen shows the active workout; tap to resume.

## Data migration
Only one: if an older build stored a routine-editor draft inside S.cur (edit flag), it moves to S.ed on first launch. Workouts, routines, history, settings are unchanged. New optional field: routine.used (timestamp) for "recent routines".

## Device checklist (not verifiable off-device)
- [ ] Back on STATS: toast, second back within 2 s exits; app reopens on STATS with your workout still running
- [ ] Start workout, open exercise menu > warm-up: back, back, back = menu, workout, tabs (workout kept)
- [ ] Gesture back behaves the same as the button
- [ ] Swipe app from recents mid-workout, reopen: workout, sets, notes, elapsed time intact
- [ ] Edit a routine while a workout is active: workout unaffected
- [ ] Rest timer visible on all tabs while resting (note: persistence and background notification are Phase 2)
