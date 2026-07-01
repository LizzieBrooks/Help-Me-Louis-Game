# Help Me Louis — Android App

This wraps your `Help_Me_Louis_GAME.html` game in a minimal native Android
shell (a fullscreen WebView) so it can be built into a real `.apk`. The game
itself is untouched — it lives at `app/src/main/assets/index.html` and runs
100% offline (no internet permission needed; all audio is embedded).

## 1. Push this to GitHub

```bash
cd HelpMeLouisApp
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/<your-username>/<your-repo>.git
git push -u origin main
```

(Create the empty repo on GitHub first, then run the commands above from
inside this folder.)

## 2. Let GitHub Actions build the APK

Pushing to `main` automatically triggers `.github/workflows/build.yml`, which
builds a debug APK on GitHub's servers (your machine does nothing).

To download it:

1. Go to your repo → the **Actions** tab.
2. Open the latest **Build APK** run.
3. Scroll to **Artifacts** → download `HelpMeLouis-debug-apk` (a zip
   containing `app-debug.apk`).

Artifacts expire after 90 days. For a permanent download link instead, tag a
release:

```bash
git tag v1.0
git push origin v1.0
```

This re-runs the build and attaches `app-debug.apk` directly to a new GitHub
Release on your repo's **Releases** page — a stable link you (or anyone) can
open on a phone to install.

## 3. Install the APK on your phone

1. Download the `.apk` on your Android phone (from the Release page, or copy
   it over from the Artifacts zip).
2. Tap it. Android will ask you to allow installs from that source
   (**Settings → Apps → Install unknown apps**) — allow it just for the app
   you used to download it (e.g. Chrome or Files).
3. Tap **Install**.

This is a **debug-signed** APK — perfectly installable and playable, just not
signed for the Play Store. That's fine for personal use or sharing with
friends.

## Editing the game

Just edit `app/src/main/assets/index.html` directly and push — no other
files need to change. Bump `versionCode`/`versionName` in
`app/build.gradle` if you want each build to look distinct.

## Opening in Android Studio (optional)

You don't need Android Studio at all — GitHub Actions does the building. But
if you want to open the project locally, Android Studio will offer to
generate the missing Gradle wrapper files automatically the first time you
open it (needs internet once, for that).

## Project structure

```
HelpMeLouisApp/
├── .github/workflows/build.yml   # builds the APK on every push
├── app/
│   ├── build.gradle              # app config (package name, SDK versions)
│   └── src/main/
│       ├── AndroidManifest.xml
│       ├── assets/index.html     # <-- your game
│       ├── java/.../MainActivity.kt   # fullscreen WebView wrapper
│       └── res/                  # app name + launcher icon
├── build.gradle
└── settings.gradle
```
