# ShowBot 🎬 — Setup Guide (Gemini — 100% Free!)

---

## Step 1 — Get FREE Gemini API Key (2 mins)

1. Go to **https://aistudio.google.com**
2. Sign in with Google
3. Click **"Get API Key"** → **"Create API Key"**
4. Copy the key (starts with `AIza...`)

---

## Step 2 — Firebase Setup (5 mins, free)

1. Go to **https://console.firebase.google.com**
2. Click **"Add project"** → name it `showbot` → click through
3. Once inside, click **`</>`** (Web icon) → name it `showbot` → Register
4. **Copy the firebaseConfig object** shown on screen
5. Open `public/index.html`, find:
   `// ── PASTE YOUR FIREBASE CONFIG HERE ──`
   Replace the placeholder values with your real config

### Enable Google Sign-In
- Firebase Console → **Authentication** → **Get started** → **Google** → Enable → Save

### Enable Firestore Database
- Firebase Console → **Firestore Database** → **Create database** → **Test mode** → Done

---

## Step 3 — Push to GitHub (2 mins)

1. Go to **github.com** → New repository → name: `showbot` → Create
2. Upload all these files (drag & drop on GitHub) OR run:
   ```bash
   git init
   git add .
   git commit -m "ShowBot first commit"
   git remote add origin https://github.com/YOUR_USERNAME/showbot.git
   git push -u origin main
   ```

---

## Step 4 — Deploy on Vercel (2 mins)

1. Go to **https://vercel.com** → Log in with GitHub
2. Click **"Add New Project"** → Import `showbot` repo → **Deploy**
3. After deploy, go to **Settings → Environment Variables**
4. Add this variable:
   - **Name:** `GEMINI_API_KEY`
   - **Value:** `AIza...` (your key from Step 1)
5. Go to **Deployments** → click the 3 dots → **Redeploy**

---

## Step 5 — Add Vercel URL to Firebase (1 min)

1. Copy your Vercel URL e.g. `showbot-xyz.vercel.app`
2. Firebase Console → **Authentication** → **Settings** → **Authorized domains**
3. Click **Add domain** → paste your Vercel URL (no `https://`) → Add

---

## Done! 🎉 Your app is live!

### Install on Phone
- **Android:** Open in Chrome → tap **"📲 Install App"** button
- **iPhone:** Open in Safari → Share → **"Add to Home Screen"**

### Features
- ✅ Google Sign In
- ✅ Chat history (synced across all devices!)
- ✅ New Chat button
- ✅ Add new shows you watched
- ✅ Notes panel
- ✅ Web search for trending shows (Gemini built-in)
- ✅ Installable as phone app
- ✅ All 242 shows + your reviews baked in
- ✅ 100% FREE — 1500 messages/day

---

## Firestore Security Rules (do this after testing!)

Firebase Console → Firestore → Rules → replace with:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId}/{document=**} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
  }
}
```
