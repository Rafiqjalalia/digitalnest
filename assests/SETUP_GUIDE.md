# 🚀 Digitalnest — Setup Guide

## What you received
| File | Purpose |
|------|---------|
| `index.html` | Your public storefront — customers see this |
| `admin.html` | Your private dashboard — add & delete products |

---

## STEP 1 — Create a Firebase Project (5 minutes)

1. Go to **[https://console.firebase.google.com](https://console.firebase.google.com)**
2. Click **"Add project"** → name it `digitalnest` → continue
3. Disable Google Analytics (not needed) → **Create project**
4. Click **"Web"** icon (`</>`) to register a web app
5. Name it `digitalnest-web` → click **Register app**
6. You'll see a `firebaseConfig` object — **copy it**

---

## STEP 2 — Paste Firebase Config

Open **both** `index.html` and `admin.html` in a text editor (Notepad++, VS Code).

Find this block near the bottom of each file:

```js
const firebaseConfig = {
  apiKey:            "PASTE_YOUR_API_KEY",
  authDomain:        "PASTE_YOUR_AUTH_DOMAIN",
  projectId:         "PASTE_YOUR_PROJECT_ID",
  storageBucket:     "PASTE_YOUR_STORAGE_BUCKET",
  messagingSenderId: "PASTE_YOUR_MESSAGING_SENDER_ID",
  appId:             "PASTE_YOUR_APP_ID"
};
```

Replace the placeholder values with the real values from Firebase Console.
**Do this in BOTH files.**

---

## STEP 3 — Create Firestore Database

1. In Firebase Console, click **"Firestore Database"** in the left sidebar
2. Click **"Create database"**
3. Choose **"Start in test mode"** (for now) → **Next**
4. Choose your region (e.g. `asia-south1` for Pakistan) → **Enable**

---

## STEP 4 — Set Firestore Security Rules

In Firebase Console → Firestore → **Rules** tab, paste this:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Anyone can READ products (your customers)
    match /products/{docId} {
      allow read: if true;
      // Only YOU can write — use a secret password in URL
      allow write: if request.auth == null &&
                      request.resource.data.adminSecret == "YOUR_SECRET_HERE";
    }
  }
}
```

> **Simpler option for now:** Keep "test mode" (all reads/writes allowed for 30 days).
> Come back and update rules before going live.

---

## STEP 5 — Add Your First Product

1. Open `admin.html` in your browser (or on Netlify)
2. Click **"Add Product"** in the sidebar
3. Fill in:
   - **Title**: `1000+ AI Doctor Health Reels`
   - **Price**: `399`
   - **Category**: `AI & Tech`
   - **Image URL**: Upload your image to [imgur.com](https://imgur.com) → right-click → Copy image address
   - **Description**: Short one-liner about the bundle
4. Click **Add Product**

The product will instantly appear on `index.html` for your customers!

---

## STEP 6 — Deploy to Netlify (FREE)

1. Go to **[https://netlify.com](https://netlify.com)** → Sign up free
2. Drag and drop your entire project folder onto the Netlify dashboard
3. Your store is live! You'll get a URL like `https://digitalnest-xyz.netlify.app`

---

## How Customers Buy

Every product card has a **"Buy Now"** button that opens WhatsApp with this pre-filled message:

```
Hi Digitalnest! I want to buy the [Product Title] for Rs. [Price].
Please send payment details.
```

You respond with your **JazzCash / SadaPay** number, they pay, you send the file link. ✅

---

## Technology Stack

| Technology | What it does |
|-----------|-------------|
| **HTML + CSS** | Structure and styling |
| **Tailwind CSS** (CDN) | Utility CSS — no install needed |
| **Firebase Firestore** | Your product database — free tier is plenty |
| **Firebase JS SDK** | Connects your pages to the database |
| **Google Fonts** | Syne + DM Sans fonts |
| **Font Awesome** | Icons |
| **Netlify** | Free hosting with drag & drop |

**No Node.js, no server, no npm required.** Everything runs in the browser. 🎉

---

## Quick Troubleshooting

| Problem | Fix |
|---------|-----|
| Products not loading | Check Firebase config is pasted correctly in both files |
| "Permission denied" error | Make sure Firestore is in test mode |
| Images not showing | Use a direct image URL (Imgur works great) |
| WhatsApp link not working | Check your phone number is `923025051252` format |
