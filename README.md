# YouTube Downloader

A clean, self-hosted YouTube downloader with a minimal dark UI. Paste a link, pick your settings, and download straight to your machine — no accounts, no tracking, no nonsense.

---

## How it works

The frontend (`index.html`) talks to a local Express server (`server.js`) running on **port 3000**. The server shells out to `yt-dlp` to fetch video info and handle downloads. Files are temporarily written to your system's temp directory and streamed to the browser, then deleted automatically.

---

## Requirements

| Tool | Install |
|------|---------|
| [Node.js](https://nodejs.org) | Download from nodejs.org |
| yt-dlp | `winget install yt-dlp` |
| FFmpeg | Installed automatically alongside yt-dlp |

> **FFmpeg is required** for merging video and audio streams. It ships with yt-dlp when installed via winget, so no separate setup is needed.

---

## Setup

**1. Install yt-dlp** (includes FFmpeg):

```bash
winget install yt-dlp
```

**2. Install Node dependencies:**

```bash
npm init -y
npm install express cors
```

This generates `package.json` and installs `express` and `cors` — the only two runtime dependencies.

---

## Running

**1. Start the server:**

```bash
node server.js
```

You should see:
```
✅ Server running at http://localhost:3000
```

**2. Open the frontend:**

Open `index.html` directly in your browser (no separate web server needed).

**3. Use it:**

- Paste a YouTube URL — a preview will appear automatically
- Pick your resolution and codec
- Click **Fetch** and wait for the download to process
- Click **Download** when it turns green

> The server must be running in the background whenever you use the app. Keep the terminal open.

---

## Project Structure

```
├── server.js       # Express backend — handles yt-dlp, job queue, file streaming
├── fetcher.js      # Frontend JS — API calls, polling, download trigger
├── index.html      # UI — paste URL, pick settings, trigger download
├── global.css      # Styles
├── package.json
└── README.md
```

---

## Resolution & Codec Notes

| Resolution | Codec Behavior |
|------------|----------------|
| Best / 4K / 1440p | Always VP9 or AV1 — YouTube doesn't offer H.264 above 1080p |
| 1080p / 720p | Codec selection applies (H.264, H.265, VP9, AV1) |
| MP3 | Extracts audio only — resolution setting is ignored |

If the requested codec isn't available for a video, the server automatically falls back to the next best available format rather than failing.

---

## Troubleshooting

**"Could not fetch video info" or download fails**
- Make sure `node server.js` is running and the terminal shows the `✅` line
- Run `yt-dlp --version` in a terminal to confirm it's installed and on your PATH
- Try restarting the server if it's been running for a while

**yt-dlp not found**
- After `winget install yt-dlp`, open a **new** terminal window before running the server — the PATH won't update in an already-open terminal

**Port 3000 already in use**
- Something else is using port 3000. Change the port at the bottom of `server.js` (`app.listen(3000, ...)`) and update the `SERVER` constant at the top of `fetcher.js` to match.

---

> This tool is for personal use. Respect copyright and YouTube's Terms of Service when downloading content.
