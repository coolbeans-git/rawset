# Testing RAWSET on Android

## 1. Install
1. Push to GitHub, wait for Actions > Build APK, download artifact `rawset-apk`, unzip.
2. Copy `rawset.apk` to the phone, open it, allow "install unknown apps" when prompted.
3. Open RAWSET, allow notifications.

## 2. Smoke test (about 10 minutes)
- [ ] Home loads, starburst animates, ticker scrolls
- [ ] Routines > Templates > Upper Lower > Install + set week; Week tab shows Mon/Tue/Thu/Fri
- [ ] Start today's routine (or any); loading screen appears, stopwatch runs
- [ ] Enter weight and reps, tick set: rest bar appears, phone vibrates at 0, notification shows
- [ ] Set 2 of an exercise to Drop (tap set number): ticking set 1 must NOT start the rest timer
- [ ] Menu > Add warm up sets (target 100): 3 warm-up sets appear on top
- [ ] Menu > Plate calculator (100 kg, bar 20): 25 + 15 per side
- [ ] Pair two exercises in a superset: rest starts only after the second exercise's set
- [ ] Beat a previous weight: PR alert appears
- [ ] Finish > Save: appears in Log history; Stats tab updates
- [ ] Settings > Export backup: share sheet opens; save to Drive/Files
- [ ] Settings > Import (merge) with that file: counts unchanged
- [ ] Close app from recents and reopen: data and any running workout are still there

## 3. Debugging
- Enable Developer options > USB debugging, connect to a PC, open `chrome://inspect` in desktop Chrome, inspect RAWSET to see console errors.
- If notifications or share do nothing, check the console for "Plugins undefined" errors and open an issue with the log.
- `adb logcat | grep -i capacitor` shows native-side errors.

## 4. Quick UI-only test without building
Open www/index.html in a desktop browser, or serve the folder (`npx serve www`) and open the LAN address on the phone. Notifications, vibration and share do not work this way.
