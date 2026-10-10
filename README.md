# Pooja schedule app – setup (Firebase + GitHub Pages)

Files: `index.html` (the app), `firestore.rules` (who may open the data).

## 1. Firebase (free "Spark" plan)
1. Go to https://console.firebase.google.com → **Add project** → name it (e.g. `thalayakulam-pooja`). Google Analytics can be off.
2. **Build → Authentication → Get started → Sign-in method → Google → Enable** → choose a support email → Save.
3. **Build → Firestore Database → Create database** → pick a location near you (e.g. `asia-south1` Mumbai) → **Start in production mode**.
4. Firestore → **Rules** tab → replace everything with the contents of `firestore.rules`, put the real Google email addresses of everyone who may use the app in the list, then **Publish**.
5. **Project settings (gear icon) → General → Your apps → Web (`</>`)** → register an app (no hosting needed). Copy the `firebaseConfig` values.
6. Open `index.html` in a text editor and replace the four `PASTE_...` values near the top (`apiKey`, `authDomain`, `projectId`, `appId`) with yours. (These values are not secrets; the rules above protect the data.)

## 2. GitHub Pages (free)
1. Create a GitHub account → **New repository** (public, e.g. `pooja-schedule`).
2. **Add file → Upload files** → upload `index.html` → Commit.
3. Repo **Settings → Pages** → Source: **Deploy from a branch** → branch `main`, folder `/ (root)` → Save.
4. After a minute the site is at `https://<your-github-username>.github.io/pooja-schedule/`.

## 3. Allow the website to sign in
Firebase → **Authentication → Settings → Authorized domains → Add domain** → `<your-github-username>.github.io` (domain only, no path).

## 4. Use it
Open the site address, sign in with Google. Then in **Bookings → Import from Excel**, upload your existing file once. Everyone signed in sees the same bookings and months live.

## Adding or removing a user later
Edit the email list in Firestore → Rules → Publish.

## Notes
- Data lives in Firestore documents `pooja/bookings` and `pooja/months`. Use **Backup (JSON)** now and then; **Restore** loads a backup.
- If two people edit at the same moment, the last save wins.
- Check Firebase's current free-plan limits; a temple team's usage is very small.
