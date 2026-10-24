# Family Hub – setup (GitHub Pages + free Firebase sync)

## Part 1 – Firebase (shared data between family devices)
1. Go to https://console.firebase.google.com → **Add project** (name it e.g. `family-hub`, turn Google Analytics off).
2. **Build → Authentication → Get started → Sign-in method → Anonymous → Enable → Save.**
3. **Build → Firestore Database → Create database** → production mode → choose a nearby region.
4. In Firestore, open the **Rules** tab, replace everything with the text below, then **Publish**:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /families/{code} {
      allow get, create, update: if request.auth != null;
    }
  }
}
```
5. **Project settings (gear icon) → General → Your apps → Web (</>)** → register the app (skip Hosting) → copy the `firebaseConfig` values.
6. Open `firebase-config.js` and replace `PASTE_API_KEY`, `PASTE_PROJECT_ID` (two places) and `PASTE_APP_ID`.

## Part 2 – GitHub Pages
1. Create a GitHub account if needed, then **New repository** (e.g. `family-hub`, Public).
2. **Add file → Upload files**: upload every file from this folder (index.html, firebase-config.js, manifest.webmanifest, sw.js and the three .png icons), then **Commit**.
3. **Settings → Pages → Build and deployment**: Source = *Deploy from a branch*, Branch = `main`, folder `/ (root)` → **Save**.
4. After about a minute your app is at `https://YOUR-USERNAME.github.io/family-hub/`.

## Part 3 – Use it
- On first open, each device asks for the **family code**. Use the same long, private phrase on every device (at least 8 characters). It acts as the family password and is NOT stored in GitHub. Tap the status text at the top right to change it later.
- **iPhone/iPad:** open the address in Safari → Share → **Add to Home Screen**. It opens full screen like an app.
- **Android/Chrome:** menu → **Install app**.
- Set the parent PIN in **Parent mode** on first use.

## Notes
- Anyone who knows your family code can read and edit your family data. Keep it private.
- If sync fails, check that Anonymous sign-in is enabled and the rules were published.
- Reminders and notifications only work while the app is open.
