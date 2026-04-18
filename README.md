# Family Allowance Tracker — Setup Guide

This guide walks you through every step, assuming you've never done this before. It will take about 30–40 minutes. Take it slow, don't skip steps, and if anything looks different than described, stop and send me a screenshot.

## Before You Start

**What you need:**
- A computer (not just your phone)
- Your Google account (for Firebase)
- Your GitHub account (`noonangarrettr`)
- These three files from me:
  - `index.html`
  - `database.rules.json`
  - `README.md` (this guide)

**What we're building:**
A website that lives at a GitHub Pages URL, talks to Firebase (Google's database), and can be saved to the home screen of iPhones so it feels like an app.

---

## PART 1 — Create Your Firebase Project

Firebase is where the actual data (scores, history) gets stored.

### Step 1: Open Firebase

1. Go to **https://console.firebase.google.com** in your web browser
2. If it asks you to sign in, use your Google account
3. You'll see a page with a blue card that says **"+ Add project"** or **"Create a project"** — click it

### Step 2: Name your project

1. Under "Project name", type: `family-allowance`
2. Click **Continue**

### Step 3: Skip Google Analytics

1. The next page asks about Google Analytics
2. Click the toggle switch to turn it **OFF** (it doesn't need to be on for this)
3. Click **Create project**
4. Wait about 30 seconds while it sets up, then click **Continue**

You'll now see the Firebase dashboard. Keep this tab open — we'll come back many times.

---

## PART 2 — Turn On the Database

### Step 4: Open Realtime Database

1. On the left side of the Firebase dashboard, look for a menu
2. If you don't see a menu, click the three lines icon (☰) in the top-left
3. Find **Build** in the menu and click it to expand
4. Click **Realtime Database**

### Step 5: Create the database

1. You'll see a button that says **Create Database** — click it
2. A window pops up asking about location
3. Leave the default location (**United States (us-central1)**) and click **Next**
4. Now it asks about security rules — choose **"Start in locked mode"** (we'll fix the rules ourselves later)
5. Click **Enable**

Wait a moment. You'll see an empty database page with a URL at the top that looks like:
`https://family-allowance-XXXXX-default-rtdb.firebaseio.com/`

That URL is your database. Good — leave this tab as is and keep going.

---

## PART 3 — Turn On Sign-In

### Step 6: Open Authentication

1. Go back to the left menu and click **Build** → **Authentication**
2. Click the **Get Started** button

### Step 7: Enable Email/Password sign-in

1. You'll see a list of sign-in providers
2. Click **Email/Password** (the first one)
3. A panel opens on the right. Flip the first switch (**Enable**) to **on**
4. Leave "Email link" off
5. Click **Save**

### Step 8: Create the parent accounts

1. At the top of the Authentication page, click the **Users** tab
2. Click **Add user**
3. Enter:
   - Email: `mom@family.local`
   - Password: (pick something — write it down!)
4. Click **Add user**
5. Click **Add user** again and enter:
   - Email: `dad@family.local`
   - Password: (pick something — write it down!)
6. Click **Add user**

You should now see two users listed. Note: these emails aren't real emails. Firebase won't send anything to them. They're just used as identifiers for signing in.

**Important:** Do NOT create accounts for Rutherford or Oliver here. The app will create their accounts automatically when they first tap their name and set a PIN.

---

## PART 4 — Connect the App to Firebase

### Step 9: Register the app with Firebase

1. Click the **gear icon** ⚙️ at the top-left (next to "Project Overview")
2. Click **Project settings**
3. Scroll down to a section called **"Your apps"**
4. You'll see icons: iOS, Android, and **`</>`** (this one means "web")
5. Click the **`</>`** icon

### Step 10: Register the web app

1. Under "App nickname", type: `family-tracker`
2. **Do NOT** check the box for Firebase Hosting
3. Click **Register app**

### Step 11: Copy your Firebase config

1. Firebase shows you a code block that looks like this:
   ```
   const firebaseConfig = {
     apiKey: "AIzaSyABC123...",
     authDomain: "family-allowance-78994.firebaseapp.com",
     databaseURL: "https://family-allowance-78994-default-rtdb.firebaseio.com",
     projectId: "family-allowance-78994",
     storageBucket: "family-allowance-78994.appspot.com",
     messagingSenderId: "123456789",
     appId: "1:123456789:web:abc123"
   };

   ```
2. **Select the entire `firebaseConfig = { ... };` block**, including the curly braces and semicolon
3. Copy it (Cmd+C or right-click → Copy)
4. Click **Continue to console**

### Step 12: Paste the config into index.html

1. Open `index.html` in a text editor (TextEdit on Mac, Notepad on Windows, or VS Code if you have it)
2. Press Cmd+F (Mac) or Ctrl+F (Windows) to search
3. Search for: `YOUR_API_KEY`
4. You'll find a section that looks like this:
   ```js
   const firebaseConfig = {
     apiKey: "YOUR_API_KEY",
     authDomain: "YOUR_PROJECT.firebaseapp.com",
     ...
   };
   ```
5. Select that entire `const firebaseConfig = { ... };` block (the one in the file, not the one you copied)
6. Paste your real config over it (Cmd+V or Ctrl+V)
7. Save the file (Cmd+S or Ctrl+S)

**Double-check:** The file should still say `const firebaseConfig = {` at the start. Make sure the line with `const firebaseConfig = ` is still there — sometimes pasting removes it.

---

## PART 5 — Set the Security Rules

This part is important. These rules stop anyone who finds your URL from messing with your data.

### Step 13: Go to database rules

1. In Firebase, click **Build** → **Realtime Database** on the left
2. At the top, click the **Rules** tab (next to "Data")

### Step 14: Paste the rules

1. You'll see some default rules in a code box
2. **Delete everything** in that code box (click in it, Cmd+A to select all, delete)
3. Open the file `database.rules.json` in a text editor
4. Copy **everything** in it
5. Paste into the Firebase rules box
6. Click **Publish** at the top

It should say "Rules published". If it shows an error, stop and send me the error — don't keep going.

---

## PART 6 — Put It on GitHub Pages

Now the file lives on your computer. Let's put it online.

### Step 15: Create a new GitHub repository

1. Go to **https://github.com** and sign in (`noonangarrettr`)
2. Click the **+** icon at the top-right and pick **New repository**
3. Repository name: `family-allowance`
4. Leave it **Public** (required for free GitHub Pages)
5. Check **Add a README file**
6. Click **Create repository**

### Step 16: Upload your files

1. On the new repo page, click **Add file** → **Upload files**
2. Drag `index.html` from your computer into the upload area
3. (Optional but recommended) Also drag `database.rules.json` and `README.md` so you have a backup
4. Scroll down, leave the commit message as-is
5. Click **Commit changes**

### Step 17: Turn on GitHub Pages

1. On your repo page, click **Settings** (in the top tabs)
2. On the left sidebar, click **Pages**
3. Under "Build and deployment":
   - **Source**: Deploy from a branch
   - **Branch**: main (and folder: `/ (root)`)
4. Click **Save**

### Step 18: Wait for your site to go live

1. GitHub will say "Your site is being built" or similar
2. Wait 1–3 minutes, then refresh the Pages settings page
3. At the top you'll see: **"Your site is live at https://noonangarrettr.github.io/family-allowance/"**
4. Copy that URL. That's your app!

---

## PART 7 — Test It

### Step 19: First visit on your computer

1. Open the URL in your web browser
2. You should see the "Family" login screen with four buttons: Rutherford, Oliver, Mom, Dad

### Step 20: Sign in as a parent

1. Click **Dad** (or Mom)
2. Enter the password you made earlier
3. Click **Sign In**
4. You should see the main app with "This Week", "Check-In", "History" tabs
5. Try tapping a score (like 3 "Owned" for Self-Management)
6. It should say "Saved" briefly

If it says "Error saving" — the security rules might be wrong. Double-check Part 5.

### Step 21: First-time sign-in for the boys

1. Sign out (tap "Sign out" in the top right)
2. Click **Rutherford**
3. You should see: "Hi Rutherford — set up your PIN"
4. Have him pick a 4-digit PIN, type it, and type it again to confirm
5. Click **Set PIN**
6. He's in! Now when he signs in next time, the screen will just ask for his PIN.

Repeat for Oliver.

---

## PART 8 — Add to Home Screen on Each iPhone

Do this on each iPhone (yours, your wife's, Rutherford's, Oliver's):

1. Open **Safari** (must be Safari, not Chrome)
2. Go to: `https://noonangarrettr.github.io/family-allowance/`
3. Tap the **Share** button (square with arrow pointing up)
4. Scroll down and tap **Add to Home Screen**
5. Name it "Family"
6. Tap **Add**

Now there's a "Family" icon on the home screen. It opens full-screen like a real app.

---

## Common Issues

**"Sign-in failed. Check your password."**
→ You mistyped the password, or the email address in the app doesn't match what you put in Firebase. Check that the parent emails in Firebase are exactly `mom@family.local` and `dad@family.local` (lowercase, no spaces).

**"Error saving"**
→ Security rules issue. Go back to Part 5 and re-paste the rules. Make sure it says "Rules published".

**Score buttons don't do anything**
→ Make sure you're signed in (not stuck on the login screen). If the parent is trying to save for themselves, make sure a boy is selected at the top of the week card.

**Boys got locked out after clearing Safari / getting a new phone**
→ Their PIN still works! The account is in Firebase, not the phone. Just open the app and enter the PIN.

**Forgot a PIN**
→ Send me a message. I'll tell you how to reset it from the Firebase console (it's a 2-minute fix).

---

## Sending Changes Later

If we iterate on the app, I'll give you a new `index.html`. To update:

1. Go to your GitHub repo → `index.html` file
2. Click the pencil icon (Edit)
3. Delete everything, paste the new version
4. Scroll down, click **Commit changes**
5. Wait 1–2 minutes, refresh the app — new version is live

---

Once you've got it running, tell me how it feels. Likely next tweaks:
- Adjust the visual polish
- Add a weekly reminder notification
- A "lock the month" button that prevents any more edits after you pay out
- CSV export
