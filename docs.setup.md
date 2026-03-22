# OsirisGarden — Full Backend Setup

## Step 1: Get a Gemini API key (free)

1. Go to [aistudio.google.com/apikey](https://aistudio.google.com/apikey)
2. Click **"Create API key"**
3. Copy the key (starts with `AIzaSy...`)
4. In OsirisGarden → ⚙️ Settings → paste your Gemini API key → Save

That's all you need for the full frontend to work — chat, diagnosis, and weather.

---

## Step 2: Optional — Set up n8n for the full backend

n8n gives you richer AI predictions, better Gemini prompts, and a proper backend.

### Install n8n
```bash
# With npm
npm install -g n8n
n8n start

# Or with Docker
docker run -it --rm --name n8n -p 5678:5678 n8nio/n8n
```

Or use [n8n Cloud](https://n8n.io) (free tier available).

### Import the workflow

1. Open n8n at `http://localhost:5678`
2. Click **"+"** → **"Import from file"**
3. Upload `backend/osiris-backend-v3.1.json`
4. Toggle the workflow **ON**
5. Copy the webhook URL: `https://your-n8n.com/webhook/osiris`

### Connect to OsirisGarden

1. In OsirisGarden → ⚙️ Settings
2. Paste your n8n webhook URL
3. Click **Save all settings**
4. Click **"Test n8n connection"** — should show ✅

### Your location (for live weather)

1. In Settings → scroll to **"Your location"**
2. Click **"Auto-detect my location"** or enter coordinates manually
3. Save settings

---

## Architecture
```
Browser
  ↓ (Gemini API key in request)
OsirisGarden Frontend (GitHub Pages)
  ↓ PATH A: n8n webhook (if configured)
  ↓ PATH B: Gemini API directly (if only key is set)

Weather data → Open-Meteo API (always free, no key)
```
