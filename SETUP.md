# Anvi's Prelim Tracker: setup guide

Files you need to upload: `index.html` and `apple-touch-icon.png`.

You can use the site right after Part B. Without Part A it works on each phone separately (marks stay on that phone). Part A makes all three phones share the same marks.

---

## Part A: shared data with Firebase (about 10 minutes)

1. Go to https://console.firebase.google.com and sign in with your Google account.
2. Click **Create a project**. Name it `anvi-tracker`. Turn **Google Analytics off**. Click Create.
3. **Database and rules**
   - In the left menu choose **Build, then Firestore Database**, then **Create database**.
   - Location: **asia-south1 (Mumbai)**. Choose **Production mode**. Click Enable.
   - Open the **Rules** tab, delete everything, paste the rules below, and click **Publish**.

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /families/{code}/{document=**} {
      allow read, write: if code.size() >= 10;
    }
  }
}
```

   These rules let the app read and write only under your family code. Nobody can list the codes, so the code works like a password.

4. **Get your web app details**
   - Click the gear icon, then **Project settings**.
   - Under **Your apps**, click the **web icon `</>`**, name it `tracker`, leave Hosting unticked, click Register app.
   - You will see a block called `firebaseConfig`. Copy each value into the matching line at the top of `index.html` (inside the quotes, replacing `PASTE_HERE`).
   - These values are not secrets. Keep your family code out of this file.

## Part B: put it online with GitHub Pages (about 5 minutes)

5. On github.com click **New repository**. Name it `anvi-tracker`. Choose **Public** (free GitHub Pages needs this). Click Create.
6. Click **uploading an existing file**, drag in `index.html` and `apple-touch-icon.png`, and click **Commit changes**.
7. Go to **Settings, then Pages**. Under Build and deployment choose **Deploy from a branch**, branch **main**, folder **/ (root)**, then Save.
8. After a minute your site is live at `https://YOUR-GITHUB-USERNAME.github.io/anvi-tracker/`.

If you change `index.html` later, upload the new file over the old one and wait a minute.

## Part C: on each phone

9. Open the site link in the phone's browser.
10. Enter the **family code** once. Pick something long that only the family knows (at least 10 letters or digits, no spaces), for example `anvi2027-boards-xyz`. Use **the same code on all three phones**. The page shows the last 3 characters of the code at the bottom so you can check they match.
11. Add it to the home screen.
    - **iPhone (Safari):** tap Share, then **Add to Home Screen**.
    - **Android (Chrome):** tap the three dots, then **Add to Home screen**.

## Good to know

- If the tracker looks empty on a new phone, the family code was probably typed differently. Tap **Forget code on this phone** and enter it again.
- Anyone who knows the family code can see and change the marks. Treat it like a password.
- Reminders: in the Upcoming tab, use **Download calendar file**, import it at calendar.google.com (Settings, then Import), and set that calendar's notification for all-day events to 2 days before.
- Firebase's free plan is far more than a family tracker needs.
