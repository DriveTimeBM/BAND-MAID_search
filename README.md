# BAND-MAID Video Search

A minimal, client-side YouTube search page targeting BAND-MAID and BAND-MAIKO content.

## How it works

- Searches YouTube Data API v3 for recent BAND-MAID / BAND-MAIKO videos
- Applies a client-side regex filter (`\bband[-\s]?mai(?:d|ko)\b`) to drop false positives
- Sorted by date, filterable by recency, with pagination

## Setup

### 1. Get a YouTube Data API v3 key

1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Create or select a project
3. Enable **YouTube Data API v3**
4. Create an API key under **APIs & Services → Credentials**

### 2. Restrict the key (important)

In the API key settings:

- **Application restrictions** → HTTP referrers
- Add your GitHub Pages URL: `https://yourusername.github.io/*`
- Add local dev: `http://localhost:*` and `http://127.0.0.1:*`

Also set a daily **quota cap** under *YouTube Data API v3 → Quotas* — default is 10,000 units/day; each search costs ~100 units.

### 3. Add your key locally

```
cp config.template.js config.js
# Edit config.js and replace YOUR_API_KEY_HERE with your real key
```

`config.js` is listed in `.gitignore` — it will never be committed.

### 4. Deploy to GitHub Pages

```bash
git init
git add index.html config.template.js .gitignore README.md
git commit -m "initial"
git remote add origin https://github.com/yourusername/bm-search.git
git push -u origin main
```

Enable GitHub Pages in the repo settings (Branch: `main`, folder: `/`).

Visitors to your GitHub Pages URL need `config.js` to exist. Since it's gitignored, they'll see the API key error message — this page is meant for your own use, not public distribution of the key.

## Files

| File | Purpose |
|---|---|
| `index.html` | The entire app |
| `config.js` | Your API key — **gitignored, never commit** |
| `config.template.js` | Safe placeholder committed to the repo |
| `.gitignore` | Excludes `config.js` |
