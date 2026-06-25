# KBAKA — Android project

This is a real Android Studio/Gradle project that wraps your KBAKA web app
in a native WebView, so it installs and runs like a normal Android app —
icon, app name, no browser bar. Your HTML/JS file is bundled inside the app
at `app/src/main/assets/index.html` and runs locally; it still talks to your
Google Apps Script URL over the internet exactly like it does in the browser
today, so the customer sync setup from before still applies.

I can't compile the actual .apk file myself — that step needs Android's
SDK/build tools, which aren't available in my sandbox. But everything below
gets you a real, installable APK with no guesswork. Pick ONE option.

---

## Option A — Easiest: let GitHub build it for you (no installs)

You don't need Android Studio at all for this option.

1. Create a free account at github.com if you don't have one.
2. Create a new repository (it can be Private).
3. Upload **all the files in this folder** to that repository, keeping the
   same folder structure (drag-and-drop on the GitHub website works fine —
   make sure the hidden `.github` folder comes along too; if GitHub's
   upload page doesn't show it, use GitHub Desktop or `git push` instead).
4. Go to the **Actions** tab of your repo. A workflow called
   **"Build KBAKA APK"** will run automatically (takes ~2–4 minutes).
5. When it finishes (green check), click into that run, scroll to
   **Artifacts**, and download **kbaka-debug-apk** — it's a zip containing
   `app-debug.apk`.
6. Send that APK to your phone (e.g. via Google Drive, email, or USB cable),
   tap it, and allow "install from unknown sources" if asked.

If step 3's drag-and-drop is awkward, the command-line version is:
```
cd kbaka-android
git init
git add .
git commit -m "KBAKA android app"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO.git
git push -u origin main
```

---

## Option B — Build it yourself with Android Studio

1. Download and install **Android Studio** (free): https://developer.android.com/studio
2. Open Android Studio → **Open** → select this `kbaka-android` folder.
3. Let it sync (first time it'll download some Android SDK pieces —
   this needs internet and a few minutes).
4. Top menu → **Build → Build Bundle(s)/APK(s) → Build APK(s)**.
5. When it finishes, click the **"locate"** link in the notification, or
   find the file at:
   `app/build/outputs/apk/debug/app-debug.apk`
6. Copy that file to your phone and install it the same way as above.

---

## Notes

- This produces a **debug APK** — perfectly fine for installing on your own
  phone or sharing with friends/customers directly. You only need a signed
  **release** build if you plan to publish it on the Google Play Store —
  ask me if/when you get there and I'll walk you through signing it.
- The app icon is a placeholder I generated to match your red "K" branding —
  swap it any time via Android Studio's **Image Asset** tool if you want a
  different one.
- Internet permission is already included in the manifest, since the app
  needs it to reach your Google Apps Script URL.
