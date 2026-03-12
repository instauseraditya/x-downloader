# X Video Downloader — Free Setup Guide
## Stack: Python (Flask + yt-dlp) · Railway (free backend) · GitHub Pages (free frontend)

---

## 📁 Project Structure

```
x-downloader/
├── backend/
│   ├── app.py           ← Flask API
│   ├── requirements.txt ← Python dependencies
│   ├── Procfile         ← Railway start command
│   └── railway.json     ← Railway config
└── frontend/
    └── index.html       ← Your UI (host anywhere)
```

---

## STEP 1 — Deploy Backend to Railway (Free)

### 1.1 Create a GitHub repo for the backend

1. Go to https://github.com/new
2. Name it: `x-downloader-backend`
3. Set to **Public** (Railway free tier works with public repos)
4. Click **Create repository**

### 1.2 Push your backend files

Open a terminal and run:

```bash
cd x-downloader/backend

git init
git add .
git commit -m "Initial backend"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/x-downloader-backend.git
git push -u origin main
```

### 1.3 Deploy on Railway

1. Go to https://railway.app and sign up (free — use GitHub login)
2. Click **New Project** → **Deploy from GitHub repo**
3. Select your `x-downloader-backend` repo
4. Railway auto-detects Python and installs from `requirements.txt`
5. Wait ~2 minutes for the build to finish
6. Click your project → **Settings** → **Domains** → click **Generate Domain**
7. Copy your domain — it looks like: `https://x-downloader-backend.up.railway.app`

### 1.4 Test your backend

Open this URL in browser (replace with your domain):

```
https://YOUR_RAILWAY_URL/health
```

You should see: `{"status": "ok"}`

---

## STEP 2 — Set Your Backend URL in the Frontend

Open `frontend/index.html` and find this line near the bottom:

```javascript
const BACKEND_URL = 'YOUR_RAILWAY_URL';
```

Replace it with your Railway domain:

```javascript
const BACKEND_URL = 'https://x-downloader-backend.up.railway.app';
```

---

## STEP 3 — Host Frontend for Free (GitHub Pages)

### 3.1 Create another GitHub repo

1. Go to https://github.com/new
2. Name it: `x-downloader` (or anything you like)
3. Set to **Public**
4. Click **Create repository**

### 3.2 Push your frontend

```bash
cd x-downloader/frontend

git init
git add .
git commit -m "Frontend"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/x-downloader.git
git push -u origin main
```

### 3.3 Enable GitHub Pages

1. Go to your repo on GitHub
2. Click **Settings** → **Pages** (left sidebar)
3. Under **Source**, select **Deploy from branch**
4. Branch: `main`, folder: `/ (root)`
5. Click **Save**
6. Wait ~1 minute — your site will be live at:
   `https://YOUR_USERNAME.github.io/x-downloader`

---

## ✅ You're Done!

Your full free setup:

| Part     | Service       | Cost | URL                                              |
|----------|---------------|------|--------------------------------------------------|
| Backend  | Railway       | FREE | https://x-downloader-backend.up.railway.app      |
| Frontend | GitHub Pages  | FREE | https://YOUR_USERNAME.github.io/x-downloader     |

---

## 🔧 Troubleshooting

**"Could not reach the backend"**
→ Check your Railway app is running (green dot in dashboard)
→ Make sure BACKEND_URL in index.html has no trailing slash

**"Could not extract video"**
→ The post may be from a private/protected account
→ yt-dlp may need updating: Railway will auto-update on redeploy

**Railway free tier limits**
→ 500 hours/month of runtime (enough for personal use)
→ App sleeps after inactivity — first request may take ~5 seconds to wake up

**To redeploy after changes**
→ Just push to GitHub — Railway auto-deploys on every push

---

## 🔄 Keeping yt-dlp Updated

X sometimes changes its API. If downloads stop working, update yt-dlp:

1. Edit `requirements.txt` — change the yt-dlp version to latest
2. Commit and push to GitHub
3. Railway will auto-redeploy with the new version

Check latest version at: https://github.com/yt-dlp/yt-dlp/releases
